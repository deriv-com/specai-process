# Service Architecture Output Guidelines

## Service Design Principles

### Service Naming Convention
- Service names must be single words (e.g., `trading`, `accounts`, `market`, `risk`)
- Choose names that clearly represent the service's primary domain
- Avoid generic names like `core`, `common`, or `shared`
- Names should directly reflect bounded contexts from the domain model

### Service Internal Structure
Each service should be designed with an internal structure that best fits its complexity and requirements. The complexity score from the PRD phase (0-10) should guide the architectural decisions:

#### Internal Structure Guidelines by Complexity Score

**Score 0-3: Simple Services (Prototype/Utility Level)**
- **Structure**: Flat, minimal file structure
- **Description**: Single file or very few files with direct implementation
- **Example**: "The service will have a simple, flat structure with core functionality in one or two files"
- **Characteristics**:
  - All endpoints in a single file
  - Direct database calls without abstraction layers
  - Direct external API integration
  - Minimal or no internal separation
  - Built for rapid development (1-2 days)

**Score 4-7: Standard Services (Business Application Level)**
- **Structure**: Light modular organization
- **Description**: Logical separation of concerns without over-engineering
- **Example**: "The service will be organized into a few logical components for API handling, business logic, and data access"
- **Characteristics**:
  - Separate files for routes, business logic, and data access
  - Simple repository pattern for data operations
  - Basic error handling and validation layers
  - Some reusable components
  - Built for maintainability (1-2 weeks)

**Score 8-10: Complex Services (Enterprise Level)**
- **Structure**: Full modular architecture
- **Description**: Well-defined modules with clear boundaries and interfaces
- **Example**: "The service will be organized into distinct modules: API layer, business domain layer, persistence layer, integration layer"
- **Characteristics**:
  - Clear module boundaries with defined interfaces
  - Comprehensive error handling and resilience patterns
  - Advanced patterns (CQRS, Event Sourcing if needed)
  - Extensive abstraction for flexibility
  - Built for scale and long-term evolution

#### Applying Complexity-Based Design
When documenting the **Internal Structure** section for a service:
1. Check the PRD complexity score
2. Use the appropriate structure template based on the score
3. Avoid suggesting "modules" for simple services - use terms like "components" or "functions"
4. Scale the description detail to match the complexity
5. Be explicit about the simplicity for low-complexity services

#### Example Internal Structure Descriptions

**For a Score 0-3 Service (PDF Converter):**
```
**Internal Structure**:
The service will have a simple, flat structure optimized for rapid development:
- Single main application file handling all REST endpoints
- Direct database queries using the PostgreSQL driver
- Direct integration with external APIs (OpenAI, Gemini)
- Basic configuration file for environment settings
- Minimal abstraction to keep the codebase small and understandable
```

**For a Score 4-7 Service (Task Manager):**
```
**Internal Structure**:
The service will be organized into a few logical components:
- **API Handler**: REST endpoint definitions and request validation
- **Business Logic**: Task management operations and workflow rules
- **Data Access**: Repository pattern for database operations
- **Authentication**: JWT token validation and user context
- **External Services**: Email notification integration
```

**For a Score 8-10 Service (Trading Platform):**
```
**Internal Structure**:
The service will be organized into distinct modules with clear boundaries:
- **API Module**: REST and WebSocket endpoint handlers with rate limiting
- **Domain Module**: Trading logic, order matching, risk calculations
- **Persistence Module**: Repository interfaces, database migrations, caching layers
- **Integration Module**: Market data feeds, payment gateways, regulatory reporting
- **Event Module**: Event sourcing, domain event publishing
- **Security Module**: Authentication, authorization, audit logging
```

### Service Boundaries
- Each service must have clear, well-defined boundaries based on domain boundaries
- Services should be loosely coupled with minimal dependencies
- Each service owns its data and persistence layer
- No shared databases between services
- Service boundaries must respect aggregate root boundaries from the domain model

### API Structure
- Each service may expose a **Public API** for external clients (when needed)
- Each service may expose an **Internal API** for other services (only if other services depend on this one)
- How these APIs are implemented internally is a design decision
- API design should follow consistent principles across the system

