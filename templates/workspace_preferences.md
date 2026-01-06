# Workspace Preferences

This file contains overarching preferences for this workspace that persist across project resets. These are your default technology choices that you don't want to repeat for every project.

## Setup Instructions (For AI/start.md)

When creating this file for the first time, ask the user these questions:

1. **Backend Language**: What's your preferred programming language? (e.g., Go, Python, Node.js, Java)
2. **Database**: What's your preferred database? (e.g., PostgreSQL, MySQL, MongoDB, SQLite)
3. **Web Framework**: What framework do you prefer for your chosen language? (e.g., Gin for Go, FastAPI for Python, Express for Node.js)
4. **Frontend Framework**: What's your preferred frontend framework? (e.g., React, Vue, Angular, or "vanilla" for plain HTML/JS)
5. **API Style**: Do you prefer REST or GraphQL?
6. **Testing Coverage**: What's your minimum test coverage target? (e.g., 80%, 90%, or "none")
7. **Any other preferences**: Anything else you'd like to set as defaults? (e.g., Docker, cloud provider, CI/CD tools)

Then fill in the sections below with their answers.

## Technology Stack Preferences

### Backend Development
**Preferred Language**: Go
**Rationale**: Modern, performant, excellent concurrency support, strong typing

**Preferred Web Framework**: 
- For APIs: Gin or Echo
- For GraphQL: gqlgen
**Rationale**: Lightweight, fast, idiomatic Go

### Database Preferences
**Preferred Relational Database**: PostgreSQL
**Rationale**: Robust, feature-rich, excellent JSON support, proven scalability

**Preferred NoSQL Database**: MongoDB
**Rationale**: Flexible schema, good for rapid prototyping

**Preferred Cache**: Redis
**Rationale**: Fast, versatile, supports pub/sub

**Preferred Message Queue**: RabbitMQ
**Rationale**: Reliable, feature-rich, good management tools

### Frontend Development
**Preferred Framework**: React
**Rationale**: Large ecosystem, strong community, flexible

**Preferred State Management**: Zustand (simple) / Redux Toolkit (complex)
**Rationale**: Zustand for simplicity, RTK for complex state

**Preferred UI Library**: Material-UI / Tailwind CSS
**Rationale**: MUI for rapid development, Tailwind for custom designs

**Preferred Build Tool**: Vite
**Rationale**: Fast, modern, excellent DX

### DevOps & Infrastructure
**Containerization**: Docker
**Orchestration**: Docker Compose (dev) / Kubernetes (production)
**CI/CD**: GitHub Actions
**Cloud Provider**: AWS (primary) / GCP (secondary)

## API Design Preferences

**API Style**: REST (default) / GraphQL (when appropriate)
**API Documentation**: OpenAPI 3.0 / Swagger
**Authentication**: JWT with refresh tokens
**Rate Limiting**: Token bucket algorithm
**Versioning Strategy**: URL path versioning (v1, v2)

## Security Preferences

**Password Hashing**: Argon2id
**Encryption**: AES-256-GCM
**TLS Version**: 1.3 minimum
**CORS Policy**: Strict, whitelist-based
**CSP Policy**: Strict with nonces

## Code Quality Preferences

**Testing Coverage Target**: 80% minimum
**Linting**: Language-specific strict rules
**Code Formatting**: Language-specific auto-formatters
**Documentation**: Inline comments + README + API docs
**Git Strategy**: Feature branches with PR reviews

## Architecture Preferences

**Service Architecture Style**:
- Simple (0-3 complexity): Monolith
- Standard (4-7 complexity): Modular monolith
- Complex (8-10 complexity): Microservices

**Data Architecture**:
- Single source of truth per domain
- Event sourcing for audit-critical data
- CQRS when read/write patterns differ significantly

**Communication Patterns**:
- Synchronous: REST/gRPC for request-response
- Asynchronous: Events/queues for decoupling

## Performance Preferences

**Response Time Target**: < 200ms p95
**Database Query Optimization**: Explain analyze all queries
**Caching Strategy**: Cache-aside pattern
**CDN Usage**: For all static assets

## Naming Conventions

**Services**: Single lowercase words (e.g., auth, trading, market)
**APIs**: RESTful resource naming (/users, /orders)
**Database**: snake_case for tables and columns
**Code**: Language-specific conventions

## Development Workflow Preferences

**PR Size**: < 400 lines of code changes
**Review Requirements**: At least 1 reviewer
**Deployment Strategy**: Blue-green deployments
**Feature Flags**: For gradual rollouts

---

## Usage Notes

These preferences serve as defaults for all projects in this workspace. They can be overridden at the phase level when needed (in `workspace/output/{phase}/preferences.md`).

The precedence order is: Phase > Workspace

## How to Use

1. **First Time**: Copy this template to `workspace/preferences.md` and customize
2. **Project Resets**: This file persists - only phase preferences are cleared
3. **New Projects**: These defaults apply automatically

Remember: These are defaults to reduce repetition, not rigid rules. Override at the phase level when needed.