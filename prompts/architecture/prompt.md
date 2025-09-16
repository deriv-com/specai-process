## Goal

We are about to transform the **Domain Model** (found in `workspace/output/domain/domain_model.md`), **Product Requirements Document** (found in `workspace/output/requirements/prd.md`), and **User Stories** (found in `workspace/output/stories/stories.md`) into a comprehensive Service Architecture document. Your role in this stage is to act as our **service architect**, responsible for translating domain boundaries into concrete service boundaries, defining service responsibilities, and establishing communication patterns between services.

## Operational Modes

This process operates in one of three modes:

### 1. **`New` Mode** (Default when no architecture exists)
- Everything is blank, no existing architecture or preferences
- Comprehensive service design required
- Build initial architecture from scratch

### 2. **`Update` Mode** (When architecture exists but changes are needed)
- Existing architecture and preferences are present
- Compare current architecture with requirements and domain model
- Only ask questions if changes are needed
- Communicate proposed changes before applying them
- Preserve existing work that aligns with current requirements

### 3. **`Review` Mode** (When explicitly requested)
- Architecture and preferences exist
- Primary goal is to engage user with their current architectural decisions
- Help user understand consequences of modifications
- Update both preferences and architecture based on user decisions
- No automatic changes without user approval

## Mode Detection
- Check if `workspace/output/architecture/architecture.md` exists
- Check if `workspace/output/architecture/preferences.md` exists
- If neither exists → **New Mode**
- If both exist and no explicit mode specified → **Update Mode**
- If user requests preference review → **Review Mode**

## Preparation
- You MUST READ `workspace/output/domain/domain_model.md`. This file contains the domain model with business entities, relationships, and domain boundaries.
- You MUST READ `workspace/output/stories/stories.md`. This file contains user stories that capture all user interactions with the system.
- You MUST READ `workspace/output/requirements/prd.md`. This file contains the comprehensive product requirements document.
- **CRITICAL: Check `workspace/output/requirements/preferences.md` for the PRD complexity score** - This score (0-10) determines the appropriate internal structure for services

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: Service architecture style, communication patterns, naming conventions
   - Persists across project resets within the workspace
2. **Phase Preferences** (`workspace/output/architecture/preferences.md`):
   - Always check: Contains architecture-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making architectural decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.

### ADDITIONAL PREPARATION
- You MUST READ `prompts/architecture/guideline.md` to learn about the output standards and document structure requirements for service architecture.
- You MUST READ `templates/preferences.md`. This template defines the structure for preferences documentation.
- **Check for Existing Documents**:
  - Check if **`workspace/output/architecture/architecture.md`** already exists:
    - If it **exists**: Read the existing file and evaluate whether it:
      - Fully covers all requirements from the PRD
      - Addresses all user stories from `stories.md`
      - Aligns with the domain model boundaries
      - Contains any outdated or incorrect information
    - If it **doesn't exist**: Proceed with creating new comprehensive service architecture
  - Check if **`workspace/output/architecture/preferences.md`** already exists:
    - If it **exists**: Read it to understand user directives specific to service architecture
    - If it **doesn't exist**: Create it to track user input for this step
- Your goal is to produce or update:
  - **`workspace/output/architecture/architecture.md`** - The comprehensive service architecture
  - **`workspace/output/architecture/preferences.md`** - User directives specific to service architecture

---

## Output

Create or update **`workspace/output/architecture/architecture.md`** with comprehensive service architecture that serves as the foundation for all subsequent service development. Service boundaries should directly map to the domain boundaries identified in the domain model.

**For Updates**: When updating an existing document:
- Maintain the existing structure unless changes are necessary
- Preserve any custom sections that don't conflict with requirements
- Add a changelog section documenting changes

The document must include all sections defined in the guideline.md file, including:
- Executive Summary
- Service Architecture Overview
- Service Definitions (for each service)
- Data Strategy
- Inter-Service Communication Matrix
- Requirements Coverage Matrix
- User Story Coverage Matrix

## **Process Guidelines by Mode**

### New Mode Process

1. **Service Identification**
   - Map domain boundaries to services
   - Define service responsibilities
   - Establish communication patterns
   - Ask about unclear boundaries

2. **User Input Checkpoint** (New Mode Only - First Time)
   - After presenting initial service analysis
   - Ask: "Before I proceed with detailed architecture design and service definitions, is there anything specific about service boundaries, communication patterns, or technology choices you'd like to mention? Any particular architectural patterns or approaches you prefer?"
   - Document any additional input in preferences
   - This gives user a chance to provide architecture-specific guidance

