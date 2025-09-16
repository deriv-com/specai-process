# Development Output Guidelines

## Development Standards

### Code Quality Principles
- Write clean, maintainable, and well-documented code
- Follow SOLID principles and design patterns appropriate to the chosen language
- Ensure proper error handling and input validation
- Implement comprehensive logging for debugging and monitoring
- Write self-documenting code with clear variable and function names

### Complexity-Based Implementation

#### Simple Services (PRD Score 0-3)
- Implement as single file or minimal files
- Direct implementation without layers
- All functionality in one place
- Focus on getting it working quickly
- Example: A converter service might have just main file and config

#### Standard Services (PRD Score 4-7)
- Light separation into logical components
- Basic abstraction for maintainability
- Organized by concern (routes, logic, data)
- Use simple patterns like repository for data access
- Example: Separate API routes, business logic, and database operations

#### Complex Services (PRD Score 8-10)
- Full modular architecture as specified
- Clear module boundaries with interfaces
- Comprehensive separation of concerns
- Advanced patterns where beneficial
- Example: Distinct modules for each major capability

### Testing Requirements

#### Unit Tests
- Test individual functions and methods
- Mock external dependencies
- Cover happy path and error scenarios
- Aim for high coverage of business logic

#### Integration Tests
- Test API endpoints end-to-end
- Verify database operations
- Test external service integrations
- Validate error responses

#### Test Organization
- Place tests adjacent to code being tested
- Use descriptive test names
- Include test data and fixtures
- Document complex test scenarios

### API Implementation Standards

#### RESTful APIs
- Use proper HTTP methods and status codes
- Implement consistent error response format
- Follow resource-oriented design
- Include proper content negotiation

#### Internal Service Communication
- Use defined internal APIs from specifications
- Implement proper retry and timeout logic
- Handle service unavailability gracefully
- Log all inter-service calls for debugging

### Security Implementation

#### Input Validation
- Validate all inputs at entry points
- Sanitize data before processing
- Use parameterized queries for databases
- Implement rate limiting where specified

#### Authentication & Authorization
- Implement auth as specified in API specs
- Secure sensitive data in transit and at rest
- Follow principle of least privilege
- Audit security-relevant operations

### Performance Considerations

#### Optimization Guidelines
- Optimize for readability first, performance second
- Profile before optimizing
- Use caching where specified
- Implement pagination for large datasets
- Consider async processing for long operations

#### Resource Management
- Properly close connections and resources
- Implement connection pooling
- Monitor memory usage
- Handle graceful shutdowns

### Documentation Requirements

#### Code Documentation
- Document complex algorithms and business logic
- Include examples for public APIs
- Explain non-obvious design decisions
- Keep documentation up-to-date with code

#### API Documentation
- Document all endpoints with examples
- Include error responses
- Specify rate limits and constraints
- Provide authentication details

### Development Workflow

#### File Organization
- Follow language-specific conventions
- Group related functionality
- Separate concerns appropriately
- Keep files focused and manageable

#### Configuration Management
- Externalize configuration
- Use environment variables
- Provide sensible defaults
- Document all configuration options

### Language-Specific Guidelines

#### Go Services
- Follow standard Go project layout
- Use Go modules for dependencies
- Run `go fmt` and `go vet`
- Handle errors explicitly

#### Python Services
- Follow PEP 8 style guide
- Use type hints where beneficial
- Create virtual environments
- Use appropriate frameworks (FastAPI, Flask)

#### Node.js Services
- Use ES6+ features
- Implement proper async/await
- Handle promises correctly
- Use appropriate frameworks (Express, Fastify)

### Integration Readiness

#### Containerization
- **Dockerfile**: Create a Dockerfile for each service
  - Use appropriate base image for the tech stack (Node, Python, Go, Java, etc.)
  - Consider multi-stage builds for smaller production images
  - Include all runtime dependencies
  - Set proper working directory
  - Configure the service port with EXPOSE
  - Define health check command appropriate to the service
  - Key elements to include:
    - Base image selection matching the service's tech stack
    - Dependency installation (npm, pip, go mod, maven, etc.)
    - Application build steps if needed
    - Proper file copying and permissions
    - Environment variable support
    - Health check configuration
    - Appropriate startup command

#### Health Check Endpoint
- **Implementation**: Create `/health` or `/api/health` endpoint
  - Return 200 OK when service is ready
  - Check database connectivity if applicable
  - Verify critical dependencies are available
  - Response format: `{"status": "healthy", "timestamp": "..."}`

#### Environment Configuration
- **Documentation**: Create `.env.example` file with all variables
  - Include descriptions for each variable
  - Provide sensible defaults where appropriate
  - Mark required vs optional variables
  - Example:
    ```env
    # Required
    DATABASE_URL=postgresql://user:pass@localhost:5432/dbname
    API_KEY=your-api-key-here
    
    # Optional (defaults shown)
    PORT=3000
    LOG_LEVEL=info
    ```

#### Database Readiness
- **Migration Scripts**: Place in standard location
  - Use `migrations/` or `db/migrations/` directory
  - Number or timestamp migrations for ordering
  - Include both up and down migrations
  - Provide seed data scripts if needed

#### Service Discovery
- **Configuration**: Support dynamic service URLs
  - Use environment variables for other service URLs
  - Example: `ACCOUNTS_SERVICE_URL=http://accounts:3000`
  - Support both local and containerized environments

### Quality Checklist

Before marking development complete:
- [ ] All functionality from service.md implemented
- [ ] All API endpoints match specifications
- [ ] Comprehensive error handling in place
- [ ] Tests passing with good coverage
- [ ] Code follows language standards
- [ ] Documentation complete
- [ ] Security measures implemented
- [ ] Performance requirements met
- [ ] Configuration externalized
- [ ] Logs provide debugging capability
- [ ] **Dockerfile created and tested**
- [ ] **Health check endpoint implemented**
- [ ] **Environment variables documented in .env.example**
- [ ] **Database migrations in standard location**
- [ ] **Service URLs configurable via environment**
