## Goal
This prompt orchestrates the complete service specification workflow. It identifies all services from the architecture, presents their current status, allows service selection, and manages the full development lifecycle for service specifications.

**Flow**: Service Discovery → Status Presentation → Service Selection → Mode Determination → Workflow Orchestration

## Operational Modes Support

When creating tasks for services, you can use three modes:
- `mode=new`: For services that don't have specifications yet
- `mode=update`: For existing services that need updates
- `mode=review`: For reviewing and potentially modifying service preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/architecture/architecture.md`: The overall service architecture to understand service boundaries and relationships.
   - You MUST READ `prompts/services/guideline.md`: To learn about the output standards and document structure requirements for service specifications.

## Process

### Step 1: Service Discovery & Next Service Selection
- Read the service architecture document to identify ALL services
- Check which services are already completed (`service.md` exists)
- Check if architecture has "Development Order Recommendation" section
- Identify the next logical service to work on based on:
  - Services that don't have specifications yet
  - Dependencies between services (foundation services first)
  - Suggested development order from architecture (if available)

### Step 2: Execute Service Workflow
Work on the selected next service, determine its mode and execute the appropriate workflow:

#### Mode Determination:
- `mode=new`: If service.md does NOT exist
- `mode=update`: If service.md EXISTS and changes may be needed
- `mode=review`: If user explicitly requests preference review for existing service

## Service Development Workflows

### For NEW Services (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/services/service.md for service={service_name} mode=new. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/services/service.md for service={service_name} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/services/verify.md for service={service_name}"
   - Wait for the verification task to complete
   - Read the verification report

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask with mode: roo-arch
     - Provide the message: "Follow the instructions at prompts/services/service.md for service={service_name} mode=update. When done tell me creation <failed|succeeded>. This service was developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at workspace/cache/verify_service_{service_name}.md"
  - Wait for the task to complete
  - Repeat verification if needed until all issues are resolved

**NOTE**: All file paths use clean service names, ensuring developer-friendly directory structures.

5. Record the final result for the service (succeeded/failed)

## For EXISTING Services (mode=update):
1. **Update Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/services/service.md for service={service_name} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new services
   - Handle issue resolution if needed

## For REVIEW Services (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/services/service.md for service={service_name} mode=review. Engage with the user to review their current service preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 3: Summary Report
After the service workflow completes, provide a summary:
- Service name and domain
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- If verification was performed, note any issues that were resolved
- Location of the service specification: `workspace/output/services/{service_name}/service.md`

### Step 4: Continue or Complete
Present options:
- **Work on next service**: Automatically suggest the next logical service to work on
- **Work on specific service**: Ask user which service they want to work on
- **Complete session**: All desired services have been processed

**Final Result**: Clean, developer-friendly file structure using service names like `trading/`, not service IDs like `SVC-TR-K3M/`.

## Important Notes
- Stay within the specified service's boundaries
- Modules within a service can directly call each other
- Cross-service communication only through published APIs
- Each service has its own persistence layer - no shared databases
- Module naming follows pattern: `{service_name}-{function}` (e.g., trading-persistence, trading-engine)
- All modules are documented within the single service.md file

## Custom Roles
- Start with `roo-arch` custom mode
- All service development tasks must start in `roo-arch` mode
- Creates new tasks for service specification
- Creates verification tasks using `roo-verify` mode
- Handles issue resolution by creating follow-up development tasks
- Monitors and reports on the results