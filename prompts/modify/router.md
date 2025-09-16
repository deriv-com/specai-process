# Modification Router

## Goal

This prompt handles user modification requests after initial development is complete. It analyzes the modification, determines the correct entry point in the development pipeline, records the change as a directive in the appropriate preferences file, and triggers the update cascade through subsequent steps.

**Core Principle**: We record the CURRENT DESIRED STATE, not history. Each directive represents what the system should be NOW, replacing any conflicting previous directives.

## Preparation

### Step 1: Understand the Development Process (REQUIRED)
You MUST FIRST understand what each phase does by reading:
1. **Process Manifest**: Read `tools/templates/process_files.md` to get overview of all phases
2. **Phase Overviews**: Read ALL files in `tools/templates/phase_overviews/`:
   - `requirements_overview.md` - What Requirements phase creates and handles
   - `domain_overview.md` - What Domain Modeling phase creates and handles
   - `stories_overview.md` - What User Stories phase creates and handles
   - `architecture_overview.md` - What Architecture phase creates and handles
   - `api_overview.md` - What API Specifications phase creates and handles
   - `services_overview.md` - What Service Specifications phase creates and handles
   - `develop_overview.md` - What Backend Development phase creates and handles
   - `frontend_architecture_overview.md` - What Frontend Architecture phase creates and handles
   - `ui_overview.md` - What UI Specifications phase creates and handles
   - `frontend_development_overview.md` - What Frontend Development phase creates and handles
   - `integration_overview.md` - What Integration phase creates and handles
   - `modify_overview.md` - How modifications cascade through phases

This gives you complete understanding of:
- What each phase is responsible for
- What artifacts each phase creates
- What types of changes belong to each phase
- How phases depend on each other

### Step 2: Understand Current System State (REQUIRED)
Then READ these files to understand the current implementation:
- `workspace/output/requirements/prd.md`: Current product requirements
- `workspace/output/domain/domain_model.md`: Current domain model
- `workspace/output/stories/stories.md`: Current user stories
- `workspace/output/architecture/architecture.md`: Current service architecture
- Check for API specifications in `workspace/output/api/`
- Check for service specifications in `workspace/output/services/*/service.md`
- Check for backend implementations in `workspace/code/*/`
- Check for frontend architecture in `workspace/output/frontend/architecture.md`
- Check for UI specifications in `workspace/output/frontend/ui/`
- Check for frontend implementation in `workspace/code/frontend/`
- Read ALL existing preferences.md files to understand current directives

## Process

### Step 1: Confirm Understanding
Before analyzing any modification, ensure you have:
- [ ] Read the process manifest and ALL phase overviews
- [ ] Understood what each phase handles
- [ ] Read current system state files
- [ ] Understood existing directives

If not, go back to Preparation section.

### Step 2: Analyze the Modification Request

When a user provides a modification request, analyze:
1. **What is being changed?** (feature, behavior, constraint, technology, security)
2. **What is the scope?** (single service, multiple services, entire system)
3. **What artifacts are affected?** (requirements, domain, APIs, code)
4. **Is this a security issue?** (vulnerability, exposure, access control)

**⚠️ SECURITY ISSUES SPECIAL HANDLING:**
Security vulnerabilities should be classified based on WHERE the fix needs to happen:
- Frontend security (XSS, file access) → Level 10
- Backend security (SQL injection, auth) → Level 7
- API security (authentication, rate limits) → Level 5
- Configuration security (CORS, CSP) → Level 11

### Step 3: Classify the Modification

Using your understanding from the phase overviews, determine the modification level and entry point.

**KEY PRINCIPLE**: Match the modification to the phase that CREATES or OWNS the artifact being changed.

#### Classification Guide:
Ask yourself these questions in order:
1. Does this change business features, rules, or requirements? → Level 1 (Requirements)
2. Does this change data entities or relationships? → Level 2 (Domain)
3. Does this change user workflows or interactions? → Level 3 (Stories)
4. Does this change service boundaries or communication? → Level 4 (Architecture)
5. Does this change API contracts or endpoints? → Level 5 (API)
6. Does this change internal service design? → Level 6 (Service)
7. Is this a backend code-only change? → Level 7 (Backend Dev)
8. Does this change frontend framework or architecture? → Level 8 (Frontend Arch)
9. Does this change UI components or layouts? → Level 9 (UI Specs)
10. Is this a frontend code-only change? → Level 10 (Frontend Dev)
11. Does this change Docker/environment config? → Level 11 (Integration)

