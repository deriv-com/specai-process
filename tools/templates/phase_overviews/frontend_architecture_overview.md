# Frontend Architecture Phase Overview

## Purpose
Designs the frontend application architecture based on API specifications and user stories, defining the technology stack, component architecture, state management strategy, and integration patterns that will guide frontend implementation.

## Key Concepts
- **Complexity-Based Framework Selection**: Framework choice based on PRD complexity score
  - 0-3: Vanilla HTML/CSS/JS or lightweight frameworks
  - 4-7: React/Vue SPA with component architecture
  - 8-10: Next.js/Nuxt with SSR, micro-frontends
- **API-First Design**: Frontend architecture driven by API contracts
- **Component Architecture**: Reusable UI component strategy
- **State Management**: Data flow and state handling patterns
- **Responsive Design**: Multi-device support strategy

## Process Flow
1. Read API specifications to understand available endpoints
2. Read user stories to identify UI requirements
3. Check PRD complexity score for framework guidance
4. Design component architecture and hierarchy
5. Define state management approach
6. Establish routing and navigation patterns
7. Design authentication and authorization flows
8. Create integration patterns with backend APIs
9. Run verification for completeness

## Critical Features
- Framework selection based on complexity
- Component hierarchy visualization
- State management architecture
- Routing structure definition
- API client SDK generation approach
- Authentication flow design
- Build and deployment configuration
- Performance optimization strategy

## Files Involved
- **Input**: `workspace/output/services/*/api/*_public.md`, `workspace/output/stories/stories.md`, `workspace/output/requirements/prd.md`
- **Guidelines**: `prompts/frontend/guideline.md`
- **Output**: `workspace/output/frontend/architecture.md`, `workspace/output/frontend/preferences.md`
- **Verification**: Creates `workspace/cache/verify_frontend_architecture.md`

## Key Deliverables
- Executive summary of frontend approach
- Technology stack with justification
- Component architecture diagram
- State management strategy
- Routing architecture
- Authentication/authorization flows
- API integration patterns
- Build configuration approach
- Performance requirements
- Responsive design strategy
- Development guidelines

## Common Modifications at This Level
- Framework changes
- State management library switches
- Component structure reorganization
- Routing strategy changes
- Authentication method updates
- Build tool modifications

## Important Guidelines
- Match complexity to appropriate framework
- Design for reusability and maintainability
- Follow API contracts from specifications
- Consider performance from the start
- Plan for responsive design
- Include accessibility requirements
- Document deployment requirements
- Design for testability

## Quality Checklist
- Framework appropriate for complexity
- Component architecture well-structured
- State management clearly defined
- API integration patterns established
- Authentication flows documented
- Routing structure logical
- Performance strategy defined
- Responsive design planned
- Build configuration specified
- Testing approach documented