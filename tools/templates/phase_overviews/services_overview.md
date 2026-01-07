# Service Specifications Phase Overview

## Purpose
Creates detailed specifications for complete services within the microservice architecture, comprehensive enough for AI or developers to implement all modules and functionality described in the service architecture.

## Key Concepts
- **Service Completeness**: Each service.md contains ALL specifications for the entire service
- **Complexity-Based Design**: Internal structure based on PRD complexity score
  - 0-3: Flat structure, single file implementation
  - 4-7: Light modular organization  
  - 8-10: Full modular architecture with clear boundaries
- **Module Documentation**: All modules documented within single service.md file
- **Technology Stack**: Language, framework, and database choices with rationale

## Process Flow
1. Read service architecture for boundaries and requirements
2. Check PRD complexity score for structure guidance
3. Design internal architecture appropriate to complexity
4. Define all modules/components within service
5. Document data architecture and persistence
6. Specify security and performance requirements
7. Define deployment requirements for integration
8. Run verification for implementation readiness

## Critical Features
- Orchestrated workflow for all services
- Mode-aware processing (new/update/review)
- Complexity-appropriate internal structure
- Complete module specifications
- Directory structure visualization
- Tech stack justification
- Deployment requirements for Docker/integration

## Files Involved
- **Input**: `workspace/output/architecture/architecture.md`, API specs if exist
- **Guidelines**: `prompts/services/guideline.md`
- **Output**: `workspace/output/services/{service}/service.md`
- **Preferences**: `workspace/output/services/preferences.md` (single file for all services)
- **Verification**: Creates `workspace/cache/verify_service_{service}.md`

## Key Deliverables
- Service overview and purpose
- Technology stack with justification
- Architecture design explanation
- Complete directory structure
- Module/component specifications
- Data architecture and models
- Security architecture
- Performance and scalability approach
- Error handling strategies
- External dependencies
- Deployment requirements (env vars, health checks, ports)
- Development guidelines

## Common Modifications at This Level
- Internal module reorganization
- Technology stack changes
- Design pattern changes
- Algorithm modifications
- Performance optimizations
- Database technology switches

## Important Guidelines
- Service.md is comprehensive specification for ENTIRE service
- Use clean service names for files (not IDs)
- Respect complexity score from PRD
- All modules documented in one file
- Include deployment requirements for integration
- Flexibility in design based on requirements
- Test case IDs follow TC-XX-XXX format

## Quality Checklist
- Service purpose clear
- Tech stack appropriate
- Internal architecture well-reasoned
- Directory structure complete
- All modules specified
- Data architecture comprehensive
- Security measures defined
- Performance requirements addressed
- Deployment requirements specified