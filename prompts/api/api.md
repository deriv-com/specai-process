# API Specification

This document outlines project-specific preferences for generating APIs for domain services.

## Operational Modes

This process operates in one of three modes:

### 1. **`New` Mode** (Default when no API spec exists)
- Everything is blank, no existing API specification or preferences
- Comprehensive API design required
- Build initial specification from scratch

### 2. **`Update` Mode** (When API spec exists but changes are needed)
- Existing API specification and preferences are present
- Compare current spec with service architecture and requirements
- Only ask questions if changes are needed
- Communicate proposed changes before applying them
- Preserve existing work that aligns with current requirements

### 3. **`Review` Mode** (When explicitly requested)
- API specification and preferences exist
- Primary goal is to engage user with their current API decisions
- Help user understand consequences of modifications
- Update both preferences and API spec based on user decisions
- No automatic changes without user approval

## Mode Detection
You will be provided with specific parameters:
- `service_name`: The **clean service name** (e.g., `trading`, `accounts`, `market`) - NOT service ID
- `api_type`: Either "public" or "internal"

**IMPORTANT**: The `service_name` parameter MUST be a clean, single-word service name for file system usage, NOT a service ID like `SVC-TR-K3M`.

Then check:
- If `workspace/output/api/{service_name}_{api_type}.md` exists
- If `workspace/output/api/preferences.md` exists
- If neither exists → **New Mode**
- If both exist and no explicit mode specified → **Update Mode**
- If user requests preference review → **Review Mode**

## Important Note
You must create or update the API specification ONLY for the specified service and API type.

## Preparation

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: API style, authentication patterns, versioning strategy
   - Persists across project resets
2. **Phase Preferences** (`workspace/output/api/preferences.md`):
   - Always check: Contains API-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making API design decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.

