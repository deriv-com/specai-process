# Architecture Phase Overview

## Purpose
Translates the Domain Model boundaries into concrete service architecture, defining service responsibilities, boundaries, and communication patterns that will guide all subsequent implementation phases.

## Key Concepts
- **Service Boundaries**: Map domain boundaries to microservice boundaries
- **Service Naming**: Single-word names reflecting domain (e.g., trading, accounts, market)
- **Data Ownership**: Each service owns its data with no shared databases
- **Communication Patterns**: Define sync/async inter-service communication
- **Complexity-Based Structure**: Services designed based on PRD complexity score
  - 0-3: Simple, flat structure
  - 4-7: Light modular organization
  - 8-10: Full modular architecture

## Process Flow
1. Read domain model, user stories, and PRD
2. Map domain boundaries to services
3. Define service responsibilities
4. Establish communication patterns
5. Design data ownership strategies
6. Create inter-service communication matrix
7. Generate requirements coverage matrix
8. Define development order based on dependencies
9. Run verification for completeness

## Critical Features
- Service ID generation (SVC-XX-XXX for docs, clean names for files)
- Architecture diagram with Mermaid.js
- Consumer-driven communication matrix
- Requirements and story coverage matrices
- Orchestration requirements for integration
- Internal structure guidance based on complexity
- Development order recommendations

## Files Involved
- **Input**: `workspace/output/domain/domain_model.md`, `workspace/output/stories/stories.md`, `workspace/output/requirements/prd.md`
- **Guidelines**: `prompts/architecture/guideline.md`
- **Output**: `workspace/output/architecture/architecture.md`, `workspace/output/architecture/preferences.md`
- **Verification**: Creates `workspace/cache/verify_architecture_architecture.md`

## Key Deliverables
- Executive summary of architecture approach
- Service definitions with boundaries and responsibilities
- Data strategy documentation
- Inter-service communication matrix
- Requirements coverage matrix
- User story coverage matrix
- Development order recommendations
- Orchestration requirements for each service

## Common Modifications at This Level
- Service splits or merges
- Changed service boundaries
- Modified communication patterns
- Different data distribution
- New service dependencies
- Scalability approach changes

## Important Guidelines
- Services must have clear, meaningful names
- Respect domain aggregate boundaries
- No shared databases between services
- Design for loose coupling
- Consider startup dependencies
- Document health check endpoints
- Include port allocations
- Plan for both public and internal APIs

## Quality Checklist
- All services have clear boundaries
- Service names meaningful and single-word
- Data ownership clearly defined
- No circular dependencies
- Communication patterns documented
- All requirements mapped to services
- All user stories covered
- Development order logical