# UI Specifications Output Guidelines

## UI Design Philosophy

### Component-Driven Design
- Build UI from reusable, composable components
- Follow atomic design principles (atoms → molecules → organisms)
- Ensure consistency across all components
- Design for reusability and maintainability

### User-Centered Approach
- Every component serves user needs from stories
- Prioritize usability over aesthetics
- Consider all user types and abilities
- Design for the least capable device first

### Design System Integration
- Establish consistent visual language
- Use design tokens for theming
- Maintain pattern library
- Document usage guidelines

## Component Specification Standards

### Required Sections for Each Component

#### 1. Purpose
- Clear, concise description (1-2 sentences)
- Primary use case
- Value proposition

#### 2. Visual Design
```markdown
## Visual Design

### Appearance
[Describe the component's visual appearance in detail]

### Variants
- **Primary**: [Most common usage]
- **Secondary**: [Alternative style]
- **Success**: [Positive actions/feedback]
- **Danger**: [Destructive actions/warnings]
- **[Custom]**: [Specific to application needs]

### States
- **Default**: Base appearance
- **Hover**: Mouse over state
- **Focus**: Keyboard focus state
- **Active**: Being interacted with
- **Disabled**: Not interactive
- **Loading**: Async operation in progress
- **Error**: Validation or error state
```

#### 3. Anatomy
Break down component structure:
```markdown
## Anatomy
Button Component:
├── Container (button element)
├── Icon (optional leading/trailing)
├── Label (text content)
└── Spinner (loading state)
```

#### 4. Props/Attributes
```markdown
## Props/Attributes
| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| variant | string | No | "primary" | Visual variant |
| size | string | No | "medium" | Component size |
| disabled | boolean | No | false | Disabled state |
| loading | boolean | No | false | Loading state |
| onClick | function | No | - | Click handler |
```

#### 5. Behavior
```markdown
## Behavior

### Interactions
- **Click/Tap**: [Action triggered]
- **Keyboard**: 
  - Enter/Space: Activate
  - Tab: Focus navigation
- **Touch**: [Mobile-specific behavior]

### Animations
- **Entry**: Fade in (200ms ease-out)
- **State Change**: Color transition (150ms)
- **Loading**: Spinner rotation (1s linear infinite)
```

#### 6. Responsive Behavior
```markdown
## Responsive Behavior

### Mobile (320px - 767px)
- Full width in containers
- Larger touch targets (min 44px)
- Stacked layouts

### Tablet (768px - 1023px)
- Flexible widths
- Standard touch targets

### Desktop (1024px+)
- Fixed or auto widths
- Mouse-optimized targets
```

#### 7. Accessibility
```markdown
## Accessibility

### ARIA Requirements
- `role="button"` (if not button element)
- `aria-label` (if no visible text)
- `aria-pressed` (for toggle buttons)
- `aria-disabled` (when disabled)
- `aria-busy` (when loading)

### Keyboard Navigation
- Focusable via Tab key
- Activatable via Enter/Space
- Focus visible indicator

### Screen Reader
- Announces label and state
- State changes announced
- Loading state communicated
```

#### 8. Usage Guidelines
```markdown
## Usage Guidelines

### Do's
- Use primary variant for main actions
- Provide clear, action-oriented labels
- Include loading states for async operations
- Ensure sufficient color contrast

### Don'ts
- Don't use more than one primary button per section
- Avoid vague labels like "Click here"
- Don't disable without explanation
- Avoid using color alone to convey meaning
```

#### 9. Code Examples
```markdown
## Code Example
```jsx
// React Example
<Button
  variant="primary"
  size="large"
  loading={isSubmitting}
  onClick={handleSubmit}
>
  Submit Form
</Button>

// Vue Example
<base-button
  variant="primary"
  size="large"
  :loading="isSubmitting"
  @click="handleSubmit"
>
  Submit Form
</base-button>
```
```

#### 10. Related Components
```markdown
## Related Components
- **LinkButton**: For navigation actions
- **IconButton**: For icon-only actions
- **ButtonGroup**: For related actions
- **DropdownButton**: For action menus
```

## Component Set Organization

