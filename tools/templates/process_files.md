# Core Process Files Manifest

This document provides a quick reference to all process files in the AI-driven development platform. Each file is listed with a one-line description for rapid identification.

## How to Use This System

1. **Start Here**: This manifest gives you a complete list of all files (~75 lines)
2. **Get Context**: Read phase overview files in `tools/templates/phase_overviews/` for detailed context (~60-80 lines each)
3. **Deep Dive**: Read only the specific implementation files you need

This approach uses ~1,000 lines instead of 8,000+ lines when reading everything.

## Template Files
- templates/prd.md - Comprehensive PRD template for complex systems (8-10 complexity score)
- templates/prd_minimal.md - Simplified PRD template for simple applications (0-3 complexity score)
- templates/prd_standard.md - Standard PRD template for business applications (4-7 complexity score)
- templates/preferences.md - Template for tracking user decisions and directives as current state
- templates/workspace_preferences.md - Template for workspace-wide default preferences that persist across resets

## Main Orchestration
- prompts/start.md - Main workflow orchestrator that acts as triage/manager, routing and delegating requests without executing

## Requirements Phase
- prompts/requirements/prompt.md - Transforms product brief into structured PRD with complexity assessment
- prompts/requirements/verify.md - Verification checklist for PRD completeness and quality
- prompts/requirements/guideline.md - Standards and quality guidelines for requirements documentation

## Domain Modeling Phase
- prompts/domain/prompt.md - Creates conceptual domain model from PRD with entity relationships
- prompts/domain/guideline.md - Domain modeling standards, patterns, and best practices
- prompts/domain/verify.md - Domain model verification checklist for consistency

## User Stories Phase
- prompts/stories/prompt.md - Generates comprehensive user stories from requirements and domain
- prompts/stories/guideline.md - User story standards and coverage requirements
- prompts/stories/verify.md - User story verification for completeness and alignment

## Architecture Phase
- prompts/architecture/prompt.md - Translates domain boundaries into service architecture
- prompts/architecture/guideline.md - Service design principles and architecture standards
- prompts/architecture/verify.md - Architecture verification for boundaries and dependencies

## API Specifications Phase
- prompts/api/prompt.md - Orchestrates API specification workflow for all services
- prompts/api/guideline.md - API design standards for public and internal APIs
- prompts/api/verify.md - API specification verification for completeness
- prompts/api/api.md - Creates individual API specifications for services

## Frontend Architecture Phase
- prompts/frontend/prompt.md - Orchestrates frontend architecture workflow
- prompts/frontend/frontend.md - Designs frontend architecture based on APIs and user stories
- prompts/frontend/guideline.md - Frontend architecture standards and technology selection
- prompts/frontend/verify.md - Frontend architecture verification for completeness

## UI Specifications Phase
- prompts/ui/prompt.md - Orchestrates UI specification workflow
- prompts/ui/ui.md - Creates comprehensive UI component specifications
- prompts/ui/guideline.md - UI design standards and component patterns
- prompts/ui/verify.md - UI specification verification for completeness

## Service Specifications Phase
- prompts/services/prompt.md - Orchestrates service specification workflow
- prompts/services/guideline.md - Service design philosophy and implementation guidelines
- prompts/services/service.md - Creates detailed service specifications with modules
- prompts/services/verify.md - Service specification verification for implementation readiness

## Backend Development Phase
- prompts/develop/prompt.md - Orchestrates backend code implementation workflow
- prompts/develop/guideline.md - Backend development standards and best practices
- prompts/develop/develop.md - Implements backend code based on specifications
- prompts/develop/verify.md - Backend code verification for correctness and completeness
- prompts/develop/review.md - Architecture and security review of backend implementations

## Frontend Development Phase
- prompts/frontend-dev/prompt.md - Orchestrates frontend implementation workflow
- prompts/frontend-dev/develop.md - Implements frontend application based on architecture and UI specs
- prompts/frontend-dev/guideline.md - Frontend development standards and patterns
- prompts/frontend-dev/verify.md - Frontend implementation verification for completeness
- prompts/frontend-dev/review.md - UX and performance review of frontend implementation

## Integration Phase
- prompts/integration/prompt.md - Orchestrates Docker Compose integration setup
- prompts/integration/guideline.md - Integration best practices and patterns
- prompts/integration/compose.md - Generates Docker Compose configuration
- prompts/integration/verify.md - Integration setup verification

## Modification Management
- prompts/modify/router.md - Routes modification requests (including security) to appropriate entry points (Levels 1-11)
- prompts/modify/guideline.md - Modification principles and cascade management
- prompts/modify/verify.md - Modification verification for consistency
- prompts/modify/examples.md - Concrete examples of different modification types

## Evaluation & Configuration
- evals/4projects.md - Four-level evaluation suite for testing platform capabilities from junior to staff engineering skills
- evals/ai_engineer_levels.md - Detailed capability definitions for L1-L4 AI engineers
- .roomodes - Custom AI role configurations for different phases

## Tool Files
- tools/improve.md - Process improvement workflow with intelligent file discovery
- tools/visual.md - Visual documentation generation
- tools/present.md - Presentation and documentation creation
- tools/post.md - Blog post generation
- tools/preferences.md - Preference management tool for workspace/phase hierarchy

## Phase Overview Files
For detailed context about each phase, see `tools/templates/phase_overviews/`:
- requirements_overview.md - PRD creation from product briefs
- domain_overview.md - Domain modeling and data architecture
- stories_overview.md - User story generation
- architecture_overview.md - Service architecture design
- api_overview.md - API specification workflow
- frontend_architecture_overview.md - Frontend architecture design
- ui_overview.md - UI component specification
- services_overview.md - Service specification details
- develop_overview.md - Backend code implementation process
- frontend_development_overview.md - Frontend implementation process
- integration_overview.md - Docker Compose setup
- modify_overview.md - Modification routing and management
- ai_levels_overview.md - AI engineer capability levels (L1-L4) definition
- preferences_overview.md - Two-tier preference hierarchy for reducing repetition