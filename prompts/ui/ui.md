# UI Component Specifications

## Goal
Create comprehensive UI component specifications based on frontend architecture, user stories, and design patterns. Define visual components, layouts, interactions, and user experience guidelines.

## Operational Modes

### Mode Detection
First, check if specifications exist for the component set in `workspace/output/frontend/ui/{component_set}/`:
- **EXISTS**: Enter `update` or `review` mode based on task
- **DOES NOT EXIST**: Enter `new` mode

## Component Sets
Work on one component set at a time:
1. **design_tokens** - Colors, typography, spacing, shadows
2. **core_components** - Buttons, inputs, cards, badges
3. **layout_components** - Headers, footers, sidebars, containers
4. **navigation_components** - Menus, tabs, breadcrumbs, pagination
5. **form_components** - Form controls, validation, field groups
6. **data_display** - Tables, lists, grids, charts
7. **feedback_components** - Alerts, toasts, modals, loading states
8. **feature_components** - Business-specific components

## Preparation

### Required Reading
1. **INSTRUCTION FILES**
   - `workspace/output/frontend/architecture.md`: Technology stack and patterns
   - `workspace/output/stories/stories.md`: User interactions and UI needs
   - `prompts/ui/guideline.md`: Output standards

2. **EXISTING WORK** (for update/review modes)
   - `workspace/output/frontend/ui/{component_set}/`: Current specifications
   - `workspace/output/frontend/ui/preferences.md`: Previous decisions

## Mode: New

### Step 1: Analyze Requirements
Based on component set type:

#### For Design Tokens
Extract from requirements:
- Brand colors if specified
- Typography preferences
- Spacing system needs
- Visual style (modern, classic, minimal)

#### For Core Components
Identify from user stories:
- Button types needed (primary, secondary, danger)
- Input types required (text, select, checkbox)
- Card layouts for content
- Badge/tag requirements

#### For Layout Components
Determine from architecture:
- Application shell structure
- Header requirements (navigation, user info)
- Sidebar needs (if applicable)
- Footer content

#### For Navigation Components
Extract from user stories:
- Main navigation structure
- Sub-navigation needs
- Breadcrumb requirements
- Pagination patterns

#### For Form Components
Identify from user stories:
- Form types in the application
- Validation requirements
- Field grouping needs
- Multi-step forms

#### For Data Display
Determine from API responses:
- Table structures needed
- List layouts required
- Grid displays
- Chart/visualization needs

#### For Feedback Components
Extract from user stories:
- Alert types (success, error, warning, info)
- Modal dialogs needed
- Loading state requirements
- Toast notification needs

### Step 2: Create Component Specifications

For each component in the set, create a specification file:

```markdown
# [Component Name]

## Purpose
[Brief description of component's role]

## Visual Design
### Appearance
[Describe visual appearance]

### Variants
- **Primary**: [Description]
- **Secondary**: [Description]
- **[Other variants]**: [Description]

### States
- **Default**: [Description]
- **Hover**: [Description]
- **Active**: [Description]
- **Disabled**: [Description]
- **Loading**: [Description]
- **Error**: [Description]

## Anatomy
[Component structure breakdown]
```
- [Part 1]: [Description]
- [Part 2]: [Description]

## Props/Attributes
| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| [prop] | [type] | Yes/No | [default] | [description] |

## Behavior
### Interactions
- **Click**: [What happens]
- **Keyboard**: [Keyboard support]
- **Touch**: [Touch behavior]

### Animations
- **Entry**: [Animation description]
- **Exit**: [Animation description]
- **State Change**: [Transitions]

## Responsive Behavior
### Mobile (320px - 767px)
[Mobile-specific behavior]

### Tablet (768px - 1023px)
[Tablet-specific behavior]

### Desktop (1024px+)
[Desktop-specific behavior]

## Accessibility
### ARIA Requirements
- `role`: [ARIA role]
- `aria-label`: [Label requirements]
- Other ARIA attributes