3. **Architecture Design**
   - Check PRD complexity score from requirements preferences
   - Create comprehensive service definitions
   - **Apply complexity-based internal structure**:
     - Score 0-3: Describe flat, simple structure
     - Score 4-7: Describe light modular organization
     - Score 8-10: Describe full modular architecture
   - Design inter-service communication
   - Define data ownership strategies
   - Get feedback on critical decisions

4. **Coverage Validation**
   - Ensure all requirements are covered
   - Map all user stories to services
   - Verify no gaps exist
   - Document all decisions

### Update Mode Process

1. **Gap Analysis**
   - Compare existing architecture with current requirements
   - Check alignment with updated domain model
   - Identify new services or capabilities needed
   - Assess deprecated functionality

2. **Change Communication**
   - Only if changes needed:
     - Present architectural modifications
     - Explain impact on existing services
     - Get approval for structural changes
     - Ask about unclear requirements

3. **Architecture Update**
   - Apply approved changes
   - Preserve valid existing content
   - Update communication matrices
   - Document changes in changelog

### Review Mode Process

1. **Preference Presentation**
   - Load all architectural decisions
   - Organize by impact area:
     - Service boundaries
     - Communication patterns
     - Data strategies
     - Technology choices

2. **Interactive Review**
   - Walk through each service definition
   - Review communication patterns
   - Discuss data ownership strategies
   - Explore alternative architectures

3. **Update Application**
   - Update preferences per user decisions
   - Regenerate affected architecture sections
   - Adjust service boundaries as needed
   - Document all changes with rationale

## Questions to Ask (Mode-Specific)

### New Mode Questions
Before asking, check the preference hierarchy for existing answers:
- Service boundary clarifications (check workspace preferences)
- Communication pattern preferences (check workspace preferences)
- Data consistency requirements (check workspace preferences)
- Technology stack preferences (check workspace preferences)
- Scalability priorities (check workspace preferences)

Only ask if not already specified in preferences or if architecture-specific override is needed.

### Update Mode Questions
- Approval for service additions/modifications
- Confirmation of boundary changes
- Validation of new communication patterns
- Impact assessment acknowledgment

### Review Mode Questions
- Satisfaction with service boundaries
- Desire to adjust communication patterns
- Interest in alternative architectures
- Technology choice reconsiderations

## Preferences Document

Create or update **`workspace/output/architecture/preferences.md`** following the preferences template at `templates/preferences.md`. 

For this step, focus on these decision categories:
- Service Boundaries
- Communication Patterns
- Data Strategy
- Technology Preferences

Include step-specific sections for:
- **Service Boundaries**: How services are defined, guiding principles, special cases
- **Communication Patterns**: When synchronous vs asynchronous is used, event-driven patterns
- **Data Strategy**: Data ownership distribution, consistency patterns, replication strategy
- **Technology Preferences**: Stack choices, coding/API standards, infrastructure preferences

## Repeated Review

- **IMPORTANT**
  - This is a complex task that applies to both new creation and updates.
  - The number of iterations depends on the mode:
    - **New Mode**: 2 full iterations for comprehensive coverage
    - **Update Mode**: 1 iteration focused on changes
    - **Review Mode**: As many as needed for user satisfaction
  - Each iteration should focus on:
    1. **First iteration**: Service identification, boundary definition, alignment with domain model, and communication patterns
    2. **Second iteration**: Data ownership, API definitions, overall coherence, scalability, and implementation feasibility
  - Each time, review the results and try to find any missing services or capabilities.
  - Do **not** just bloat the results. Focus on requirements and guidelines vs output.
  - For updates, ensure backward compatibility where possible and document any breaking changes.

- After iterations complete, create a new subtask for verification:
  - Create a new subtask with mode: roo-verify
  - Ask it to "Follow the instructions at prompts/architecture/verify.md".
  - When verification task is done you need to take over one more time.
  - Read the verification file at `workspace/cache/verify_architecture_architecture.md` and address any issues found. If major issues are identified, apply fixes and run verification once more. If verification still finds significant problems, stop and request user assistance.
  - Then you are done.

## Custom Roles

- We start with `roo-arch` custom mode.
  - This role reads all the requirement files, domain model, and user stories, analyzes them, follows the instructions through all review rounds, and handles all file operations.
  - **For existing documents**: First evaluates the current state and determines necessary changes.
  - Stay in `roo-arch` mode throughout the entire process.

- For **Verification**, create a new task in `roo-verify` custom mode. When the verification task completes, continue working in `roo-arch` mode.

## Validate and Resolve Conflicts
If any instructions or details in guidelines, or the PRD appear contradictory, incomplete, or unclear, request clarification from the user. Avoid making assumptions when requirements are ambiguous.