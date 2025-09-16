# Integration Output Guidelines

## Integration Philosophy

The integration phase brings together all individually developed services into a cohesive, locally runnable system. This is not about production deployment, but rather creating a development and testing environment that accurately represents how services interact.

## Docker Compose Best Practices

### Service Configuration
- Use build contexts pointing to service directories
- Leverage multi-stage Dockerfiles for efficiency
- Configure restart policies appropriately
- Use proper health checks with sensible timeouts
- Define clear dependency chains

### Environment Management
- Never commit actual .env files
- Provide comprehensive .env.example
- Use environment variable interpolation
- Support override files for local development
- Document all required variables

### Networking
- Use custom bridge networks for isolation
- Enable service discovery by container name
- Map only necessary ports to host
- Consider using aliases for service communication
- Implement proper network segmentation

### Data Persistence
- Use named volumes for databases
- Mount source code for development hot-reload
- Separate data volumes from config volumes
- Implement backup strategies for development data
- Provide data reset mechanisms

## Integration Patterns by Complexity

### Simple Services (PRD Score 0-3)
**Integration Approach**: Minimal orchestration
- Single docker-compose.yml file
- Basic service definitions
- Simple environment variables
- SQLite or single shared database
- No complex dependencies

Example structure:
```yaml
services:
  app:
    build: ../converter
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: sqlite:///data/app.db
    volumes:
      - ./data:/data
```

### Standard Services (PRD Score 4-7)
**Integration Approach**: Moderate orchestration
- Separate database service
- Inter-service networking
- Environment-based configuration
- Health checks and dependencies
- Basic monitoring setup

Example structure:
```yaml
services:
  postgres:
    image: postgres:14
    # ... configuration
  
  app:
    build: ../app
    depends_on:
      postgres:
        condition: service_healthy
    # ... configuration
  
  worker:
    build: ../worker
    depends_on:
      - app
    # ... configuration
```

### Complex Services (PRD Score 8-10)
**Integration Approach**: Full orchestration
- Multiple database technologies
- Message queues and caching layers
- Service mesh considerations
- Observability stack (logs, metrics, traces)
- Complex initialization sequences
- Multiple network segments

Example structure:
```yaml
services:
  # Data Layer
  postgres:
    # ... configuration
  redis:
    # ... configuration
  kafka:
    # ... configuration
  
  # Core Services
  gateway:
    # ... configuration
  auth:
    # ... configuration
  
  # Supporting Services
  monitoring:
    # ... configuration
```

## Database Initialization

### PostgreSQL Setup
```sql
-- init-scripts/postgres/01-create-databases.sql
CREATE DATABASE main_db;
CREATE DATABASE test_db;

-- Create service-specific schemas
\c main_db;
CREATE SCHEMA IF NOT EXISTS accounts;
CREATE SCHEMA IF NOT EXISTS trading;
```

### Redis Configuration
```conf
# init-scripts/redis/redis.conf
maxmemory 256mb
maxmemory-policy allkeys-lru
save 900 1
save 300 10
```

## Utility Scripts

### Start Script Template
```bash
#!/bin/bash
# scripts/start.sh

echo "Starting application stack..."

# Check Docker is running
if ! docker info > /dev/null 2>&1; then
    echo "Docker is not running. Please start Docker first."
    exit 1
fi

# Create .env if it doesn't exist
if [ ! -f ../.env ]; then
    echo "Creating .env from .env.example..."
    cp .env.example .env
    echo "Please update .env with your configuration"
    exit 1
fi

# Start services
docker-compose up -d

# Wait for services to be healthy
echo "Waiting for services to be healthy..."
./health-check.sh

echo "Application stack is running!"
echo "Services available at:"
echo "  - Main App: http://localhost:3000"
echo "  - API Docs: http://localhost:3000/api/docs"
```