### Data Ownership
- Each service has exclusive ownership of its data domain
- Cross-service data access only through published APIs
- Each service implements its own persistence strategy
- Data models should align with domain aggregates
- No direct database access from outside the service

### API Exposure Patterns
Different architectural patterns are appropriate for different projects:
- **Direct Service APIs**: Services expose their own public APIs directly to clients
- **API Gateway Pattern**: A gateway service aggregates and routes requests to backend services
- **Backend for Frontend (BFF)**: Specialized backends for different client types
- **Orchestration Layer**: A service that coordinates complex workflows across multiple services
- Choose the pattern that best fits your project's requirements, team structure, and operational needs

### Common Architectural Considerations
When designing your service architecture, consider:
- **Service Cohesion**: Services should have a clear, focused purpose
- **Coupling**: Aim for loose coupling between services where appropriate
- **Data Ownership**: Clear ownership boundaries help maintain consistency
- **Business Logic Placement**: Consider where logic best fits based on your chosen pattern
- **Operational Complexity**: Balance architectural purity with operational simplicity

## Document Structure

### Executive Summary
Provide a concise overview of the service architecture approach, explaining the rationale for service boundaries and how they collectively fulfill the product requirements while respecting domain boundaries.

### Service Architecture Overview
- High-level view of all services and their relationships
- Include a **architecture diagram** using Mermaid.js showing services and their communication patterns
- Explain the overall architectural principles and patterns (microservices, event-driven, etc.)
- Describe the technology stack choices and rationale

### Service Definitions
For each service, provide these sections:
- **Service ID**: `SVC-[SERVICE]-[3CHAR]` (e.g., SVC-TR-K3M for trading service) - *For documentation traceability only*
- **Service Name**: Single-word identifier matching the domain (e.g., `trading`, `accounts`, `market`) - *Used for all file paths and directories*
- **Purpose**: Clear statement of the service's primary responsibility (2-3 sentences)
- **Domain Alignment**: Which bounded context(s) this service implements
- **Business Capabilities**: List of business functions this service provides
- **Data Domains**: Specific data entities owned and managed by this service (aligned with aggregates)
- **Public API**: Describe the PUBLIC API endpoints this service exposes directly to external clients
- **Internal API**: List the services offered to other services internally (only if needed)
- **Dependencies**: Other services this service depends on (with purpose)
- **Key Responsibilities**: Detailed list of what this service is responsible for
- **User Stories Coverage**: List of user story IDs from `stories.md` that this service addresses
- **Constraints**: Performance, scalability, or compliance requirements specific to this service
- **Requirements from Other Services**: For each service this depends on, list specific capabilities needed
- **Internal Structure**: High-level overview of how this service will be organized internally (must align with PRD complexity score - see Internal Structure Guidelines by Complexity Score)
- **Orchestration Requirements** (for Integration phase):
  - **Startup Dependencies**: Services that must be running before this service starts
  - **Health Check**: Endpoint or method to verify service is ready (e.g., `/health`)
  - **Environment Variables**: Key configuration variables needed
  - **Database Requirements**: Database type and initialization needs
  - **Port Allocation**: Default port number for the service

### Data Strategy
Explain the overall data ownership and management strategy:
- How data integrity is maintained across services
- Approach to eventual consistency
- Event sourcing or CQRS patterns (if applicable)
- Data replication or caching strategies
- Transaction boundaries and saga patterns
- How domain events are used for inter-service communication

### Inter-Service Communication Matrix
Create a detailed matrix showing what each service requires from other services. This consumer-driven approach ensures providers know exactly what consumers need. Format:
| Consumer Service | Provider Service | Required Capabilities | Communication Pattern | Purpose | Priority |
|------------------|------------------|----------------------|----------------------|---------|----------|
Example:
| trading | accounts | GetAccountBalance(accountId) | Sync REST API | Check available funds before trade | Critical |
| trading | risk | ValidateTradeRisk(tradeParams) | Sync REST API | Pre-trade risk validation | Critical |
| accounts | notifications | SendEmail(template, data) | Async Event | Account activity notifications | Medium |

