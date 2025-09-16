## Goal

We are about to transform the **Product Requirements Document** (found in `workspace/output/requirements/prd.md`) into a comprehensive domain model that captures the core business entities, their relationships, and data architecture. Your role in this stage is to act as our **domain architect**, responsible for identifying business entities, establishing relationships, defining data ownership, and creating a unified conceptual model that will guide platform boundaries and data distribution.

## Operational Modes

This process operates in one of three modes:

### 1. **`New` Mode** (Default when no domain model exists)
- Everything is blank, no existing domain model or preferences
- Comprehensive entity extraction and modeling required
- Build initial preferences from scratch

### 2. **`Update` Mode** (When domain model exists but changes are needed)
- Existing domain model and preferences are present
- Compare current model with PRD requirements
- Only ask questions if changes are needed
- Communicate proposed changes before applying them
- Preserve existing work that aligns with current requirements

### 3. **`Review` Mode** (When explicitly requested)
- Domain model and preferences exist
- Primary goal is to engage user with their current modeling decisions
- Help user understand consequences of modifications
- Update both preferences and domain model based on user decisions
- No automatic changes without user approval

## Mode Detection
- Check if `workspace/output/domain/domain_model.md` exists
- Check if `workspace/output/domain/preferences.md` exists
- If neither exists → **New Mode**
- If both exist and no explicit mode specified → **Update Mode**
- If user requests preference review → **Review Mode**

## Preparation
- You MUST READ `workspace/output/requirements/prd.md`. This file contains the comprehensive product requirements document.
- You MUST READ `prompts/domain/guideline.md` to learn about the output standards and document structure requirements for domain modeling.
- You MUST READ `templates/preferences.md`. This template defines the structure for preferences documentation.
- **Check for Existing Documents**:
  - Check if **`workspace/output/domain/domain_model.md`** already exists:
    - If it **exists**: Read the existing file and evaluate whether it:
      - Covers all business entities from the PRD
      - Includes all necessary relationships
      - Contains any outdated or missing elements
    - If it **doesn't exist**: Proceed with creating new comprehensive domain model
  - Check if **`workspace/output/domain/preferences.md`** already exists:
    - If it **exists**: Read it to understand user directives specific to this step
    - If it **doesn't exist**: Create it to track user input for this step
- Your goal is to produce or update:
  - **`workspace/output/domain/domain_model.md`** - The comprehensive domain model and data architecture
  - **`workspace/output/domain/preferences.md`** - User directives specific to domain modeling

---

## Output

Create or update **`workspace/output/domain/domain_model.md`** with a comprehensive domain model that serves as the foundation for platform definitions and data architecture.

**For Updates**: When updating an existing document:
- Maintain existing entity definitions that remain accurate
- Add a changelog section documenting what was added/modified/deprecated
- Preserve the existing structure unless changes are necessary

The document must include all sections defined in the guideline.md file.

## **Process Guidelines by Mode**

### New Mode Process

1. **Entity Extraction**
   - Identify all business entities from the PRD
   - Focus on nouns that represent core business concepts
   - Distinguish between entities and attributes
   - Group related entities into logical domains

2. **User Input Checkpoint** (New Mode Only - First Time)
   - After presenting initial entity analysis
   - Ask: "Before I proceed with domain modeling questions and creating the domain model, is there anything specific about the data architecture, entity relationships, or domain boundaries you'd like to mention? Any particular patterns or approaches you prefer?"
   - Document any additional input in preferences
   - This gives user a chance to provide domain-specific guidance

3. **Comprehensive Questions**
   - Ask about unclear entity boundaries
   - Clarify relationship cardinalities
   - Confirm data ownership strategies
   - Validate consistency requirements

4. **Model Creation**
   - Build complete domain model
   - Define all relationships
   - Establish domain boundaries
   - Document all decisions in preferences

### Update Mode Process

1. **Gap Analysis**
   - Compare existing model with current PRD
   - Identify new entities or relationships
   - Check for deprecated elements
   - Assess alignment with updated requirements

2. **Change Communication**
   - Only if changes needed:
     - Present proposed modifications
     - Explain impact on domain boundaries
     - Get user approval for structural changes
     - Ask clarifying questions for new elements

3. **Model Update**
   - Apply approved changes
   - Preserve valid existing content
   - Update changelog
   - Maintain backward compatibility where possible

### Review Mode Process

1. **Preference Presentation**
   - Load all current modeling decisions
   - Organize by impact area:
     - Entity definitions
     - Domain boundaries
     - Data ownership
     - Consistency patterns

2. **Interactive Review**
   - Walk through each decision category
   - Explain current choices and impacts
   - Offer alternative approaches
   - Discuss trade-offs

3. **Update Application**
   - Update preferences per user decisions
   - Regenerate affected model sections
   - Document all changes with rationale

## Questions to Ask (Mode-Specific)

### New Mode Questions
- Entity boundary clarifications
- Relationship cardinality confirmations
- Data ownership preferences
- Consistency requirements
- Domain grouping validations

### Update Mode Questions
- Approval for entity additions/removals
- Confirmation of relationship changes
- Validation of new domain boundaries
- Impact assessment acknowledgment

### Review Mode Questions
- Satisfaction with current boundaries
- Desire to adjust data ownership
- Interest in alternative patterns
- Confirmation of trade-off acceptance

## Preferences Document

Create or update **`workspace/output/domain/preferences.md`** following the preferences template at `templates/preferences.md`. 

For this step, focus on these decision categories:
- Entity Boundaries
- Domain Groupings
- Data Ownership Strategy
- Consistency Patterns

Include step-specific sections for:
- **Domain Boundaries**: How domains are separated, criteria for boundary definition, special cases
- **Data Ownership Strategy**: Centralized/Distributed/Hybrid approach, ownership assignment rules, shared data handling
- **Consistency Patterns**: Where strong consistency is required, where eventual consistency is acceptable, transaction boundary definitions

## Repeated Review

- **IMPORTANT**
  - This is a foundational task that influences platform boundaries and data distribution.
  - The number of iterations depends on the mode:
    - **New Mode**: 2 full iterations for comprehensive coverage
    - **Update Mode**: 1 iteration focused on changes
    - **Review Mode**: As many as needed for user satisfaction
  - Each iteration should focus on:
    1. **First iteration**: Entity completeness and relationship accuracy
    2. **Second iteration**: Domain boundaries, data ownership, and consistency patterns
  - Each time, review for missing entities or unclear relationships.
  - Do **not** include implementation details. Keep focus on conceptual model.

- After iterations complete, create a new subtask for verification:
  - Create a new subtask with mode: roo-verify
  - Ask it to "Follow the instructions at prompts/domain/verify.md".
  - When verification task is done you need to take over one more time.
  - Read the verification file at `workspace/cache/verify_domain_model.md` and address any issues found. If major issues are identified, apply fixes and run verification once more.
  - Then you are done.

## Custom Roles

- We start with `roo-arch` custom mode.
  - This role reads all the requirement files, identifies entities, creates the domain model, and handles all file operations.
  - **For existing documents**: First evaluates the current state and determines necessary changes.
  - Stay in `roo-arch` mode throughout the entire process.

- For **Verification**, create a new task in `roo-verify` custom mode. When the verification task completes, continue working in `roo-arch` mode.