### Health Check Script Template
```bash
#!/bin/bash
# scripts/health-check.sh

SERVICES=("app:3000" "api:3001" "worker:3002")
MAX_ATTEMPTS=30

for service in "${SERVICES[@]}"; do
    IFS=':' read -r name port <<< "$service"
    echo -n "Checking $name... "
    
    attempts=0
    while [ $attempts -lt $MAX_ATTEMPTS ]; do
        if curl -f "http://localhost:$port/health" > /dev/null 2>&1; then
            echo "✓"
            break
        fi
        attempts=$((attempts + 1))
        sleep 2
    done
    
    if [ $attempts -eq $MAX_ATTEMPTS ]; then
        echo "✗ (timeout)"
        exit 1
    fi
done

echo "All services are healthy!"
```

## Testing Integration

### Smoke Test Example
```bash
#!/bin/bash
# tests/smoke-tests.sh

echo "Running smoke tests..."

# Test 1: API is accessible
curl -f http://localhost:3000/api/health || exit 1

# Test 2: Database connection works
docker-compose exec app npm run db:ping || exit 1

# Test 3: Inter-service communication
curl -X POST http://localhost:3000/api/test-integration || exit 1

echo "Smoke tests passed!"
```

## Documentation Standards

### README Structure
```markdown
# [Project Name] - Local Development Environment

## Prerequisites
- Docker 20.10+
- Docker Compose 2.0+
- 8GB RAM minimum
- 10GB free disk space

## Quick Start
1. Clone the repository
2. Navigate to `workspace/code/integration`
3. Copy `.env.example` to `.env` and configure
4. Run `./scripts/start.sh`
5. Access the application at http://localhost:3000

## Architecture
[Include diagram of service relationships]

## Services
| Service | Port | Description | Health Check |
|---------|------|-------------|--------------|
| app | 3000 | Main application | /health |
| api | 3001 | REST API | /health |

## Development Workflow
### Starting Services
```bash
./scripts/start.sh
```

### Viewing Logs
```bash
./scripts/logs.sh [service-name]
```

### Resetting Data
```bash
./scripts/reset.sh
```

## Troubleshooting
### Service won't start
- Check port conflicts: `docker ps`
- Check logs: `docker-compose logs [service]`
- Verify environment variables

### Database connection issues
- Ensure database is healthy: `docker-compose ps`
- Check connection string in .env
- Verify network connectivity
```

## Quality Checklist

### Essential Requirements
- [ ] All services defined in docker-compose.yml
- [ ] Health checks implemented and working
- [ ] Dependencies correctly ordered
- [ ] Environment variables documented
- [ ] Volumes for data persistence
- [ ] Network configuration correct
- [ ] Ports properly mapped
- [ ] Scripts executable and tested

### Development Experience
- [ ] Single command startup
- [ ] Fast service startup
- [ ] Easy log access
- [ ] Simple debugging setup
- [ ] Hot reload where applicable
- [ ] Clear error messages
- [ ] Graceful shutdown

### Documentation
- [ ] Prerequisites listed
- [ ] Quick start guide works
- [ ] Architecture documented
- [ ] Troubleshooting section helpful
- [ ] Service URLs listed
- [ ] Environment variables explained

## Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| Port already in use | Another service using port | Change port in .env or stop other service |
| Service depends_on not working | Health check not properly configured | Implement proper health check endpoint |
| Database not initialized | Init scripts not running | Check init script permissions and syntax |
| Services can't communicate | Network configuration issue | Ensure services on same network |
| Environment variables not set | Missing .env file | Copy .env.example and configure |
| Slow startup | Large build context | Use .dockerignore to exclude unnecessary files |
| Out of memory | Insufficient Docker resources | Increase Docker memory allocation |

## Integration Testing Strategy

### Levels of Testing
1. **Health Checks**: Service is running and responsive
2. **Connectivity Tests**: Services can reach each other
3. **API Tests**: Endpoints return expected responses
4. **Integration Tests**: End-to-end workflows function
5. **Performance Tests**: System handles expected load

### Test Automation
- Run tests in CI/CD pipeline
- Use docker-compose for test environment
- Implement test data fixtures
- Clean up after test runs
- Report test results clearly