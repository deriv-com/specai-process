# UI Specifications Orchestration Workflow

## Goal
This prompt orchestrates the UI specification workflow. It creates comprehensive UI component specifications based on frontend architecture, user stories, and design patterns, defining visual components, layouts, interactions, and user experience.

**Flow**: Architecture Analysis → Component Identification → UI Specification → Verification

## Operational Modes Support

When creating tasks for UI specifications, you can use three modes:
- `mode=new`: For projects without UI specifications yet
- `mode=update`: For existing UI specs that need updates
- `mode=review`: For reviewing and potentially modifying UI preferences with user engagement

## Preparation
1. **INSTRUCTION FILES**
   - You MUST READ `workspace/output/frontend/architecture.md`: To understand component strategy and technology stack
   - You MUST READ `workspace/output/stories/stories.md`: To extract UI requirements from user stories
   - You MUST READ `workspace/output/requirements/prd.md`: To understand overall system requirements
   - You MUST READ `prompts/ui/guideline.md`: To learn about output standards for UI specifications

## Process

### Step 1: UI Specification Discovery
- Check if UI specifications exist in `workspace/output/frontend/ui/`
- Identify component sets that need specifications:
  - Core components (buttons, forms, cards)
  - Layout components (headers, sidebars, footers)
  - Feature components (from user stories)
  - Data display components (tables, lists, charts)
- Map user stories to UI screens and components

### Step 2: Component Set Selection
Work on component sets in logical order:
1. **Design tokens** (colors, typography, spacing)
2. **Core components** (foundation elements)
3. **Layout components** (application structure)
4. **Navigation components** (menus, breadcrumbs)
5. **Form components** (inputs, validation)
6. **Data display** (tables, lists, cards)
7. **Feature components** (business-specific)
8. **Feedback components** (alerts, modals, toasts)

### Step 3: Execute UI Workflow

For each component set:

#### Mode Determination:
- `mode=new`: If the component set spec does NOT exist
- `mode=update`: If the spec EXISTS and changes may be needed
- `mode=review`: If user explicitly requests preference review

#### For NEW Component Set (mode=new):
1. **Initial Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/ui/ui.md for component_set={component_set_name} mode=new. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the initial result (succeeded/failed)

2. **Self-Review Phase** (if initial development succeeded):
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/ui/ui.md for component_set={component_set_name} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the self-review result (succeeded/failed)

3. **Verification Phase** (if self-review succeeded):
   - Create a new subtask with mode: roo-verify
   - Provide the message: "Follow the instructions at prompts/ui/verify.md for component_set={component_set_name}"
   - Wait for the verification task to complete
   - Read the verification report at `workspace/cache/verify_ui_{component_set_name}.md`

4. **Issue Resolution Phase** (if verification found issues):
   - If the verification report contains issues:
     - Extract only the issues/problems section from the verification report
     - Create a new subtask with mode: roo-arch
     - Provide the message: "Follow the instructions at prompts/ui/ui.md for component_set={component_set_name} mode=update. When done tell me creation <failed|succeeded>. The UI specifications were developed but I found some issues that need to be addressed:
       {issues_found_from_verification_report}
       
       For complete context, please read the full verification report at workspace/cache/verify_ui_{component_set_name}.md"
   - Wait for the task to complete
   - Repeat verification if needed until all issues are resolved

5. Record the final result (succeeded/failed)

#### For EXISTING Component Set (mode=update):
1. **Update Development Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/ui/ui.md for component_set={component_set_name} mode=update. When done tell me creation <failed|succeeded>"
   - Wait for the task to complete
   - Record the update result (succeeded/failed)

2. **Verification Phase** (if update succeeded):
   - Follow the same verification process as for new component sets
   - Handle issue resolution if needed

#### For REVIEW Component Set (mode=review):
1. **Preference Review Phase**:
   - Create a new subtask with mode: roo-arch
   - Provide the message: "Follow the instructions at prompts/ui/ui.md for component_set={component_set_name} mode=review. Engage with the user to review their current UI preferences and help them understand the impact of any modifications they might want to make. When done tell me review <completed|cancelled>"
   - Wait for the task to complete
   - Record the review result

2. **Post-Review Update** (if changes were made):
   - If the review resulted in preference changes:
     - Create an update task to apply the changes
     - Follow the update workflow

### Step 4: Summary Report
After each component set workflow completes, provide a summary:
- Component set name and type
- Mode used (new/update/review)
- Result (succeeded/failed/completed/cancelled)
- Components specified
- If verification was performed, note any issues resolved
- Location of specifications: `workspace/output/frontend/ui/{component_set}/`

### Step 5: Continue or Complete
Present options:
- **Work on next component set**: Suggest the next logical set
- **Work on specific component set**: Ask user which set to work on
- **Complete session**: All desired UI specifications processed

## Important Notes
- UI specifications should follow atomic design principles
- Components must align with frontend architecture technology
- Ensure consistency across all component sets
- Include all interaction states (hover, active, disabled, loading)
- Document responsive behavior for each component
- Specify accessibility requirements (ARIA labels, keyboard nav)
- All UI preferences tracked in `workspace/output/frontend/ui/preferences.md`

## Custom Roles
- Start with `roo-arch` custom mode
- All UI specification tasks must start in `roo-arch` mode
- Creates verification tasks using `roo-verify` mode
- Handles issue resolution by creating follow-up tasks
- Monitors and reports on the results