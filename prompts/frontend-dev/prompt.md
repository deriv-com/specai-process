# Frontend Development Orchestration Workflow

## Goal
This prompt orchestrates the complete frontend development workflow. It implements the frontend application based on architecture and UI specifications, managing the development lifecycle and ensuring implementation aligns with designs.

**Flow**: Preparation → Mode Determination → Development → Verification → Review

## Operational Modes Support

When creating tasks for frontend development, you can use three modes:
- `mode=new`: For frontend applications that don't have implementations yet
- `mode=update`: For existing frontends that need updates
- `mode=review`: For reviewing and potentially modifying development preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/frontend/architecture.md`: Technology stack and patterns
   - You MUST READ `workspace/output/frontend/ui/`: UI component specifications
   - You MUST READ `prompts/frontend-dev/guideline.md`: Development standards
   - Check API specifications in `workspace/output/api/*_public.md`

## Process

### Step 1: Frontend Development Analysis
- Check if frontend implementation exists at `workspace/code/frontend/`
- Review frontend architecture for technology decisions
- Review UI specifications for component requirements
- Identify API endpoints to integrate

### Step 2: Mode Determination
- `mode=new`: If no implementation exists in `workspace/code/frontend/`
- `mode=update`: If implementation exists and changes may be needed
- `mode=review`: If user explicitly requests preference review

### Step 3: Execute Development Workflow

#### For NEW Frontend (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/frontend-dev/develop.md mode=new. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/frontend-dev/develop.md mode=update. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/frontend-dev/verify.md"
   - Wait for the verification task to complete
   - Read the verification report at `workspace/cache/verify_frontend_develop.md`

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask. Use `roo-pe` mode for the task.
     - Provide the message: "Follow the instructions at prompts/frontend-dev/develop.md mode=update. When done tell me development <failed|succeeded>. The frontend was developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at workspace/cache/verify_frontend_develop.md"
   - Wait for the task to complete
   - Repeat verification if needed until all issues are resolved

5. **UX & Performance Review Phase** (if verification passed):
   - Create a new subtask with mode: roo-man
   - Provide the message: "Follow the instructions at prompts/frontend-dev/review.md verification_status=PASS"
   - Wait for the review task to complete
   - Read the review report at `workspace/cache/review_frontend_develop.md`
   - If critical issues found, may need to loop back to Issue Resolution

6. Record the final result (succeeded/failed)

#### For EXISTING Frontend (mode=update):
1. **Update Development Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/frontend-dev/develop.md mode=update. When done tell me development <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new frontend
   - Handle issue resolution if needed
   
3. **UX & Performance Review Phase** (if verification passed):
   - Follow the same review process as for new frontend

#### For REVIEW Frontend (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask. Use `roo-pe` mode for the task.
   - Provide the message: "Follow the instructions at prompts/frontend-dev/develop.md mode=review. Engage with the user to review their current frontend development preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 4: Summary Report
After the workflow completes, provide a summary:
- Frontend framework and architecture
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- Components implemented
- API integrations completed
- If verification was performed, note any issues resolved
- If UX review was performed, note any findings
- Key implementation decisions made
- Location of implementation: `workspace/code/frontend/`

### Step 5: Continue or Complete
Present options:
- **Test the frontend**: Run development server and test
- **Deploy preparation**: Build for production
- **Complete session**: Frontend development is complete

## Important Notes
- Implementation should match complexity score from PRD:
  - 0-3: Simple, minimal structure
  - 4-7: Component-based organization
  - 8-10: Full modular architecture
- Follow the frontend architecture decisions
- Implement all UI specifications
- Integrate with all required APIs
- Include comprehensive error handling
- Optimize for performance from the start
- All development preferences tracked in `workspace/code/frontend/preferences.md`

## Custom Roles
- Start with `roo-arch` custom mode (for orchestration)
- Development tasks use `roo-pe` mode (tasks calling develop.md)
- Verification tasks use `roo-verify` mode (tasks calling verify.md)
- Review tasks use `roo-man` mode (tasks calling review.md)
- Monitors and reports on the results