### Design Tokens (`design_tokens/`)
Foundation for all components:
```markdown
# Design Tokens

## Colors
### Brand Colors
- Primary: #0066CC
- Secondary: #6C757D
- Success: #28A745
- Danger: #DC3545
- Warning: #FFC107
- Info: #17A2B8

### Neutral Colors
- Gray-900: #212529
- Gray-800: #343A40
[...]

## Typography
### Font Families
- Heading: 'Inter', sans-serif
- Body: 'Inter', sans-serif
- Code: 'Fira Code', monospace

### Font Sizes
- xs: 0.75rem (12px)
- sm: 0.875rem (14px)
- base: 1rem (16px)
[...]

## Spacing
### Scale
- 0: 0
- 1: 0.25rem (4px)
- 2: 0.5rem (8px)
[...]

## Shadows
- sm: 0 1px 2px rgba(0,0,0,0.05)
- md: 0 4px 6px rgba(0,0,0,0.1)
[...]
```

### Core Components (`core_components/`)
Fundamental building blocks:
- Button
- Input
- Select
- Checkbox
- Radio
- Switch
- Card
- Badge
- Avatar
- Icon

### Layout Components (`layout_components/`)
Application structure:
- Container
- Grid
- Header
- Footer
- Sidebar
- Main
- Section
- Divider

### Navigation Components (`navigation_components/`)
User navigation:
- Navbar
- Tabs
- Breadcrumb
- Pagination
- Menu
- Dropdown
- Steps

### Form Components (`form_components/`)
Data input and validation:
- FormField
- FormGroup
- InputGroup
- FieldError
- FieldHelp
- FormActions

### Data Display (`data_display/`)
Information presentation:
- Table
- List
- Grid
- Card
- Accordion
- Tree
- Timeline
- Chart

### Feedback Components (`feedback_components/`)
User feedback and states:
- Alert
- Toast
- Modal
- Drawer
- Popover
- Tooltip
- Progress
- Spinner
- Skeleton

### Feature Components (`feature_components/`)
Business-specific components mapped from user stories

## Quality Checklist

Before finalizing UI specifications:
- [ ] All user stories have UI coverage
- [ ] Components follow atomic design principles
- [ ] Visual design is consistent
- [ ] All states are documented
- [ ] Responsive behavior defined
- [ ] Accessibility requirements met
- [ ] Keyboard navigation specified
- [ ] ARIA attributes documented
- [ ] Usage guidelines clear
- [ ] Code examples provided
- [ ] Related components linked
- [ ] Design tokens comprehensive

## Specification Completeness

### Minimum Requirements
Each component must have:
1. Purpose statement
2. Visual design with variants
3. All interactive states
4. Props/attributes table
5. Accessibility requirements
6. Usage guidelines

### Recommended Additions
- Detailed anatomy breakdown
- Animation specifications
- Multiple code examples
- Design rationale
- Performance considerations
- Testing guidelines

## Update Guidelines

When updating existing UI specifications:
- Preserve working patterns
- Document design changes
- Ensure backward compatibility
- Update all affected components
- Maintain consistency across set
- Update preferences with decisions

## Design Token Management

### Token Categories
- **Colors**: Brand, semantic, neutral
- **Typography**: Families, sizes, weights, line-heights
- **Spacing**: Consistent scale
- **Shadows**: Elevation system
- **Borders**: Widths, styles, radii
- **Breakpoints**: Responsive thresholds
- **Animations**: Durations, easings
- **Z-index**: Layering scale

### Token Naming Convention
```
--{category}-{property}-{variant}-{state}

Examples:
--color-primary-500
--spacing-md
--font-size-lg
--shadow-sm
--radius-lg
```

## Implementation Notes

### Framework Agnostic
- Specifications should work with any framework
- Provide examples for chosen framework
- Use semantic HTML as base
- Document behavior, not implementation

### Progressive Enhancement
- Start with semantic HTML
- Layer on styling
- Add interactivity
- Enhance with ARIA

### Performance Considerations
- Specify lazy loading needs
- Document animation performance
- Consider bundle size impact
- Plan for code splitting