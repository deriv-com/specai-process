# Integration Orchestration Workflow

## Goal

This prompt orchestrates the creation of a complete local development environment using Docker Compose. It brings together all developed services into a cohesive, runnable system with proper networking, dependencies, and configuration.

**Flow**: Service Discovery → Environment Analysis → Docker Compose Generation → Testing Setup → Documentation

## Operational Modes Support

When creating the integration setup, you can use three modes:
- `mode=new`: First-time integration setup creation
- `mode=update`: Update existing setup when services change
- `mode=review`: Review and modify integration preferences

## Preparation

### Required Reading
1. **Architecture Document**
   - READ `workspace/output/architecture/architecture.md`: To understand service relationships and orchestration requirements
   - Extract orchestration requirements for each service (ports, dependencies, health checks)

2. **Service Implementations**
   - Check `workspace/code/*/` directories for all implemented services
   - Verify each service has a Dockerfile
   - Check for .env.example files in each service

3. **Service Specifications**
   - READ service specifications from `workspace/output/services/*/service.md` for deployment requirements
   - Note database requirements and external dependencies

4. **Development Guidelines**
   - READ `prompts/develop/guideline.md`: For integration readiness requirements

## Process

### Step 1: Service Discovery and Analysis

Identify all implemented services:
- List all directories in `workspace/code/`
- For each service, verify:
  - Dockerfile exists and is properly configured
  - Health check endpoint is implemented
  - Environment variables are documented
  - Database requirements are clear
  - Port assignments don't conflict

Create a service inventory:
```
Services Found:
- Service Name | Port | Database | Health Check | Dependencies
- trading      | 3000 | PostgreSQL | /health | accounts, market
- accounts     | 3001 | PostgreSQL | /health | None
- market       | 3002 | Redis | /health | None
```

### Step 2: Determine Integration Mode

- **New Mode**: No docker-compose.yml exists
- **Update Mode**: docker-compose.yml exists and needs updates
- **Review Mode**: User wants to modify integration preferences

### Step 3: Generate Integration Configuration

#### For NEW Integration (mode=new):

1. **Create Docker Compose Configuration**
   Create `workspace/code/integration/docker-compose.yml`:
   - Define all services with proper build contexts
   - Configure environment variables
   - Set up networking (use a custom network for inter-service communication)
   - Define volumes for data persistence
   - Specify health checks
   - Configure startup dependencies
   - Include database services (PostgreSQL, Redis, etc.)
   - Add any required infrastructure (Kafka, ElasticSearch, etc.)

2. **Create Environment Configuration**
   Create `workspace/code/integration/.env.example`:
   - Global environment variables
   - Database connection strings
   - Service URLs for inter-service communication
   - API keys and secrets (with placeholder values)
   - Ports configuration

3. **Create Database Initialization**
   Create `workspace/code/integration/init-scripts/`:
   - Database creation scripts
   - Initial schema setup
   - Seed data if needed
   - User creation for services

4. **Create Utility Scripts**
   Create helpful scripts in `workspace/code/integration/scripts/`:
   - `start.sh`: Start all services with proper order
   - `stop.sh`: Gracefully stop all services
   - `reset.sh`: Reset databases and restart
   - `logs.sh`: Tail logs from all services
   - `health-check.sh`: Check health of all services
   - `test.sh`: Run integration tests

5. **Create Integration Documentation**
   Create `workspace/code/integration/README.md`:
   - System architecture overview
   - Prerequisites (Docker, Docker Compose versions)
   - Quick start guide
   - Service URLs and ports table
   - Troubleshooting guide
   - Development workflow tips

#### For UPDATE Integration (mode=update):

1. **Analyze Changes**
   - Compare current services with docker-compose.yml
   - Identify new services to add
   - Identify removed services to delete
   - Check for configuration changes

2. **Update Configuration**
   - Update docker-compose.yml with changes
   - Update .env.example with new variables
   - Update scripts if needed
   - Update documentation

3. **Verify Compatibility**
   - Ensure no port conflicts
   - Check dependency changes
   - Validate environment variables

