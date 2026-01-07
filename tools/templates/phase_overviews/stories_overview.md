# User Stories Phase Overview

## Purpose
Transforms the Product Requirements Document and Domain Model into comprehensive user stories that capture all user interactions with the system, serving as the foundation for service architecture design.

## Key Concepts
- **User Type Identification**: Extract all distinct user types from PRD (end-users, administrators, system actors)
- **Story Format**: Standard "As a [user], I want to [action] so that [benefit]" format
- **Service Hints**: Add service hints in parentheses to guide service boundaries
- **Platform Boundaries**: Early indication of how stories group into services
- **Coverage Matrix**: Map stories back to PRD requirements for completeness

## Process Flow
1. Read PRD and domain model for context
2. Identify all user types and their characteristics
3. Create comprehensive stories for each user type
4. Ensure coverage of all PRD features
5. Align stories with domain model entities
6. Add service hints for architectural guidance
7. Create coverage matrix for traceability
8. Run verification for completeness

## Critical Features
- Comprehensive user type identification
- Atomic user stories (one need per story)
- Story IDs following US-XX-XXX format
- Service hint mapping for architecture guidance
- Cross-user interaction capture
- Coverage matrix generation
- Focus on WHAT users need, not HOW

## Files Involved
- **Input**: `workspace/output/requirements/prd.md`, `workspace/output/domain/domain_model.md`
- **Guidelines**: `prompts/stories/guideline.md`
- **Output**: `workspace/output/stories/stories.md`, `workspace/output/stories/preferences.md`
- **Verification**: Creates `workspace/cache/verify_stories_stories.md`

## Key Deliverables
- User types with descriptions and characteristics
- User stories organized by type
- Cross-user type stories for interactions
- Story coverage matrix
- Service distribution summary
- Platform hint assignments

## Common Modifications at This Level
- Adding new user workflows
- Changing user permissions
- Modifying user journeys
- Adding or removing user types
- Adjusting interaction patterns

## Important Guidelines
- Extract ALL user types including indirect users
- Keep stories concise and atomic
- Use consistent domain terminology
- Include edge cases and admin functions
- Cover full user journey
- Don't create implementation-specific stories
- Preserve story IDs during updates

## Quality Checklist
- All user types identified
- Each type has clear characteristics
- All PRD features have stories
- Stories follow standard format
- Story IDs unique and formatted
- Service hints logical
- Cross-user interactions captured
- Coverage matrix complete