### Keyboard Navigation
- **Tab**: [Tab behavior]
- **Enter/Space**: [Activation]
- **Arrow Keys**: [If applicable]
- **Escape**: [If applicable]

### Screen Reader
[Screen reader considerations]

## Usage Guidelines
### Do's
- [Best practice 1]
- [Best practice 2]

### Don'ts
- [Anti-pattern 1]
- [Anti-pattern 2]

## Code Example
```[language]
// Pseudocode or framework-specific example
<Component
  variant="primary"
  size="medium"
  onClick={handleClick}
>
  Content
</Component>
```

## Related Components
- [Component 1]: [Relationship]
- [Component 2]: [Relationship]
```

### Step 3: Create Component Set Index
Create an index file for the component set:

```markdown
# [Component Set Name]

## Overview
[Description of this component set]

## Components in This Set
1. **[Component 1]** - [Brief description]
2. **[Component 2]** - [Brief description]
3. **[Component 3]** - [Brief description]

## Design Principles
[Principles guiding these components]

## Usage Patterns
[Common patterns for using these components together]

## Implementation Priority
1. [Highest priority component]
2. [Second priority]
3. [Third priority]
```

### Step 4: Update Preferences
Create or update `workspace/output/frontend/ui/preferences.md`:

```markdown
# UI Specification Preferences

## Design System
- **Approach**: [Custom/Existing]
- **If Existing**: [Which one]
- **Customization Level**: [Heavy/Light/None]

## Component Library
- **Build Approach**: [From scratch/Extend existing]
- **Base Library**: [If extending]

## Visual Design
- **Style**: [Modern/Classic/Minimal/Bold]
- **Animations**: [Heavy/Subtle/None]
- **Shadows**: [Yes/No]
- **Rounded Corners**: [Yes/No]

## [Component Set] Decisions
- **Decision 1**: [Rationale]
- **Decision 2**: [Rationale]
```

## Mode: Update

### Step 1: Read Current Specifications
- Load existing component specifications
- Load current preferences

### Step 2: Identify Changes
Check for updates in:
- New user stories requiring UI components
- Changed architecture affecting components
- New features needing components
- Design improvements needed

### Step 3: Gap Analysis
Compare current specs with new requirements:
- Missing components
- Missing states or variants
- Outdated patterns
- Accessibility improvements

### Step 4: Update Specifications
Modify only what needs to change:
- Add new components
- Update existing component specs
- Refine interaction patterns
- Enhance accessibility

### Step 5: Update Documents
- Update component specification files
- Update component set index
- Update preferences with changes

## Mode: Review

### Step 1: Load Current State
- Read all component specifications
- Understand current decisions

### Step 2: Interactive Review
Engage with user about:
1. **Visual Design**:
   - Are components visually appealing?
   - Consistency issues?
   - Brand alignment?

2. **Component Coverage**:
   - Missing components?
   - Unnecessary components?
   - Component complexity appropriate?

3. **Interaction Patterns**:
   - Interactions intuitive?
   - Consistency across components?
   - Mobile experience good?

4. **Accessibility**:
   - Meeting requirements?
   - Keyboard navigation complete?
   - Screen reader friendly?

### Step 3: Document Changes
If user wants modifications:
- Update preferences with new decisions
- Regenerate specifications based on changes
- Document reasons for changes

## Directory Structure

Create this structure for each component set:
```
workspace/output/frontend/ui/
├── design_tokens/
│   ├── colors.md
│   ├── typography.md
│   ├── spacing.md
│   └── index.md
├── core_components/
│   ├── button.md
│   ├── input.md
│   ├── card.md
│   └── index.md
├── [other_component_sets]/
└── preferences.md
```

## Completion

After creating/updating specifications:
- Verify all components in set are specified
- Ensure consistency across components
- Confirm accessibility requirements met
- Report: "creation succeeded" or "creation failed" with reason

## Important Notes
- Follow atomic design principles
- Ensure consistency within and across sets
- Include all interaction states
- Document responsive behavior
- Specify accessibility requirements
- Provide clear usage guidelines