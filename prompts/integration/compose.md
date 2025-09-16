# Docker Compose Integration Generator

## Goal
Generate a complete Docker Compose setup that orchestrates all services, databases, and dependencies for local integration testing. This creates a one-command solution to run the entire system locally.

## Operational Modes

### 1. **`New` Mode** (mode=new)
- No existing integration setup
- Generate complete Docker Compose environment from scratch
- Create all supporting files and scripts

### 2. **`Update` Mode** (mode=update)
- Integration setup exists
- Update to reflect new services or changes
- Preserve custom configurations where possible

## Preparation

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: Database technology, message queue, cache, containerization
   - Persists across project resets
2. **Phase Preferences** (`workspace/code/integration/preferences.md`):
   - Always check: Contains integration-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making integration decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.


### Read Core Documents
1. **Architecture**: `workspace/output/architecture/architecture.md`
   - Identify all services and their relationships
   - Note startup dependencies from "Orchestration Requirements"
   - Map inter-service communication patterns

2. **Service Specifications**: `workspace/output/services/{service}/service.md`
   - Tech stack for each service
   - Database requirements
   - "Deployment Requirements" section for environment variables
   - Port allocations

3. **API Specifications**: `workspace/output/api/*.md`
   - Port numbers for each service
   - Authentication mechanisms
   - Base URLs for service discovery

4. **Actual Code**: `workspace/code/{service}/`
   - Dockerfile (must exist from Development phase)
   - `.env.example` files
   - Package files (package.json, requirements.txt, go.mod)
   - Migration scripts location
   - Configuration files

## Process

### Step 1: Service Analysis
For each service found in `workspace/code/`:
1. Verify Dockerfile exists
2. Extract environment variables from code and specs
3. Identify database type and version needed
4. Note port allocation (default or specified)
5. Determine health check endpoint
6. Map dependencies on other services

### Step 2: Database Discovery
Identify all unique databases needed:
- PostgreSQL instances
- MongoDB instances
- Redis instances
- MySQL instances
- Other data stores

For each database:
- Determine appropriate version
- Plan initialization approach
- Identify services that use it

### Step 3: Generate Docker Compose

Create `workspace/code/integration/docker-compose.yml`:

```yaml
services:
  # Databases first (no dependencies)
  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: dbuser
      POSTGRES_PASSWORD: dbpass
      POSTGRES_DB: maindb
    volumes:
      - ./databases/postgres-init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U dbuser"]
      interval: 10s
      timeout: 5s
      retries: 5

  # Services with proper dependencies
  accounts:
    build: ../accounts
    ports:
      - "3001:3000"
    environment:
      DATABASE_URL: postgresql://dbuser:dbpass@postgres:5432/maindb
      PORT: 3000
      NODE_ENV: development
    depends_on:
      postgres:
        condition: service_healthy
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  trading:
    build: ../trading
    ports:
      - "3002:3000"
    environment:
      DATABASE_URL: postgresql://dbuser:dbpass@postgres:5432/maindb
      ACCOUNTS_SERVICE_URL: http://accounts:3000
      PORT: 3000
    depends_on:
      postgres:
        condition: service_healthy
      accounts:
        condition: service_healthy
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

networks:
  default:
    name: integration-network

volumes:
  postgres-data:
  mongo-data:
  redis-data:
```

### Step 4: Generate Environment Configuration

Create `workspace/code/integration/.env.example`:
```env
# Database Configuration
POSTGRES_USER=dbuser
POSTGRES_PASSWORD=dbpass
POSTGRES_DB=maindb
MONGO_INITDB_ROOT_USERNAME=mongouser
MONGO_INITDB_ROOT_PASSWORD=mongopass

# Service Ports (external:internal)
ACCOUNTS_PORT=3001:3000
TRADING_PORT=3002:3000
MARKET_PORT=3003:3000

# Service URLs (for internal communication)
ACCOUNTS_SERVICE_URL=http://accounts:3000
TRADING_SERVICE_URL=http://trading:3000
MARKET_SERVICE_URL=http://market:3000

# External APIs (if needed)
EXTERNAL_API_KEY=demo-key-for-testing
```

### Step 5: Generate Database Initialization

For PostgreSQL, create `workspace/code/integration/databases/postgres-init.sql`:
```sql
-- Create schemas for each service
CREATE SCHEMA IF NOT EXISTS accounts;
CREATE SCHEMA IF NOT EXISTS trading;
CREATE SCHEMA IF NOT EXISTS market;

-- Grant permissions
GRANT ALL ON SCHEMA accounts TO dbuser;
GRANT ALL ON SCHEMA trading TO dbuser;
GRANT ALL ON SCHEMA market TO dbuser;

-- Any shared lookup tables
CREATE TABLE IF NOT EXISTS public.currencies (
    code VARCHAR(3) PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

INSERT INTO public.currencies (code, name) VALUES
    ('USD', 'US Dollar'),
    ('EUR', 'Euro'),
    ('GBP', 'British Pound');
```

