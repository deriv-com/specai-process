# Service Specifications Output Guidelines

## Service Definition
A service is a complete deployable unit that implements a bounded context from the domain model. Each service contains an internal structure optimized for its specific requirements and complexity.

## Service Design Philosophy

### Internal Structure Flexibility
The internal structure of each service should be designed based on:
- **Service complexity**: Simple services may need minimal structure, complex ones may need multiple modules
- **Business requirements**: Let the functional needs drive the design
- **Technology best practices**: Follow the chosen tech stack's conventions
- **Team preferences**: Respect existing patterns and developer familiarity
- **Architecture guidance**: Follow the Internal Structure specified in the service architecture

### Structure Guidelines by Complexity

**Simple Services (PRD Score 0-3)**:
- Single main file or very few files
- Direct implementation without layers
- Minimal abstraction
- All code in one place for easy understanding
- Example: A PDF converter might have just `main.py` and `config.py`

**Standard Services (PRD Score 4-7)**:
- Light separation into logical components
- Some abstraction for maintainability
- Organized by concern (routes, logic, data)
- Example: A task manager might have API routes, business logic, and data access separated

**Complex Services (PRD Score 8-10)**:
- Full modular architecture
- Clear module boundaries
- Well-defined interfaces
- Comprehensive separation of concerns
- Example: A trading platform with distinct modules for orders, risk, matching, etc.

### Common Patterns (Not Prescriptive)
Services often include some combination of:
- API handling (public and/or internal)
- Business logic implementation
- Data persistence
- Background processing
- Integration with other services

However, the specific organization and naming should be determined by what makes sense for each service and its complexity level.

## Document Structure

### Service Specification (`service.md`)

The service.md file is the comprehensive specification for the entire service.

#### Overview
Brief summary of service purpose and domain alignment (2-3 lines max)

#### Tech Stack
List the programming languages, frameworks, databases, and infrastructure choices for this service. Explain **why** each choice is appropriate for this service's specific needs.

#### User Story Coverage
List of user story IDs this service helps fulfill (reference only, not for direct implementation)

#### Architecture Design
Explain the chosen internal architecture for this service:
- Why this structure was selected
- How different concerns are separated
- Module/component organization rationale
- Data flow and dependencies

#### Directory Structure
Complete file tree showing the service's structure as designed by the architect.
The structure should reflect the chosen architecture and tech stack conventions.

**Examples by Complexity:**

Simple Service (Score 0-3):
```
converter/
├── main.py          # All application code
├── config.py        # Configuration
├── requirements.txt
├── Dockerfile
└── README.md
```

Standard Service (Score 4-7):
```
taskmanager/
├── src/
│   ├── __init__.py
│   ├── app.py           # Application setup
│   ├── routes.py        # API endpoints
│   ├── models.py        # Data models
│   ├── business.py      # Business logic
│   └── database.py      # Database operations
├── tests/
├── requirements.txt
└── README.md
```

Complex Service (Score 8-10):
```
trading/
├── src/
│   ├── api/            # API layer
│   ├── domain/         # Business domain
│   ├── persistence/    # Data layer
│   ├── integrations/   # External services
│   └── events/         # Event handling
├── tests/
├── migrations/
└── README.md
```

#### Module/Component Specifications
Document the service components based on the complexity:

**For Simple Services (Flat Structure):**
Document the main components within the single file(s):
- Main application logic
- Configuration handling
- API endpoints
- Database operations
- External integrations

Example:
```
### Main Application (main.py)
**Purpose**: Contains all service functionality in a single file
**Core Functionality**:
- Session management functions
- PDF upload handling
- Conversion orchestration
- Database queries
- API endpoint definitions
```

**For Standard/Complex Services (Modular Structure):**
For each major module or component within the service, include:
- **Purpose**: Clear description of responsibilities
- **File Ownership**: Which files belong to this module
- **Core Functionality**:
  - Key operations and flows
  - Data models used
  - API endpoints implemented (if applicable)
  - Dependencies on other modules
  - Business logic
  - Error handling
- **Interfaces**: What this module exposes to other parts of the service
- **Configuration**: Key parameters and settings

#### Data Architecture
Detail the service's data strategy:
- **Data Models**: Complete schemas for all entities
- **Persistence Strategy**: Database choice and design rationale
- **Data Access Patterns**: How data flows through the service
- **Data Integrity**: Constraints and validation rules
- **Migration Strategy**: Approach for schema evolution