1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/architecture/architecture.md`: This contains the overall service architecture
   - You MUST READ `workspace/output/requirements/prd.md`: The comprehensive product requirements document
   - You MUST READ `prompts/api/guideline.md` to learn about the output standards and document structure requirements for API specifications
   - You MUST READ `templates/preferences.md`. This template defines the structure for preferences documentation.
   - For **internal APIs**, check the Inter-Service Communication Matrix in service architecture to understand what other services need from this service

2. **CHECK FOR EXISTING API SPECIFICATIONS**:
   - Before creating a new specification, check if the target API specification file already exists:
     - For public API: `workspace/output/api/{service_name}_public.md`
     - For internal API: `workspace/output/api/{service_name}_internal.md`
   - If it **exists**: Read the existing file and evaluate whether it:
     - Fully covers all requirements for this API type
     - Aligns with the current service architecture
     - Contains any outdated or incorrect information
     - Supports all necessary endpoints
   - If it **doesn't exist**: Proceed with creating a new comprehensive API specification
   - Check if **`workspace/output/api/preferences.md`** already exists:
     - If it **exists**: Read it to understand user directives for API specifications
     - If it **doesn't exist**: Create it to track user input for all API specifications

**IMPORTANT**: Before proceeding, ensure you have read all required files and checked for existing specifications.

## Output

Generate or update comprehensive API specifications using **clean service names** for all file paths:
- Public API: `workspace/output/api/{service_name}_public.md`
- Internal API: `workspace/output/api/{service_name}_internal.md`
- Preferences: `workspace/output/api/preferences.md` (single file for all API specifications)

**CRITICAL**: Use the clean service name (e.g., `trading`, `accounts`) for all file paths. Do NOT use service IDs (e.g., `SVC-TR-K3M`) in file system structures.

The specifications must:
- Stay within service boundaries defined in `service_architecture.md`
- Support all required functionality for the API type (public or internal)
- Enable clean integration patterns between services
- Follow consistent design principles across the system
- Include all sections defined in the guideline.md file

## Process Guidelines by Mode

### New Mode Process

1. **Feature/Requirement Extraction**
   - For public APIs: Extract features from PRD and frontend features
   - For internal APIs: Extract from Inter-Service Communication Matrix
   - Map features to specific endpoints
   - Ask about unclear requirements

2. **User Input Checkpoint** (New Mode Only - First API Only)
   - **ONLY when workspace/output/api directory is empty (first API being developed)**
   - After presenting initial feature extraction and endpoint mapping
   - Ask: "Before I proceed with detailed API design and specification, is there anything specific about endpoint design, data formats, or error handling you'd like to mention? Any particular API patterns or standards you want to follow?"
   - Document any additional input in preferences
   - This gives user a chance to provide API-wide guidance
   - **Skip this step if any API already exists in workspace/output/api**

3. **API Design**
   - Create comprehensive endpoint definitions
   - Design consistent data models
   - Establish error handling patterns
   - Get feedback on design decisions

4. **Specification Creation**
   - Build complete API specification
   - Include all required sections
   - Provide helpful examples
   - Document all decisions

### Update Mode Process

1. **Gap Analysis**
   - Compare existing spec with current requirements
   - Check alignment with service architecture
   - Identify new endpoints needed
   - Note deprecated functionality

2. **Change Communication**
   - Only if changes needed:
     - Present API modifications
     - Explain breaking changes
     - Get approval for updates
     - Ask about unclear features

3. **Specification Update**
   - Apply approved changes
   - Preserve working endpoints
   - Update data models as needed
   - Document changes in changelog

### Review Mode Process

1. **Preference Presentation**
   - Load all API design decisions
   - Organize by impact area:
     - Endpoint design patterns
     - Data model choices
     - Error handling strategies
     - Authentication approaches

2. **Interactive Review**
   - Walk through each design decision
   - Review endpoint organization
   - Discuss data model choices
   - Explore alternative approaches

3. **Update Application**
   - Update preferences per user decisions
   - Regenerate affected API sections
   - Adjust endpoints as needed
   - Document all changes

## Questions to Ask (Mode-Specific)

### New Mode Questions
- Endpoint naming preferences
- Data format preferences (nested vs flat)
- Error response structure
- Pagination approach
- Authentication requirements

### Update Mode Questions
- Approval for new endpoints
- Confirmation of breaking changes
- Validation of data model updates
- Backward compatibility needs

### Review Mode Questions
- Satisfaction with endpoint design
- Desire to adjust data models
- Interest in different patterns
- Performance optimization needs

## Preferences Document

Create or update **`workspace/output/api/preferences.md`** following the preferences template at `templates/preferences.md`.

**IMPORTANT**: This is a single preferences file for all API specifications across all services.

For this step, focus on these decision categories:
- Endpoint Design Patterns
- Data Model Strategy
- Error Handling
- Authentication Methods

Include step-specific sections for:
- **General API Standards**: Conventions that apply to all APIs
- **Endpoint Design Patterns**: Naming convention, versioning strategy, resource organization
- **Data Model Strategy**: JSON structure preferences, field naming conventions, relationship representation
- **Error Handling**: Error response format, error code strategy, user-facing vs technical messages
- **Authentication** (Public API): Method (OAuth/JWT/API Keys), scopes if applicable, rate limiting strategy

Note: Store service-specific and API type-specific preferences with clear labeling (e.g., "[trading] Public API: Authentication Method" vs "[accounts] Internal API: Service Discovery")

## Repeated Review

- **Iteration Process**
  * The number of iterations depends on the mode:
    - **New Mode**: 2 full iterations for comprehensive coverage
    - **Update Mode**: 1 iteration focused on changes
    - **Review Mode**: As many as needed for user satisfaction
  * Review and improve through iterations:
    1. **First iteration**: Endpoint completeness and alignment with requirements
    2. **Second iteration**: Consistency, usability, and implementation feasibility
  * After iterations, create verification task:
    - Create a new subtask with mode: roo-verify
    - Ask it to "Follow the instructions at prompts/api/verify.md for service={service_name} and api_type={api_type}"
    - Read verification results and address any issues
  * If verification finds major issues, fix and verify again

## Handling Existing API Specifications
When an API specification already exists:
- Perform comprehensive gap analysis against current requirements
- Identify endpoints that need to be added, modified, or deprecated
- Check if existing data models need updates
- Verify authentication and authorization alignment
- Preserve valuable existing examples and documentation
- Clearly communicate proposed changes before implementing
- Request approval for breaking changes

## Custom Roles
- Start with `roo-arch` custom mode
  - Reads all requirement files and analyzes them
  - For existing specifications: Evaluates current state and determines changes
  - Handles all file creation and updates
  - Stay in `roo-arch` mode throughout the entire process

- For **Verification**, create a new task in `roo-verify` custom mode. When the verification task completes, continue working in `roo-arch` mode.