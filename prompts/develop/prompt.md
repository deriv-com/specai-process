# Development Orchestration Workflow

## Goal
This prompt orchestrates the complete service development workflow. It identifies services from the architecture, manages the development lifecycle, and ensures implementation aligns with specifications.

**Flow**: Service Discovery → Mode Determination → Development → Verification → Review

## Operational Modes Support

When creating tasks for service development, you can use three modes:
- `mode=new`: For services that don't have implementations yet
- `mode=update`: For existing services that need updates
- `mode=review`: For reviewing and potentially modifying development preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/architecture/architecture.md`: The overall service architecture to understand service boundaries and relationships.
   - You MUST READ `prompts/develop/guideline.md`: To learn about the output standards and development requirements.

## Process

### Step 1: Service Discovery & Selection
- Read the service architecture document to identify ALL services
- Check which services already have implementations in `workspace/code/{service_name}/`
- Check if architecture has "Development Order Recommendation" section
- Identify the next logical service to work on based on:
  - Services that don't have implementations yet
  - Dependencies between services (foundation services first)
  - Suggested development order from architecture (if available)
- Present options to user for selection

**Note**: The `list_files` tool can be buggy. If it reports that files or directories don't exist, double-check with Linux commands like `ls` or `find`.

### Step 2: Mode Determination
For the selected service:
- `mode=new`: If no implementation exists in `workspace/code/{service_name}/`
- `mode=update`: If implementation exists and changes may be needed
- `mode=review`: If user explicitly requests preference review for existing service

### Step 3: Execute Development Workflow

#### For NEW Services (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/develop/develop.md for service={service_name} mode=new. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/develop/develop.md for service={service_name} mode=update. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/develop/verify.md for service={service_name}"
   - Wait for the verification task to complete
   - Read the verification report at `workspace/cache/verify_develop_{service_name}.md`

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask. Use `roo-pe` mode for the task.
     - Provide the message: "Follow the instructions at prompts/develop/develop.md for service={service_name} mode=update. When done tell me development <failed|succeeded>. This service was developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at workspace/cache/verify_develop_{service_name}.md"
   - Wait for the task to complete
   - Repeat verification if needed until all issues are resolved

5. **Architecture & Security Review Phase** (if verification passed):
   - Create a new subtask with mode: roo-man
   - Provide the message: "Follow the instructions at prompts/develop/review.md for service={service_name} verification_status=PASS"
   - Wait for the review task to complete
   - Read the review report at `workspace/cache/review_develop_{service_name}.md`
   - If critical issues found, may need to loop back to Issue Resolution

6. Record the final result for the service (succeeded/failed)

#### For EXISTING Services (mode=update):
1. **Update Development Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/develop/develop.md for service={service_name} mode=update. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new services
   - Handle issue resolution if needed
   
3. **Architecture & Security Review Phase** (if verification passed):
   - Follow the same review process as for new services

#### For REVIEW Services (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/develop/develop.md for service={service_name} mode=review. Engage with the user to review their current development preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 4: Summary Report
After the service workflow completes, provide a summary:
- Service name and domain
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- If verification was performed, note any issues that were resolved
- If security review was performed, note any critical findings
- Key implementation decisions made
- Location of the service implementation: `workspace/code/{service_name}/`

### Step 5: Continue or Complete
Present options:
- **Work on next service**: Automatically suggest the next logical service to work on
- **Work on specific service**: Ask user which service they want to work on
- **Complete session**: All desired services have been processed

## Important Notes
- Service implementations should respect the complexity score from PRD
- Each service is developed as a complete unit
- API specifications guide integration patterns
- Dependencies should be developed first
- All development preferences are tracked in `workspace/code/preferences.md`

## Custom Roles
- Start with `roo-arch` custom mode (for orchestration)
- Development tasks use `roo-pe` mode (tasks calling develop.md)
- Verification tasks use `roo-verify` mode (tasks calling verify.md)
- Review tasks use `roo-man` mode (tasks calling review.md)
- Monitors and reports on the results
