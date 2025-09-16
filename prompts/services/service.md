## Goal
We want to create or update detailed specifications for a complete service within a microservice architecture to guide future AIs in implementing the service. The specifications must be comprehensive enough for implementing **all modules and functionality described in the service architecture**.

## Operational Modes

This process operates in one of three modes:

### 1. **`New` Mode** (mode=new)
- Service specification doesn't exist
- Create service specifications from scratch
- Build initial preferences from ground up
- Focus on comprehensive coverage of all architectural requirements

### 2. **`Update` Mode** (mode=update)
- Service specification exists
- Deep gap analysis between current implementation and requirements
- Only ask questions if changes are needed
- Communicate proposed changes before applying them
- Preserve working implementations that align with current requirements

### 3. **`Review` Mode** (mode=review)
- Service specifications and preferences exist
- Primary goal is to engage user with their current service decisions
- Help user understand consequences of modifications
- Update both preferences and specifications based on user decisions
- No automatic changes without user approval

**IMPORTANT**: This prompt expects service name and mode to be provided as parameters:
- `service={service_name}` (e.g., "service=trading") - **MUST be clean service name, NOT service ID**
- `mode={new|update|review}` (e.g., "mode=update")

**CRITICAL**: The service parameter MUST use clean service names like `trading`, `accounts`, `market` for all file system operations. Do NOT use service IDs like `SVC-TR-K3M`.

## Mode Detection and Processing

- Extract parameters from the task
- If `mode=new` → **New Mode**
- If `mode=update` → **Update Mode**
- If `mode=review` → **Review Mode**

## Preparation

### Read Existing Files First
Before making ANY changes or creating ANY new content, you MUST:
1. Check if `workspace/output/services/{service_name}/service.md` exists
2. If it exists, READ the file to understand the current service structure
3. **Never start from scratch if files exist** - This will cause loss of work
4. Report what exists before proceeding with any changes
5. Check if `workspace/output/services/preferences.md` exists:
   - If it **exists**: Read it to understand user directives for service specifications
   - If it **doesn't exist**: Create it to track user input for all service specifications

### INSTRUCTION FILES
- You MUST READ `workspace/output/stories/stories.md`: To understand user interactions (for reference only)
- You MUST READ `workspace/output/requirements/prd.md`: Provides comprehensive product requirements
- **You MUST READ the service architecture: `workspace/output/architecture/architecture.md`**: This is the **authoritative source** for service definitions, boundaries, and requirements
- **CRITICAL: Pay special attention to the "Internal Structure" section of your service in the architecture** - This defines whether the service should have a simple flat structure or multiple modules
- You MUST READ `prompts/services/guideline.md`: To learn about the output standards and document structure requirements for service specifications
- You MUST READ `templates/preferences.md`. This template defines the structure for preferences documentation.

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: Default language, framework, database preferences
   - Persists across project resets within the workspace
2. **Phase Preferences** (`workspace/output/services/preferences.md`):
   - Always check: Contains service-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making technology decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.

### API SPECIFICATIONS
- **For services with APIs**: Check if corresponding API specs exist:
  - Public API: `workspace/output/api/{service_name}_public.md`
  - Internal API: `workspace/output/api/{service_name}_internal.md`
- **For services consuming other services**: Check what internal APIs are available from those services

## Outputs
For the **specified service** using **clean service names** for all file paths:
1. **Verify Service Exists**: Confirm the service is defined in the service architecture
2. **Check Existing Definitions**: Check if `workspace/output/services/{service_name}/service.md` exists
3. **Generate or Update Specs**:
   * Create or update `workspace/output/services/{service_name}/service.md` with comprehensive service specification including ALL modules
   * Update preferences: `workspace/output/services/preferences.md` (single file for all services)
   * Include all sections defined in the guideline.md file
   * Document all modules within the service (persistence, APIs, business logic, etc.)

**IMPORTANT**: Use clean service names (e.g., `trading`, `accounts`) for all file and directory paths. Do NOT use service IDs (e.g., `SVC-TR-K3M`) in the file system structure.

The specification must be comprehensive enough for implementing the complete service functionality described in the service architecture.

## Process Guidelines by Mode

### New Mode Process (mode=new)

1. **Service Analysis**
   - Read service architecture for service requirements
   - Understand all modules needed (APIs, persistence, business logic)
   - Identify dependencies on other services
   - Ask about unclear requirements

2. **User Input Checkpoint** (New Mode Only - First Service Only)
   - **ONLY when workspace/output/services directory has no service.md files (first service being specified)**
   - After presenting initial service analysis
   - Ask: "Before I proceed with detailed service design and specifications, is there anything specific about module organization, technology choices, or implementation patterns you'd like to mention? Any particular approaches or constraints you want to ensure are considered?"
   - Document any additional input in preferences
   - This gives user a chance to provide services-wide guidance
   - **Skip this step if any service.md already exists in workspace/output/services**