#### Level 1: Business/Requirements Changes
**Phase Overview Reference**: See `requirements_overview.md` for what this phase handles
**Indicators:**
- New features or removed features
- Changed business rules or constraints
- Different success metrics or KPIs
- Modified regulatory requirements
- Changed user types or permissions
**Key Artifacts**: PRD, business requirements, success metrics

**Entry Point:** Requirements
**Record in:** `workspace/output/requirements/preferences.md`
**Start update from:** `prompts/requirements/prompt.md`

#### Level 2: Domain/Data Changes
**Phase Overview Reference**: See `domain_overview.md` for what this phase handles
**Indicators:**
- New entities or removed entities
- Changed entity relationships
- Modified data ownership
- Different consistency requirements
- New domain boundaries
**Key Artifacts**: Domain model, entity relationships, data architecture

**Entry Point:** Domain Modeling
**Record in:** `workspace/output/domain/preferences.md`
**Start update from:** `prompts/domain/prompt.md`

#### Level 3: User Interaction Changes
**Phase Overview Reference**: See `stories_overview.md` for what this phase handles
**Indicators:**
- New user workflows
- Changed user stories
- Modified user journeys
- Different interaction patterns
- Changed permissions or access
**Key Artifacts**: User stories, user types, interaction flows

**Entry Point:** User Stories
**Record in:** `workspace/output/stories/preferences.md`
**Start update from:** `prompts/stories/prompt.md`

#### Level 4: Service Architecture Changes
**Phase Overview Reference**: See `architecture_overview.md` for what this phase handles
**Indicators:**
- Service splits or merges
- Changed service boundaries
- Modified communication patterns
- Different data distribution
- New service dependencies
**Key Artifacts**: Service architecture, boundaries, communication matrix

**Entry Point:** Architecture
**Record in:** `workspace/output/architecture/preferences.md`
**Start update from:** `prompts/architecture/prompt.md`

#### Level 5: API Contract Changes
**Phase Overview Reference**: See `api_overview.md` for what this phase handles
**Indicators:**
- New endpoints or removed endpoints
- Changed request/response formats
- Modified authentication methods
- Different error codes
- New webhook events
- API security changes (rate limits, auth methods)
**Key Artifacts**: API specifications, endpoints, contracts

**Entry Point:** API Specifications
**Record in:** `workspace/output/api/preferences.md`
**Start update from:** `prompts/api/prompt.md`

#### Level 6: Service Implementation Changes
**Phase Overview Reference**: See `services_overview.md` for what this phase handles
**Indicators:**
- Internal module reorganization
- Technology stack changes
- Different design patterns
- Changed algorithms
- Modified performance optimizations
**Key Artifacts**: Service specifications, module designs, tech stack

**Entry Point:** Service Specifications
**Record in:** `workspace/output/services/preferences.md`
**Start update from:** `prompts/services/prompt.md`

