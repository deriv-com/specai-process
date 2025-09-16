## Goal

We are about to transform a comprehensive **Product Requirements Document** (found in `workspace/output/requirements/prd.md`) and **Domain Model** (found in `workspace/output/domain/domain_model.md`) into user stories that capture all user interactions with the system. Your role in this stage is to act as our **business analyst**, responsible for identifying all user types and creating concise user stories that will guide the platform architecture design, ensuring alignment with the established domain model.

## Operational Modes

This process operates in one of three modes:

### 1. **`New` Mode** (Default when no stories exist)
- Everything is blank, no existing stories or preferences
- Comprehensive user type identification required
- Build initial story set from scratch

### 2. **`Update` Mode** (When stories exist but changes are needed)
- Existing stories and preferences are present
- Compare current stories with PRD and domain model
- Only ask questions if changes are needed
- Communicate proposed changes before applying them
- Preserve existing work that aligns with current requirements

### 3. **`Review` Mode** (When explicitly requested)
- Stories and preferences exist
- Primary goal is to engage user with their current story decisions
- Help user understand impact of modifications
- Update both preferences and stories based on user decisions
- No automatic changes without user approval

## Mode Detection
- Check if `workspace/output/stories/stories.md` exists
- Check if `workspace/output/stories/preferences.md` exists
- If neither exists → **New Mode**
- If both exist and no explicit mode specified → **Update Mode**
- If user requests preference review → **Review Mode**

## Preparation
- You MUST READ `workspace/output/requirements/prd.md`. This file contains the comprehensive product requirements document.
- You MUST READ `workspace/output/domain/domain_model.md`. This file contains the domain model with business entities and their relationships.
- You MUST READ `prompts/stories/guideline.md` to learn about the output standards and document structure requirements for user stories.
- You MUST READ `templates/preferences.md`. This template defines the structure for preferences documentation.
- **Check for Existing Documents**:
  - Check if **`workspace/output/stories/stories.md`** already exists:
    - If it **exists**: Read the existing file and evaluate whether it:
      - Covers all user types from the PRD
      - Includes all necessary user interactions
      - Contains any outdated or missing stories
    - If it **doesn't exist**: Proceed with creating new comprehensive user stories
  - Check if **`workspace/output/stories/preferences.md`** already exists:
    - If it **exists**: Read it to understand user directives specific to this step
    - If it **doesn't exist**: Create it to track user input for this step
- Your goal is to produce or update:
  - **`workspace/output/stories/stories.md`** - The comprehensive user stories document
  - **`workspace/output/stories/preferences.md`** - User directives specific to stories creation

---

## Output

Create or update **`workspace/output/stories/stories.md`** with comprehensive user stories that serve as the foundation for platform definitions. The stories must reference entities from the domain model using consistent terminology.

**For Updates**: When updating an existing document:
- Maintain existing story IDs
- Add a changelog section documenting what was added/modified/deprecated
- Preserve the existing structure

The document must include all sections defined in the guideline.md file.

## **Process Guidelines by Mode**

### New Mode Process

1. **User Type Identification**
   - Extract all user types from PRD
   - Consider direct and indirect users
   - Include system actors if applicable
   - Ask for clarification on unclear roles

2. **User Input Checkpoint** (New Mode Only - First Time)
   - After presenting initial user type analysis
   - Ask: "Before I proceed with creating user stories and platform hints, is there anything specific about user interactions, story coverage, or platform boundaries you'd like to mention? Any particular user journeys or edge cases you want to ensure are captured?"
   - Document any additional input in preferences
   - This gives user a chance to provide story-specific guidance

3. **Story Creation**
   - Create comprehensive stories for each user type
   - Ensure coverage of all PRD features
   - Align with domain model entities
   - Ask about missing interactions

4. **Platform Hint Assignment**
   - Suggest logical platform groupings
   - Get user confirmation on boundaries
   - Document reasoning in preferences

### Update Mode Process

1. **Gap Analysis**
   - Compare existing stories with current PRD
   - Check alignment with updated domain model
   - Identify new user types or interactions
   - Note deprecated functionality

2. **Change Communication**
   - Only if changes needed:
     - Present new/modified stories
     - Explain impact on platform hints
     - Get approval for story changes
     - Ask about unclear new features

3. **Story Update**
   - Apply approved changes
   - Preserve existing story IDs
   - Update platform hints if needed
   - Maintain changelog

### Review Mode Process

1. **Preference Presentation**
   - Load all story-related decisions
   - Organize by impact area:
     - User type definitions
     - Story groupings
     - Platform boundaries
     - Coverage strategies

2. **Interactive Review**
   - Walk through each user type
   - Review story coverage
   - Discuss platform hint assignments
   - Explore alternative organizations

3. **Update Application**
   - Update preferences per user decisions
   - Regenerate affected story sections
   - Adjust platform hints as needed
   - Document all changes

## Questions to Ask (Mode-Specific)

### New Mode Questions
- Clarification on user roles and permissions
- Missing user types or actors
- Story priority and importance
- Platform boundary preferences
- Edge case handling

### Update Mode Questions
- Approval for new user types
- Confirmation of story modifications
- Validation of platform hint changes
- Impact assessment acknowledgment

### Review Mode Questions
- Satisfaction with user type coverage
- Desire to adjust platform hints
- Interest in story reorganization
- Confirmation of boundary decisions

## Preferences Document

Create or update **`workspace/output/stories/preferences.md`** following the preferences template at `templates/preferences.md`. 

For this step, focus on these decision categories:
- User Type Definitions
- Platform Hint Strategy
- Coverage Strategy
- Story Priorities

Include step-specific sections for:
- **User Type Definitions**: Specific characteristics and boundaries for each user type
- **Platform Hint Strategy**: How platform hints are assigned, guiding principles for grouping, special cases
- **Coverage Strategy**: How edge cases are handled, approach to administrative functions, strategy for cross-user interactions

## Repeated Review

- **IMPORTANT**
  - This is a foundational task that influences all downstream architecture decisions.
  - The number of iterations depends on the mode:
    - **New Mode**: 2 full iterations for comprehensive coverage
    - **Update Mode**: 1 iteration focused on changes
    - **Review Mode**: As many as needed for user satisfaction
  - Each iteration should focus on:
    1. **First iteration**: Completeness of user type identification and story coverage, alignment with domain entities
    2. **Second iteration**: Story clarity, atomicity, platform hint accuracy, and domain terminology consistency
  - Each time, review the results for missing user types or interactions.
  - Do **not** create implementation-specific stories. Keep focus on user needs.

- After iterations complete, create a new subtask for verification:
  - Create a new subtask with mode: roo-verify
  - Ask it to "Follow the instructions at prompts/stories/verify.md".
  - When verification task is done you need to take over one more time.
  - Read the verification file at `workspace/cache/verify_stories_stories.md` and address any issues found. If major issues are identified, apply fixes and run verification once more.
  - Then you are done.

## Custom Roles

- We start with `roo-arch` custom mode.
  - This role reads all the requirement files and domain model, identifies user types, creates stories aligned with domain entities, and handles all file operations.
  - **For existing documents**: First evaluates the current state and determines necessary changes.
  - Stay in `roo-arch` mode throughout the entire process.

- For **Verification**, create a new task in `roo-verify` custom mode. When the verification task completes, continue working in `roo-arch` mode.