3. **Structure Design**
   - **Check the architecture's Internal Structure guidance**
   - If architecture specifies "simple, flat structure":
     - Design as single file or minimal files
     - Avoid creating separate modules
   - If architecture specifies "modules":
     - Design appropriate module structure
   - Ensure complete functional coverage
   - Get feedback on organization

4. **Specification Creation**
   - Create comprehensive service.md following architecture guidance
   - For simple services: Document the flat structure
   - For complex services: Include module details
   - Document how components interact
   - Record all decisions

### Update Mode Process (mode=update)

1. **File Discovery Phase**
   - Check if service.md exists
   - Report what was found
   - Read existing specification

2. **Comprehensive Gap Analysis** (REQUIRED)
   - Read ALL instruction files comprehensively
   - Read current service specification
   - Compare against architectural requirements
   - Provide detailed gap analysis report:
   ```
   Gap Analysis for {service_name} Service:
   
   Requirements vs Implementation Analysis:
   - Architectural requirements missing: [list specific gaps]
   - Guideline violations: [list specific violations]
   - API specification mismatches: [list specific mismatches]
   - Module coverage gaps: [list missing modules]
   - Outdated elements: [list what needs removal]
   
   Change Impact Assessment:
   - High Priority Changes: [list with rationale]
   - Medium Priority Changes: [list with rationale]
   - Low Priority Changes: [list with rationale]
   - Preservation Items: [list what stays]
   
   Implementation Strategy:
   - Sections to modify: [list specific sections]
   - Modules to add: [list new modules needed]
   - Modules to update: [list modules needing changes]
   ```

3. **Change Communication**
   - Present proposed changes
   - Get user approval
   - Ask clarifying questions

4. **Execute Updates**
   - Apply approved changes
   - Preserve valid content
   - Update changelog
   - Document rationale

### Review Mode Process (mode=review)

1. **Preference Presentation**
   - Load all service decisions from preferences
   - Organize by impact area:
     - Module structure
     - Technology choices
     - Design patterns
     - Implementation approaches

2. **Interactive Review**
   - Walk through each design decision
   - Review module organization
   - Discuss technology choices
   - Explore alternative approaches

3. **Update Application**
   - Update preferences per user decisions
   - Regenerate affected service sections
   - Adjust module designs as needed
   - Document all changes

## Questions to Ask (Mode-Specific)

### New Mode Questions
Before asking, check the preference hierarchy for existing answers:
- Module organization preferences (check workspace preferences first)
- Technology stack for the service (check workspace preferences)
- Error handling approaches (check workspace preferences)
- Testing strategy (check workspace preferences)
- Database technology preferences (check workspace preferences)

Only ask if not already specified in preferences or if service-specific override is needed.

### Update Mode Questions
- Approval for structural changes
- Confirmation of module modifications
- Validation of new requirements
- Impact assessment acknowledgment

### Review Mode Questions
- Satisfaction with module structure
- Desire to adjust technology choices
- Interest in different patterns
- Performance optimization needs

## Preferences Document

Create or update **`workspace/output/services/preferences.md`** following the preferences template at `templates/preferences.md`.

**IMPORTANT**: This is a single preferences file for all service specifications across all services.

For this step, focus on these decision categories:
- Service Structure
- Technology Stack
- Module Design
- Implementation Guidelines

Include step-specific sections for:
- **General Service Standards**: Conventions that apply to all services
- **Service Structure**: How modules are organized within services, naming conventions
- **Technology Stack**: Common language, framework choices with rationale
- **Module Design**: Design patterns, inter-module communication, data flow
- **Implementation Guidelines**: Error handling, logging, testing, deployment strategies

Note: Store service-specific preferences with clear labeling (e.g., "[trading] Technology Stack: Python with FastAPI" vs "[accounts] Technology Stack: Node.js with Express")

## Service.md Structure

The service.md file should include:
1. **Service Overview** - Purpose and domain alignment
2. **Tech Stack** - Technologies and rationale
3. **Architecture Design** - Explain the chosen internal architecture
4. **Directory Structure** - Show the actual file structure
5. **Component/Module Specifications**:
   - For simple services: Document the main components within files
   - For complex services: Document each module separately
6. **Data Architecture** - Database design, models, persistence strategy
7. **Security Architecture** - Authentication, authorization, data protection
8. **Performance & Scalability** - How the service handles load
9. **Error Handling & Resilience** - Error strategies
10. **External Dependencies** - Other services this depends on
11. **Development Guidelines** - Code organization, testing, deployment

## SELF-REVIEW AND CONCLUSION

**Self-Review (REQUIRED)**:
Before concluding:
- Review all your previous messages
- Check against workflow steps for your mode
- Validate completeness of all modules
- Fix any identified issues
- Report: "Self-review complete. All required steps have been executed."

**Conclude**:
- Inform completion with: **Service specification is complete for: service={service_name}**

## Custom Roles
- Start with `roo-arch` custom mode
- Stay in `roo-arch` mode throughout the entire process for all analysis and file operations