## Goal
This prompt orchestrates the complete API specification workflow. It identifies all services that need APIs from the architecture, determines which APIs exist, and manages the development lifecycle for API specifications.

**Flow**: Service Discovery → API Discovery → Next API Selection → Workflow Orchestration

## Operational Modes Support

When creating tasks for API specifications, you can use three modes:
- `mode=new`: For APIs that don't have specifications yet
- `mode=update`: For existing APIs that need updates
- `mode=review`: For reviewing and potentially modifying API preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/architecture/architecture.md`: The overall service architecture to understand which services exist and their API needs.
   - You MUST READ `prompts/api/guideline.md`: To learn about the output standards and document structure requirements for API specifications.

## Process

### Step 1: Service & API Discovery
- Read the service architecture document to identify ALL services
- For each service, determine:
  - Does it need a public API? (check if it exposes functionality to external clients)
  - Does it need an internal API? (check if other services depend on it)
- Check which API specifications already exist:
  - Public: `workspace/output/api/{service_name}_public.md`
  - Internal: `workspace/output/api/{service_name}_internal.md`
- Identify the next logical API to work on based on:
  - APIs that don't have specifications yet
  - Dependencies between services (APIs needed by other services first)
  - Suggested development order from architecture (if available)

### Step 2: Execute API Workflow
Work on the selected API, determine its mode and execute the appropriate workflow:

#### Mode Determination:
- `mode=new`: If the API specification does NOT exist
- `mode=update`: If the API specification EXISTS and changes may be needed
- `mode=review`: If user explicitly requests preference review for existing API

## API Development Workflows

### For NEW APIs (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/api/api.md for service={service_name} and api_type={api_type} mode=new. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/api/api.md for service={service_name} and api_type={api_type} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/api/verify.md for service={service_name} and api_type={api_type}"
   - Wait for the verification task to complete
   - Read the verification report

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask with mode: roo-arch
     - Provide the message: "Follow the instructions at prompts/api/api.md for service={service_name} and api_type={api_type} mode=update. When done tell me creation <failed|succeeded>. This API was developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at:
       - For public API: workspace/cache/verify_api_{service_name}_public.md
       - For internal API: workspace/cache/verify_api_{service_name}_internal.md"
   - Wait for the task to complete
   - Repeat verification if needed until all issues are resolved

**NOTE**: All file paths use clean service names, ensuring developer-friendly directory structures.

5. Record the final result for the API (succeeded/failed)

### For EXISTING APIs (mode=update):
1. **Update Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/api/api.md for service={service_name} and api_type={api_type} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new APIs
   - Handle issue resolution if needed

### For REVIEW APIs (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/api/api.md for service={service_name} and api_type={api_type} mode=review. Engage with the user to review their current API preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 3: Summary Report
After the API workflow completes, provide a summary:
- Service name and API type
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- If verification was performed, note any issues that were resolved
- Location of the API specification:
  - Public: `workspace/output/api/{service_name}_public.md`
  - Internal: `workspace/output/api/{service_name}_internal.md`

### Step 4: Continue or Complete
Present options:
- **Work on next API**: Automatically suggest the next logical API to work on
- **Work on specific API**: Ask user which API they want to work on
- **Complete session**: All desired APIs have been processed

## Important Notes
- Each service can have both public and internal APIs
- Public APIs are for external clients (web apps, mobile apps, third parties)
- Internal APIs are for service-to-service communication
- Not all services need both types of APIs
- Check the Inter-Service Communication Matrix to determine internal API needs
- API specifications should align with service boundaries and responsibilities

## Custom Roles
- Start with `roo-arch` custom mode
- All API development tasks must start in `roo-arch` mode
- Creates new tasks for API specification
- Creates verification tasks using `roo-verify` mode
- Handles issue resolution by creating follow-up development tasks
- Monitors and reports on the results