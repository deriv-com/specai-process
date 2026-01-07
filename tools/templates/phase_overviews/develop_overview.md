# Development Phase Overview

## Purpose
Implements complete services based on their specifications, translating service.md specifications into working code that meets all requirements, follows development standards, and is production-ready.

## Key Concepts
- **Complexity-Based Implementation**: Code structure matches PRD complexity score
  - 0-3: Simple, single file or minimal files
  - 4-7: Light separation into logical components
  - 8-10: Full modular architecture
- **Comprehensive Implementation**: ALL functionality from service.md
- **Standards Compliance**: Language-specific best practices
- **Integration Readiness**: Dockerfile, health checks, environment config

## Process Flow
1. Read service specification for complete requirements
2. Check PRD complexity score for structure guidance
3. Implement all modules/components as specified
4. Create comprehensive tests (unit and integration)
5. Implement security measures
6. Add Docker support for integration
7. Self-review for quality
8. Run verification for correctness
9. Architecture and security review (roo-man mode)

## Critical Features
- Orchestrated workflow with multiple review phases
- Mode detection (new/update/review)
- Complexity-appropriate implementation
- Comprehensive testing
- Docker containerization
- Health check endpoints
- Environment configuration (.env.example)
- Database migrations support

## Files Involved
- **Input**: `workspace/output/services/{service}/service.md`, API specs from `workspace/output/api/`
- **Guidelines**: `prompts/develop/guideline.md`
- **Output**: `workspace/code/{service}/` (all implementation files)
- **Preferences**: `workspace/code/preferences.md` (single file for all service implementations)
- **Verification**: Creates `workspace/cache/verify_develop_{service}.md`
- **Review**: Creates `workspace/cache/review_develop_{service}.md`

## Development Workflow
1. Initial development (roo-pe mode)
2. Self-review phase (update mode)
3. Verification phase (roo-verify mode)
4. Issue resolution if needed
5. Architecture & security review (roo-man mode)

## Key Deliverables
- Complete working code
- Comprehensive tests
- Dockerfile for containerization
- Health check endpoint (/health)
- Environment configuration (.env.example)
- Database migrations (if applicable)
- README with setup instructions
- All API endpoints implemented
- Error handling and logging

## Common Modifications at This Level
- Bug fixes (not handled by modification router)
- Code refactoring
- Performance improvements
- Better error handling
- Improved logging
- Test additions

## Important Guidelines
- Never start from scratch if code exists
- Read existing implementation first
- Preserve working code during updates
- Follow language-specific standards
- Implement ALL specifications
- Include integration requirements
- Document configuration options

## Quality Checklist
- All functionality implemented
- API endpoints match specs
- Comprehensive error handling
- Tests passing with coverage
- Code follows standards
- Documentation complete
- Security implemented
- Performance adequate
- Docker ready
- Health checks working