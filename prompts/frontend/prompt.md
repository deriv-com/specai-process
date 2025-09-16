# Frontend Architecture Orchestration Workflow

## Goal
This prompt orchestrates the frontend architecture workflow. It analyzes API specifications and user stories to design the frontend application architecture, defining technology stack, component architecture, state management strategy, and integration patterns.

**Flow**: Input Analysis → Mode Determination → Architecture Design → Verification

## Operational Modes Support

When creating tasks for frontend architecture, you can use three modes:
- `mode=new`: For projects without frontend architecture yet
- `mode=update`: For existing architectures that need updates
- `mode=review`: For reviewing and potentially modifying architecture preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/requirements/prd.md`: To understand complexity score and system requirements
   - You MUST READ `workspace/output/stories/stories.md`: To understand user interactions and UI needs
   - You MUST READ `workspace/output/architecture/architecture.md`: To understand service boundaries and API providers
   - You MUST READ `prompts/frontend/guideline.md`: To learn about output standards for frontend architecture

## Process

### Step 1: Frontend Architecture Analysis
- Check if frontend architecture exists at `workspace/output/frontend/architecture.md`
- Identify all public APIs from `workspace/output/api/*_public.md`
- Extract complexity score from PRD for framework selection guidance
- Analyze user stories for UI requirements

### Step 2: Mode Determination
- `mode=new`: If `workspace/output/frontend/architecture.md` does NOT exist
- `mode=update`: If architecture EXISTS and changes may be needed
- `mode=review`: If user explicitly requests preference review

### Step 3: Execute Frontend Architecture Workflow

#### For NEW Architecture (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/frontend/frontend.md mode=new. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/frontend/frontend.md mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/frontend/verify.md"
   - Wait for the verification task to complete
   - Read the verification report at `workspace/cache/verify_frontend_architecture.md`

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask with mode: roo-arch
     - Provide the message: "Follow the instructions at prompts/frontend/frontend.md mode=update. When done tell me creation <failed|succeeded>. The frontend architecture was developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at workspace/cache/verify_frontend_architecture.md"
   - Wait for the task to complete
   - Repeat verification if needed until all issues are resolved

5. Record the final result (succeeded/failed)

#### For EXISTING Architecture (mode=update):
1. **Update Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/frontend/frontend.md mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new architecture
   - Handle issue resolution if needed

#### For REVIEW Architecture (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/frontend/frontend.md mode=review. Engage with the user to review their current frontend architecture preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 4: Summary Report
After the workflow completes, provide a summary:
- Architecture approach (SPA, SSR, static, etc.)
- Framework selected based on complexity
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- If verification was performed, note any issues resolved
- Location of the architecture: `workspace/output/frontend/architecture.md`

### Step 5: Next Steps
Present options:
- **Continue to UI Specifications**: Design UI components based on architecture
- **Skip to Frontend Development**: If UI specs exist
- **Complete session**: Frontend architecture is ready

## Important Notes
- Framework selection is guided by PRD complexity score:
  - 0-3: Vanilla HTML/CSS/JS or lightweight frameworks
  - 4-7: React/Vue SPA with component architecture
  - 8-10: Next.js/Nuxt with SSR, micro-frontends
- Architecture must align with API specifications
- Consider performance requirements from the start
- Plan for responsive design across devices
- Include accessibility requirements

## Custom Roles
- Start with `roo-arch` custom mode
- All frontend architecture tasks must start in `roo-arch` mode
- Creates verification tasks using `roo-verify` mode
- Handles issue resolution by creating follow-up tasks
- Monitors and reports on the results