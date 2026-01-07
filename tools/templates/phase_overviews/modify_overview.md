# Modification Management Overview

## Purpose
Handles user modification requests after initial development, intelligently routing changes to the correct entry point in the development pipeline and managing the update cascade through affected phases.

## Key Concepts
- **Current State Directives**: Record WHAT the system should be NOW, not history
- **Intelligent Classification**: 11 levels from requirements to frontend/backend/integration changes
- **Cascade Management**: Updates flow through dependent phases automatically
- **Conflict Resolution**: New directives replace conflicting old ones
- **Modification vs Bug Fix**: Process changes vs code fixes

## Classification Levels
1. **Level 1 - Requirements**: Business features, rules, metrics
2. **Level 2 - Domain**: Entities, relationships, boundaries
3. **Level 3 - Stories**: User workflows, permissions, journeys
4. **Level 4 - Architecture**: Service boundaries, communication
5. **Level 5 - API**: Endpoints, contracts, authentication, API security
6. **Level 6 - Service**: Internal design, technology stack
7. **Level 7 - Backend Development**: Code-only changes, refactoring, backend security fixes
8. **Level 8 - Frontend Architecture**: Framework changes, state management
9. **Level 9 - UI Specifications**: Component design, layouts, UX patterns
10. **Level 10 - Frontend Development**: Frontend code, frontend security fixes (XSS, file access)
11. **Level 11 - Integration**: Docker configuration, environment setup, security configuration

## Process Flow
1. Analyze modification request
2. Read all context and preferences
3. Classify modification level
4. Record directive in appropriate preferences.md
5. Return classification to start.md
6. start.md orchestrates update cascade
7. Each affected phase runs in update mode
8. Verification ensures consistency

## Critical Features
- Smart routing based on change type
- State-based directive recording
- Automatic cascade determination
- Conflict detection and resolution
- Clear separation from bug fixes
- Consumer-driven approach
- Impact assessment

## Files Involved
- **Router**: `prompts/modify/router.md` - Main classification logic
- **Guidelines**: `prompts/modify/guideline.md` - Principles and patterns
- **Examples**: `prompts/modify/examples.md` - Concrete scenarios
- **Verification**: `prompts/modify/verify.md` - Consistency checking
- **Preferences**: Updated in relevant phase directories

## Directive Format
```markdown
### Directive N: [Title]
**Type**: Modification
**Current State**: [What system should be NOW]
**Context**: [Why requested]
**Impact**: [Affected components]
**Date**: [YYYY-MM-DD]
```

## Common Modification Scenarios
- Adding new features (Level 1)
- Changing business rules (Level 1)
- New entities or relationships (Level 2)
- User permission changes (Level 3)
- Service splits/merges (Level 4)
- API endpoint changes (Level 5)
- Technology stack changes (Level 6)
- Backend performance optimizations (Level 7)
- Frontend framework changes (Level 8)
- UI/UX improvements (Level 9)
- Frontend security fixes (Level 10)
- Configuration security (Level 11)

## Important Guidelines
- Always record current state, not changes
- Replace conflicting directives entirely
- Start at highest applicable level
- Let changes cascade naturally
- Document all impacts
- Validate before applying
- Handle errors gracefully
- **Security issues classified by WHERE fix happens, not urgency**
- **ALL modifications route through Router first, no exceptions**

## Quality Checklist
- Modification correctly classified
- Directive clearly states current state
- Conflicts properly resolved
- Cascade path complete
- All preferences updated
- System remains consistent
- User expectations met