#### Security Architecture
- **Authentication**: How the service authenticates requests
- **Authorization**: Access control within the service
- **Data Protection**: Encryption and security measures
- **API Security**: Rate limiting, validation, etc.

#### Performance & Scalability
- **Performance Requirements**: Latency, throughput targets
- **Scalability Strategy**: How the service scales
- **Caching Strategy**: Use of caching layers
- **Resource Management**: Database connections, memory, etc.

#### Error Handling & Resilience
- **Error Categories**: Types of errors and their handling
- **Retry Strategies**: For transient failures
- **Circuit Breakers**: For external dependencies
- **Monitoring Points**: What to monitor for health

#### External Dependencies
- **Services**: Other services this depends on
- **APIs**: External APIs consumed
- **Libraries**: Key third-party libraries

#### Deployment Requirements
**For Integration phase support:**
- **Environment Variables**: List all required environment variables with descriptions
  - Example: `DATABASE_URL` - PostgreSQL connection string
  - Example: `API_KEY` - External service authentication
  - Example: `PORT` - Service listening port (default: 3000)
- **Health Check Endpoint**: Specify the endpoint for service health verification
  - Path: `/health` or `/api/health`
  - Expected response: `{"status": "healthy"}`
- **Startup Dependencies**: Services that must be running before this service
  - Database requirements (PostgreSQL, MongoDB, Redis)
  - Other microservices this depends on
- **Database Initialization**: Requirements for database setup
  - Migration scripts location
  - Seed data requirements
  - Schema initialization approach
- **Container Configuration**: Docker-specific requirements
  - Base image preferences
  - Build arguments needed
  - Runtime configuration

#### Development Guidelines
- **Code Organization**: How code is structured within the chosen architecture
- **Testing Strategy**: Unit, integration, and end-to-end tests
  - Test cases must have unique IDs: `TC-[SERVICE]-[3CHAR]` where:
    - SERVICE: Two-letter code for the service (e.g., AC for Accounts, TR for Trading, MK for Market)
    - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
    - Examples: TC-AC-J6Q (accounts test case), TC-TR-W3F (trading test case)
- **Deployment Model**: Containerization, orchestration
- **Configuration Management**: Environment-specific settings

#### Implementation Order
Recommended order for implementing the service based on its architecture and dependencies.

## Design Principles (Not Rules)

### API Design
- Consider how external clients will interact with the service
- Design for consistency across the system
- Think about versioning and evolution

### Data Management
- Ensure clear data ownership
- Plan for data consistency requirements
- Consider performance implications

### Module Organization
- Group related functionality logically
- Minimize dependencies between modules
- Design for testability

## Quality Checklist

Before finalizing service specifications:
- [ ] Service purpose and boundaries are clear
- [ ] Tech stack is appropriate and justified
- [ ] Internal architecture is well-reasoned
- [ ] Directory structure reflects the design
- [ ] All major components are specified
- [ ] Data architecture is comprehensive
- [ ] Security measures are defined
- [ ] Performance requirements are addressed
- [ ] Error handling strategies are clear
- [ ] Development guidelines match the architecture
- [ ] External dependencies are documented
- [ ] Implementation order is logical
- [ ] **Deployment requirements are specified (env vars, health checks, dependencies)**

## Update Guidelines

When updating existing service specifications:
- Review the current architecture and understand its rationale
- Preserve working designs that meet requirements
- Document reasons for architectural changes
- Ensure changes align with overall system architecture
- Update all affected sections consistently

## ID Conventions

Use these ID formats throughout service specifications:
- **Test Cases**: `TC-[SERVICE]-[3CHAR]` (e.g., TC-TR-W3F)
- **Error Codes**: Service-specific format that makes sense for the architecture
- **Configuration Keys**: Follow the chosen tech stack's conventions

## Flexibility is Key

Remember: These guidelines provide structure, but each service should be designed to best meet its specific requirements. The architecture phase has the freedom to create the optimal design for each service based on:
- Domain complexity
- Performance requirements
- Team expertise
- Technology constraints
- Business priorities

The goal is to create services that are:
- Maintainable
- Scalable
- Testable
- Deployable
- Understandable

How you achieve these goals is a design decision, not a prescription.