#### For REVIEW Integration (mode=review):

1. **Present Current Configuration**
   - Show current service orchestration
   - Display environment setup
   - Review networking configuration

2. **Gather Feedback**
   - Ask about desired changes
   - Discuss alternative approaches
   - Update preferences based on decisions

### Step 4: Integration Testing Setup

Create integration test framework:

1. **Health Check Verification**
   Create script to verify all services are healthy:
   ```bash
   # Check each service's health endpoint
   # Wait for services to be ready
   # Report status
   ```

2. **Inter-Service Communication Tests**
   Create basic tests to verify services can communicate:
   - Test internal API calls between services
   - Verify database connections
   - Check message queue connectivity

3. **Smoke Tests**
   Create simple end-to-end tests:
   - User registration flow
   - Basic CRUD operations
   - Critical business workflows

### Step 5: Configuration Templates

#### Docker Compose Structure
```yaml
networks:
  app-network:
    driver: bridge

volumes:
  postgres-data:
  redis-data:

services:
  # Database Services
  postgres:
    image: postgres:14
    environment:
      POSTGRES_DB: main_db
      POSTGRES_USER: dbuser
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres-data:/var/lib/postgresql/data
      - ./init-scripts/postgres:/docker-entrypoint-initdb.d
    networks:
      - app-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U dbuser"]
      interval: 10s
      timeout: 5s
      retries: 5

  # Application Services
  service-name:
    build: 
      context: ../service-name
      dockerfile: Dockerfile
    ports:
      - "${SERVICE_PORT:-3000}:3000"
    environment:
      DATABASE_URL: postgresql://dbuser:${DB_PASSWORD}@postgres:5432/main_db
      OTHER_SERVICE_URL: http://other-service:3001
    depends_on:
      postgres:
        condition: service_healthy
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

### Step 6: Summary Report

After integration setup, provide a summary:
- Number of services integrated
- Database setup completed
- Network configuration
- Port allocations
- Startup order
- Location of integration files

## Important Considerations

### Service Dependencies
- Respect startup order from architecture
- Use health checks for proper sequencing
- Handle circular dependencies carefully

### Environment Management
- Use .env files for sensitive data
- Provide sensible defaults
- Document all required variables
- Support multiple environments (dev, test)

### Database Management
- Initialize databases on first run
- Support data persistence across restarts
- Provide reset scripts for development
- Handle migrations properly

### Networking
- Use custom network for isolation
- Enable service discovery by name
- Configure proper port mappings
- Handle external service connections

### Development Experience
- Fast startup times
- Easy debugging access
- Log aggregation
- Hot reload support where possible

## Quality Checklist

Before marking integration complete:
- [ ] All services included in docker-compose.yml
- [ ] Environment variables documented
- [ ] Database initialization scripts work
- [ ] Services start in correct order
- [ ] Health checks functioning
- [ ] Inter-service communication verified
- [ ] Utility scripts created and tested
- [ ] README documentation complete
- [ ] No port conflicts
- [ ] Volumes properly configured
- [ ] Network isolation working
- [ ] Can run system with single command

## Output Structure

```
workspace/code/integration/
├── docker-compose.yml          # Main orchestration file
├── docker-compose.override.yml # Local overrides (optional)
├── .env.example                # Environment template
├── .gitignore                  # Ignore .env and data
├── init-scripts/               # Database initialization
│   ├── postgres/
│   │   ├── 01-create-databases.sql
│   │   └── 02-create-users.sql
│   └── mongo/ (if needed)
├── scripts/                    # Utility scripts
│   ├── start.sh
│   ├── stop.sh
│   ├── reset.sh
│   ├── logs.sh
│   ├── health-check.sh
│   └── test.sh
├── tests/                      # Integration tests
│   ├── health-checks.sh
│   ├── api-tests.sh
│   └── smoke-tests.sh
└── README.md                   # Documentation
```

## Custom Roles

- Start with `roo-arch` custom mode for orchestration
- Create integration configuration files
- Generate utility scripts
- Document the setup process
- Ensure smooth developer experience