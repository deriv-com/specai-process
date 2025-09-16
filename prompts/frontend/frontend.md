# Frontend Architecture Design

## Goal
Design the frontend application architecture based on API specifications and user stories, defining the technology stack, component architecture, state management strategy, and integration patterns that will guide frontend implementation.

## Operational Modes

### Mode Detection
First, check if `workspace/output/frontend/architecture.md` exists:
- **EXISTS**: Enter `update` or `review` mode based on task
- **DOES NOT EXIST**: Enter `new` mode

## Preparation

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: Frontend framework, state management, UI libraries, build tools
   - Persists across project resets
2. **Phase Preferences** (`workspace/output/frontend/preferences.md`):
   - Always check: Contains frontend architecture-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making frontend architecture decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.


### Required Reading
1. **INSTRUCTION FILES**
   - `workspace/output/requirements/prd.md`: Extract complexity score and requirements
   - `workspace/output/stories/stories.md`: Understand user interactions and UI needs
   - `workspace/output/architecture/architecture.md`: Understand service boundaries
   - `prompts/frontend/guideline.md`: Learn output standards

2. **API SPECIFICATIONS**
   - Read all public API specifications from `workspace/output/api/*_public.md`
   - Understand available endpoints and data models

3. **EXISTING WORK** (for update/review modes)
   - `workspace/output/frontend/architecture.md`: Current architecture if exists
   - `workspace/output/frontend/preferences.md`: Previous decisions if exists

## Mode: New

### Step 1: Analyze Requirements
Extract from PRD:
- Complexity score (0-10)
- Performance requirements
- User types and counts
- Platform requirements (web, mobile, desktop)
- Browser support requirements

### Step 2: Framework Selection
Based on complexity score:
- **0-3 (Simple)**: 
  - Vanilla HTML/CSS/JavaScript
  - Or lightweight: Alpine.js, Petite-Vue
  - Single HTML file or minimal structure
  
- **4-7 (Standard)**:
  - React with Create React App or Vite
  - Vue 3 with Vite
  - Component-based architecture
  - Client-side routing
  
- **8-10 (Complex)**:
  - Next.js (React) with SSR/SSG
  - Nuxt 3 (Vue) with SSR/SSG
  - Micro-frontend architecture if needed
  - Advanced performance optimization

### Step 3: Design Component Architecture
Based on user stories and API endpoints:
1. **Layout Components**:
   - Application shell
   - Navigation structure
   - Page layouts

2. **Feature Components**:
   - Map user stories to feature modules
   - Identify shared components
   - Design component hierarchy

3. **UI Components**:
   - Design system components
   - Form controls
   - Data display components

### Step 4: State Management Strategy
Based on complexity:
- **Simple (0-3)**: Local component state only
- **Standard (4-7)**: 
  - React: Context API + useReducer or Zustand
  - Vue: Pinia or Vuex
- **Complex (8-10)**:
  - React: Redux Toolkit or MobX
  - Vue: Pinia with modules
  - Consider state machines (XState)

### Step 5: API Integration Patterns
Design how frontend will consume backend APIs:
1. **API Client Architecture**:
   - SDK generation approach
   - Request/response interceptors
   - Error handling strategy
   
2. **Data Fetching Strategy**:
   - Simple: Fetch API or Axios
   - Standard: React Query or SWR
   - Complex: GraphQL with Apollo

3. **Authentication Flow**:
   - Token management
   - Session handling
   - Protected routes

### Step 6: Routing Architecture
Define navigation structure:
- Route definitions
- Nested routing strategy
- Dynamic routes
- Route guards/protection

### Step 7: Performance Strategy
Based on requirements:
- Code splitting approach
- Lazy loading strategy
- Caching mechanisms
- Bundle optimization

### Step 8: Create Architecture Document
Write `workspace/output/frontend/architecture.md` following the structure in guideline.md

### Step 9: Create Preferences
Document decisions in `workspace/output/frontend/preferences.md`:
```markdown
# Frontend Architecture Preferences

## Framework Choice
- **Selected**: [Framework]
- **Reason**: [Justification based on complexity]

## State Management
- **Solution**: [Chosen approach]
- **Reason**: [Justification]

## Component Library
- **UI Library**: [If using one]
- **Custom Components**: [Yes/No]

## Build Tools
- **Bundler**: [Vite/Webpack/etc]
- **Package Manager**: [npm/yarn/pnpm]

## Testing Strategy
- **Unit Tests**: [Framework]
- **E2E Tests**: [Framework]

## Development Standards
- **Code Style**: [ESLint/Prettier config]
- **Git Workflow**: [Branching strategy]
```

## Mode: Update

### Step 1: Read Current Architecture
- Load `workspace/output/frontend/architecture.md`
- Load `workspace/output/frontend/preferences.md`

### Step 2: Identify Changes
Check for updates in:
- New API endpoints
- Changed user stories
- Modified requirements
- Performance improvements needed

### Step 3: Gap Analysis
Compare current architecture with new requirements:
- Missing components
- Outdated patterns
- New integrations needed
- Performance optimizations

### Step 4: Update Architecture
Modify only what needs to change:
- Preserve working solutions
- Add new components
- Update integration patterns
- Refine state management

### Step 5: Update Documents
- Update `workspace/output/frontend/architecture.md`
- Update `workspace/output/frontend/preferences.md` with changes

## Mode: Review

### Step 1: Load Current State
- Read architecture and preferences
- Understand current decisions

### Step 2: Interactive Review
Engage with user about:
1. **Framework Selection**:
   - Is current framework meeting needs?
   - Any performance issues?
   - Developer experience feedback?

2. **Component Architecture**:
   - Component organization working well?
   - Reusability achieved?
   - Any maintenance issues?

3. **State Management**:
   - Is state management scalable?
   - Any complexity issues?
   - Performance concerns?

4. **API Integration**:
   - Integration patterns working?
   - Error handling adequate?
   - Any reliability issues?

### Step 3: Document Changes
If user wants modifications:
- Update preferences with new decisions
- Regenerate architecture based on changes
- Document reasons for changes

## Output Standards

### Required Sections
Your output must include all sections defined in `prompts/frontend/guideline.md`:
1. Executive Summary
2. Technology Stack
3. Architecture Overview
4. Component Architecture
5. State Management
6. API Integration
7. Routing Structure
8. Authentication & Authorization
9. Performance Strategy
10. Responsive Design
11. Build Configuration
12. Testing Strategy
13. Deployment Architecture
14. Development Guidelines

## Completion

After creating/updating the architecture:
- Verify all required sections are present
- Ensure complexity alignment
- Confirm API integration completeness
- Report: "creation succeeded" or "creation failed" with reason

## Important Notes
- Architecture drives all frontend development
- Framework choice must match complexity
- Consider long-term maintenance
- Plan for scalability from the start
- Include accessibility requirements
- Design for testability