#### Level 7: Backend Code-Only Changes
**Phase Overview Reference**: See `develop_overview.md` for what this phase handles
**Indicators:**
- Backend bug fixes (but we don't handle bugs here)
- Code refactoring
- Performance improvements
- Better error handling
- Improved logging
- **Backend security fixes** (SQL injection, authentication bypass, etc.)
**Key Artifacts**: Backend code implementation

**Entry Point:** Backend Development
**Record in:** `workspace/code/preferences.md`
**Start update from:** `prompts/develop/prompt.md`

#### Level 8: Frontend Architecture Changes
**Phase Overview Reference**: See `frontend_architecture_overview.md` for what this phase handles
**Indicators:**
- Framework changes (React to Vue, etc.)
- State management library changes
- Routing strategy changes
- Build tool modifications
- Frontend performance architecture changes
- Authentication flow changes
**Key Artifacts**: Frontend architecture, framework choices, state management

**Entry Point:** Frontend Architecture
**Record in:** `workspace/output/frontend/preferences.md`
**Start update from:** `prompts/frontend/prompt.md`

#### Level 9: UI/UX Changes
**Phase Overview Reference**: See `ui_overview.md` for what this phase handles
**Indicators:**
- New UI components
- Component design changes
- Layout modifications
- Design token updates
- Interaction pattern changes
- Accessibility improvements
- Responsive design changes
**Key Artifacts**: UI specifications, component designs, layouts

**Entry Point:** UI Specifications
**Record in:** `workspace/output/frontend/ui/preferences.md`
**Start update from:** `prompts/ui/prompt.md`

#### Level 10: Frontend Code-Only Changes
**Phase Overview Reference**: See `frontend_development_overview.md` for what this phase handles
**Indicators:**
- Frontend bug fixes
- Component refactoring
- Frontend performance optimizations
- CSS/styling improvements
- Frontend error handling improvements
- **Frontend security fixes** (XSS, CSRF, file access, source exposure)
**Key Artifacts**: Frontend code implementation

**Entry Point:** Frontend Development
**Record in:** `workspace/code/frontend/preferences.md`
**Start update from:** `prompts/frontend-dev/prompt.md`

#### Level 11: Integration/Configuration Changes
**Phase Overview Reference**: See `integration_overview.md` for what this phase handles
**Indicators:**
- Docker configuration updates
- Environment variable changes
- Port allocation modifications
- Service startup order changes
- Health check adjustments
- **Security configuration** (CORS, CSP, rate limiting)
**Key Artifacts**: Docker Compose, environment config, integration setup

**Entry Point:** Integration
**Record in:** `workspace/code/integration/preferences.md`
**Start update from:** `prompts/integration/prompt.md`

### Step 4: Record the Modification as a Directive

In the appropriate preferences.md file, add or update a directive.

**For phases with single preference files (API, Services, Development):**
When multiple services/APIs share a preference file, use service-specific labeling:

```markdown
## Modification Directives

### Directive [number]: [Service/API Label] - [Brief Title]
**Service/API**: [trading|accounts|gateway|etc.]
**Type**: Modification
**Current State**: [What the system should be/do NOW]
**Previous State**: [What it was before - optional, only if replacing]
**Context**: [Why this change was requested]
**Impact**: [What parts of the system are affected]
**Date**: [YYYY-MM-DD]
```

**Examples of Service Labeling:**
- In `workspace/output/api/preferences.md`:
  - `### Directive 5: [trading-public] - Add WebSocket Support`
  - `### Directive 6: [accounts-internal] - New Authentication Method`
- In `workspace/output/services/preferences.md`:
  - `### Directive 3: [trading] - Switch to Event-Driven Architecture`
  - `### Directive 4: [gateway] - Add Rate Limiting Module`
- In `workspace/code/preferences.md`:
  - `### Directive 2: [trading] - Use Async Processing`
  - `### Directive 3: [accounts] - Implement Caching Layer`

**Important Rules:**
- Use consistent service naming (lowercase, single word)
- For APIs, include type: `[service-public]` or `[service-internal]`
- If a directive conflicts with a previous one for the SAME service, REPLACE it
- Directives for different services can coexist in the same file
- Always describe the CURRENT desired state, not the change
- Be specific and actionable
- Don't accumulate history - only current state matters

### Step 5: Present the Modification Plan

Present the analysis to the user:

```markdown
# Modification Analysis

## Request Summary
[User's modification request]

## Classification
- **Level**: [1-11 with description]
- **Entry Point**: [Step name]
- **Affected Components**: [List of affected parts]

## Directive to be Recorded
[Show the exact directive that will be added]

## Update Cascade Plan
Starting from: [Entry point]
Will update: [List of steps that need updating]

## Impact Assessment
- **Estimated Scope**: [Small/Medium/Large]
- **Breaking Changes**: [Yes/No - explain if yes]
- **Services Affected**: [List services]

Proceed with this modification plan? (yes/no/modify)
```

### Step 6: Record Directive and Return Classification

Once approved:

1. **Record the directive** in the appropriate preferences.md file
2. **Create a classification result** to return to start.md:

```markdown
# Modification Classification Complete

## Classification Result
- **Level**: [1-11]
- **Entry Point**: [requirements|domain|stories|architecture|api|services|backend-dev|frontend-arch|ui|frontend-dev|integration]
- **Start From**: [Specific prompt path]
- **Directive Location**: [Path to preferences file where directive was recorded]
- **Cascade Required**: [List of steps needing update]

## Summary
The modification has been classified as a Level [N] change requiring updates starting from [step].
The directive has been recorded in [preferences file].

Please proceed with the update cascade starting from [entry point].
```

3. **Return control to start.md** with the classification information

### Step 7: Let start.md Handle Orchestration

start.md will:
1. Receive the classification result
2. Start the update cascade from the identified entry point
3. Continue through subsequent steps as needed
4. Monitor progress and handle completion

## Decision Tree for Complex Cases

### Multiple Level Modifications
If a modification spans multiple levels:
- Start at the HIGHEST level (closest to requirements)
- Let changes cascade naturally
- Document cross-level impacts

### Conflicting Directives
If a new directive conflicts with existing ones:
- Identify all conflicts explicitly
- Ask user for resolution
- Update all affected directives atomically

### Service-Specific vs System-Wide
- If change affects ONE backend service → start at service level
- If change affects MULTIPLE services → start at architecture level
- If change affects BUSINESS LOGIC → start at requirements level
- If change affects FRONTEND ONLY → start at appropriate frontend level
- If change affects BOTH frontend and backend → start at API level or higher

## Error Handling

### Validation Failures
- If modification would break system invariants
- If modification conflicts with hard constraints
- If modification is technically impossible
→ Explain why and suggest alternatives

### Cascade Failures
- If an update step fails
- Note the failure point
- Ask whether to rollback or fix and continue
- Provide clear recovery options

## Examples

### Example 1: Add Email Notifications
**Request**: "Add email notifications when tasks are completed"
**Analysis**: New feature affecting business requirements
**Level**: 1 (Requirements)
**Cascade**: Requirements → Domain → Stories → Architecture → API → Service → Development

### Example 2: Change Database from PostgreSQL to MongoDB
**Request**: "Use MongoDB instead of PostgreSQL for the user service"
**Analysis**: Technology change within a service
**Level**: 6 (Service Implementation)
**Cascade**: Service → Development

### Example 3: Split Monolithic Service
**Request**: "Split the trading service into separate order and execution services"
**Analysis**: Architecture change
**Level**: 4 (Architecture)
**Cascade**: Architecture → API → Service → Development

### Example 4: Change from React to Vue
**Request**: "Migrate the frontend from React to Vue.js"
**Analysis**: Frontend framework change
**Level**: 8 (Frontend Architecture)
**Cascade**: Frontend Architecture → UI Specifications → Frontend Development

### Example 5: Add Dark Mode
**Request**: "Add dark mode support to the application"
**Analysis**: UI/UX feature addition
**Level**: 9 (UI Specifications)
**Cascade**: UI Specifications → Frontend Development

### Example 6: Security Vulnerability - File Access
**Request**: "Fix security issue: users can access any file via crafted URL"
**Analysis**: Frontend security vulnerability
**Level**: 10 (Frontend Development)
**Cascade**: Frontend Development only

### Example 7: Security Vulnerability - SQL Injection
**Request**: "Fix SQL injection vulnerability in user search"
**Analysis**: Backend security issue
**Level**: 7 (Backend Development)
**Cascade**: Backend Development only

### Example 8: Security Configuration
**Request**: "Implement proper CORS and CSP headers"
**Analysis**: Integration/configuration security
**Level**: 11 (Integration)
**Cascade**: Integration only

## Quality Checks

Before recording any directive:
- [ ] Is this a modification (not a bug fix)?
- [ ] Is the current state clearly described?
- [ ] Are conflicts with existing directives resolved?
- [ ] Is the entry point correctly identified?
- [ ] Is the cascade path complete?

## Custom Roles

- Stay in `roo-arch` mode throughout the routing process
- Classify the modification and record directives
- Return classification result to start.md
- Let start.md handle the actual cascade orchestration
- Do NOT create update tasks directly - return control to start.md