### Step 6: Generate Supporting Scripts

Create `workspace/code/integration/scripts/wait-for-it.sh`:
```bash
#!/usr/bin/env bash
# Wait for a service to become available
# Usage: ./wait-for-it.sh host:port [-t timeout] [-- command args]
# (Include standard wait-for-it implementation)
```

Create `workspace/code/integration/scripts/seed-data.sh`:
```bash
#!/bin/bash
echo "Seeding demo data..."

# Wait for services to be ready
./scripts/wait-for-it.sh accounts:3000 -t 60
./scripts/wait-for-it.sh trading:3000 -t 60

# Seed accounts service
curl -X POST http://localhost:3001/api/seed \
  -H "Content-Type: application/json" \
  -d '{"demo": true}'

echo "Demo data seeded successfully"
```

### Step 7: Generate Makefile

Create `workspace/code/integration/Makefile`:
```makefile
.PHONY: help up down logs ps test seed clean build

help: ## Show this help message
	@echo 'Usage: make [target]'
	@echo ''
	@echo 'Available targets:'
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-15s %s\n", $$1, $$2}'

up: ## Start all services
	docker-compose up -d
	@echo "Waiting for services to be healthy..."
	@sleep 10
	@make ps

down: ## Stop all services
	docker-compose down

logs: ## Show logs from all services
	docker-compose logs -f

ps: ## Show status of all services
	docker-compose ps

build: ## Rebuild all service images
	docker-compose build --no-cache

test: ## Run integration tests
	@echo "Running integration tests..."
	./scripts/run-tests.sh

seed: ## Seed demo data
	./scripts/seed-data.sh

clean: ## Clean up volumes and networks
	docker-compose down -v
	docker network prune -f
```

### Step 8: Generate README

Create `workspace/code/integration/README.md`:
```markdown
# Integration Testing Environment

This directory contains the Docker Compose setup for running all services together for local testing.

## Prerequisites

- Docker and Docker Compose installed
- All services must have their Dockerfiles created
- Ports 3001-3010 and 5432 should be available

## Quick Start

1. Copy environment file:
   ```bash
   cp .env.example .env
   ```

2. Start all services:
   ```bash
   make up
   ```

3. View logs:
   ```bash
   make logs
   ```

4. Seed demo data (optional):
   ```bash
   make seed
   ```

5. Stop all services:
   ```bash
   make down
   ```

## Services

| Service | Port | Health Check |
|---------|------|--------------|
| accounts | 3001 | http://localhost:3001/health |
| trading | 3002 | http://localhost:3002/health |
| market | 3003 | http://localhost:3003/health |
| postgres | 5432 | - |

## Troubleshooting

- If services fail to start, check logs: `docker-compose logs [service-name]`
- To rebuild images: `make build`
- To clean everything: `make clean`

## Development Workflow

1. Make changes to service code
2. Rebuild the affected service: `docker-compose build [service-name]`
3. Restart the service: `docker-compose restart [service-name]`
4. Check logs: `docker-compose logs -f [service-name]`
```

## Quality Checks

Before completing:
- [ ] All services from architecture are included
- [ ] All databases are properly configured
- [ ] Dependencies are correctly ordered
- [ ] Health checks are implemented
- [ ] Environment variables are documented
- [ ] Port mappings avoid conflicts
- [ ] Network is properly configured
- [ ] Volumes persist necessary data
- [ ] Makefile commands work correctly
- [ ] README provides clear instructions

## Output Structure

The complete integration setup at `workspace/code/integration/`:
```
integration/
├── docker-compose.yml        # Main orchestration file
├── .env.example             # Environment variables template
├── Makefile                 # Convenience commands
├── README.md               # Documentation
├── databases/
│   ├── postgres-init.sql   # PostgreSQL initialization
│   └── mongo-init.js       # MongoDB initialization (if needed)
├── scripts/
│   ├── wait-for-it.sh     # Service readiness check
│   ├── seed-data.sh       # Demo data seeding
│   └── run-tests.sh       # Integration test runner
└── config/
    └── service-urls.env    # Service discovery configuration
```

## Custom Roles
- Use `roo-arch` custom mode throughout
- Read all specifications and code to generate comprehensive setup
- Focus on developer experience and ease of use