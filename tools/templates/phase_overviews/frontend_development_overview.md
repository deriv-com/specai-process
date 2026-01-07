# Frontend Development Phase Overview

## Purpose
Implements the complete frontend application based on frontend architecture and UI specifications, translating designs into working code that integrates with backend APIs, follows development standards, and provides an excellent user experience.

## Key Concepts
- **Complexity-Based Implementation**: Code structure matches PRD complexity score
  - 0-3: Simple, minimal file structure
  - 4-7: Component-based organization
  - 8-10: Full modular architecture with advanced patterns
- **API Integration**: Consuming backend services through generated SDKs
- **Component Implementation**: Building reusable UI components
- **State Management**: Implementing data flow patterns
- **Testing Coverage**: Unit, integration, and E2E tests

## Process Flow
1. Read frontend architecture for technology decisions
2. Read UI specifications for component requirements
3. Generate API client SDK from API specifications
4. Implement component library based on UI specs
5. Build screen layouts and navigation
6. Integrate with backend APIs
7. Implement state management
8. Add comprehensive tests
9. Self-review for quality
10. Run verification for correctness
11. UX and performance review

## Critical Features
- Orchestrated workflow with multiple review phases
- Mode detection (new/update/review)
- Complexity-appropriate implementation
- API SDK generation and integration
- Component library development
- Responsive implementation
- Authentication flow implementation
- Build configuration and optimization
- Testing strategy implementation

## Files Involved
- **Input**: `workspace/output/frontend/architecture.md`, `workspace/output/frontend/ui/`, API specs
- **Guidelines**: `prompts/frontend-dev/guideline.md`
- **Output**: `workspace/code/frontend/` (all implementation files)
- **Preferences**: `workspace/code/frontend/preferences.md`
- **Verification**: Creates `workspace/cache/verify_frontend_develop.md`
- **Review**: Creates `workspace/cache/review_frontend_develop.md`

## Development Workflow
1. Initial development (roo-pe mode)
2. Self-review phase (update mode)
3. Verification phase (roo-verify mode)
4. Issue resolution if needed
5. UX & performance review (roo-man mode)

## Key Deliverables
- Complete working frontend application
- API client SDK
- Component library implementation
- Screen implementations
- Navigation and routing
- State management implementation
- Authentication/authorization flows
- Comprehensive tests
- Build configuration
- Documentation (README)
- Environment configuration (.env.example)
- Deployment configuration

## Common Modifications at This Level
- Bug fixes in UI components
- API integration updates
- State management improvements
- Performance optimizations
- Accessibility enhancements
- Responsive design adjustments
- Test additions

## Important Guidelines
- Never start from scratch if code exists
- Read existing implementation first
- Follow framework best practices
- Implement ALL UI specifications
- Ensure API integration works
- Include comprehensive error handling
- Optimize for performance
- Document configuration options
- Follow accessibility standards

## Quality Checklist
- All UI specifications implemented
- API integration complete and working
- Authentication flows functional
- State management consistent
- Components reusable and tested
- Responsive design working
- Accessibility standards met
- Performance targets achieved
- Tests passing with coverage
- Build optimized for production
- Documentation complete
- Error handling comprehensive