### Requirements Coverage Matrix
Create a comprehensive matrix that maps ALL requirements from the PRD to the specific services that implement them. This critical verification step ensures complete coverage and helps identify any gaps. Format:
| PRD Section/Requirement | Primary Service | Supporting Services | Implementation Notes |
|-------------------------|-----------------|---------------------|---------------------|

### User Story Coverage Matrix
Create a matrix that maps ALL user stories to the services that implement them. This ensures every user need is addressed. Format:
| Story ID | User Story Summary | Primary Service | Supporting Services | API Exposure |
|----------|-------------------|-----------------|---------------------|--------------|

### Development Order Recommendation
Based on service dependencies and business priorities:
1. Foundation services (no dependencies)
2. Core business services
3. Integration services
4. User-facing services

## Service Architecture Requirements

### Ensure Sufficient Depth for Independent Implementation
All service definitions must include:
1. Clear boundaries and scope aligned with domain model
2. Data domains owned by the service (aggregate roots)
3. Public API offerings (if any)
4. Internal API offerings for other services
5. Dependencies on other services
6. Key responsibilities and business capabilities
7. Performance and scalability considerations
8. User stories addressed by this service
9. Technology choices and rationale
10. High-level approach to internal organization (without being prescriptive)

## Quality Checklist

Before finalizing service architecture:
- [ ] All services have clear, meaningful names reflecting their domain
- [ ] Service boundaries are well-defined and justified
- [ ] Data ownership strategy is clearly documented
- [ ] Database strategy (shared vs separate) is appropriate for the project
- [ ] API structure is consistent with chosen architectural pattern
- [ ] All PRD requirements are mapped to services
- [ ] All user stories are covered by services
- [ ] Inter-service dependencies are documented
- [ ] Consumer-driven requirements are captured
- [ ] Architecture diagram accurately represents relationships
- [ ] Chosen patterns are appropriate for project requirements
- [ ] Data strategy addresses consistency and transactions
- [ ] Development order considers dependencies
- [ ] Service internal structure approach is clear but not overly prescriptive
- [ ] **Service internal structures align with PRD complexity scores (0-3: flat, 4-7: light modules, 8-10: full modules)**
- [ ] All services have unique IDs following the standard format
- [ ] **Orchestration requirements are documented (startup order, health checks, ports)**

## ID Conventions vs File System Usage

### Service IDs (For Documentation Traceability Only)
Use these ID formats throughout service architecture specifications **for cross-referencing and traceability**:
- **Services**: `SVC-[SERVICE]-[3CHAR]` (e.g., SVC-TR-K3M for trading service)
- **Architecture Components**: `ARC-[SERVICE]-[3CHAR]` (e.g., ARC-MK-P7R for market architecture component)
- **Communication Patterns**: `COM-[SERVICE]-[3CHAR]` (e.g., COM-AC-L8K for accounts communication pattern)

Where:
- `[SERVICE]`: Two-letter code for the service (AC=Accounts, TR=Trading, MK=Market, etc.)
- `[3CHAR]`: Three random alphanumeric characters

### Service Names (For File System and Task Parameters)
**ALWAYS use clean service names for**:
- Directory structures: `workspace/output/services/trading/` (NOT `workspace/output/services/SVC-TR-K3M/`)
- File names: `trading_public.md` (NOT `SVC-TR-K3M_public.md`)
- Task parameters: `service=trading` (NOT `service=SVC-TR-K3M`)
- API specifications: `trading/api/trading_public.md`
- Verification reports: `trading/trading_verify.md`

### Usage Rules
- **Service IDs**: Use ONLY in documentation sections for traceability and cross-references
- **Service Names**: Use for ALL file paths, directory names, and task parameters
- Keep Service IDs separate from the practical file system structure

## Update Guidelines

When updating existing service architecture:
- Perform comprehensive gap analysis against current requirements
- Identify what needs to be added, modified, or removed
- Preserve valuable existing content that remains accurate
- Document changes in a changelog section
- Ensure backward compatibility where possible
- Clearly document any breaking changes
- Validate alignment with updated domain model