# UI Specifications Verification

## Goal
Verify that UI component specifications are complete, consistent, and align with frontend architecture, user stories, and accessibility standards.

## Process

### Step 1: Read Required Documents
1. **UI Specifications**: `workspace/output/frontend/ui/{component_set}/`
2. **UI Preferences**: `workspace/output/frontend/ui/preferences.md`
3. **Frontend Architecture**: `workspace/output/frontend/architecture.md`
4. **User Stories**: `workspace/output/stories/stories.md`
5. **PRD**: `workspace/output/requirements/prd.md`

### Step 2: Verify Completeness

#### Component Coverage Check
Based on component set type, verify:

**Design Tokens**:
- [ ] Color palette defined
- [ ] Typography scale complete
- [ ] Spacing system documented
- [ ] Shadow definitions present
- [ ] Border radius tokens defined

**Core Components**:
- [ ] Buttons specified
- [ ] Form inputs documented
- [ ] Cards defined
- [ ] Badges/tags specified
- [ ] All variants documented

**Layout Components**:
- [ ] Header specification
- [ ] Footer specification
- [ ] Sidebar (if needed)
- [ ] Container/grid system
- [ ] Responsive behavior

**Navigation Components**:
- [ ] Main navigation
- [ ] Breadcrumbs (if needed)
- [ ] Tabs (if needed)
- [ ] Pagination (if needed)

**Form Components**:
- [ ] Field groups
- [ ] Validation displays
- [ ] Form layouts
- [ ] Field helpers

**Data Display**:
- [ ] Tables (if needed)
- [ ] Lists
- [ ] Cards/grids
- [ ] Charts (if needed)

**Feedback Components**:
- [ ] Alerts
- [ ] Toasts/notifications
- [ ] Modals
- [ ] Loading states

#### Required Sections Check
For each component, verify presence of:
- [ ] Purpose statement
- [ ] Visual design with variants
- [ ] All interactive states (default, hover, focus, active, disabled, loading, error)
- [ ] Props/attributes table
- [ ] Behavior documentation
- [ ] Responsive specifications
- [ ] Accessibility requirements
- [ ] Usage guidelines
- [ ] Code examples
- [ ] Related components

### Step 3: Verify Alignment

#### Architecture Alignment
- Technology stack matches frontend architecture
- Component examples use chosen framework
- Patterns align with architectural decisions
- State management approach consistent

#### User Story Coverage
For each user story:
- Required UI components identified
- Component specifications support story needs
- Interaction patterns match story requirements
- All user types considered

#### Design Consistency
- Visual language consistent across components
- Naming conventions followed
- Pattern reuse where appropriate
- Design tokens used consistently

### Step 4: Verify Accessibility

#### WCAG Compliance
- [ ] Color contrast ratios meet WCAG AA (4.5:1 for normal text, 3:1 for large text)
- [ ] Focus indicators visible
- [ ] Interactive elements minimum 44x44px on mobile
- [ ] Text alternatives for non-text content

#### Keyboard Navigation
- [ ] All interactive components keyboard accessible
- [ ] Tab order logical
- [ ] Focus trap handling for modals
- [ ] Escape key behavior documented

#### ARIA Implementation
- [ ] Appropriate ARIA roles specified
- [ ] ARIA labels for icon-only elements
- [ ] Live regions for dynamic content
- [ ] Landmark roles for layout components

#### Screen Reader Support
- [ ] Semantic HTML emphasized
- [ ] State changes announced
- [ ] Form field associations clear
- [ ] Error messages linked to fields

### Step 5: Verify Best Practices

#### Performance
- [ ] Lazy loading specified where needed
- [ ] Animation performance considered
- [ ] Image optimization mentioned
- [ ] Code splitting opportunities identified

#### Responsive Design
- [ ] Mobile-first approach evident
- [ ] Breakpoints consistently defined
- [ ] Touch targets appropriate for mobile
- [ ] Content reflow handled

#### Maintainability
- [ ] Components properly scoped
- [ ] Reusability emphasized
- [ ] Clear naming conventions
- [ ] Documentation comprehensive

### Step 6: Generate Verification Report

Create report at `workspace/cache/verify_ui_{component_set}.md`:

```markdown
# UI Specifications Verification Report - [Component Set]

## Summary
- **Status**: [PASS/FAIL]
- **Components Verified**: [count]
- **Critical Issues**: [count]
- **Warnings**: [count]
- **Suggestions**: [count]

## Component Coverage
### Required Components
✅/❌ [Component 1]
✅/❌ [Component 2]
[...]

### Missing Components
[List any missing required components]

## Specification Completeness
### [Component Name]
✅/❌ Purpose statement
✅/❌ Visual design
✅/❌ All states documented
✅/❌ Props table
✅/❌ Behavior documentation
✅/❌ Responsive specs
✅/❌ Accessibility requirements
✅/❌ Usage guidelines
✅/❌ Code examples

[Repeat for each component]

## Alignment Verification

### Architecture Alignment
- **Framework Match**: ✅/❌
- **Pattern Consistency**: ✅/❌
- **Issues**: [List any misalignments]

### User Story Coverage
- **Stories Requiring UI**: [count]
- **Stories Covered**: [count]
- **Gaps**: [List uncovered stories]

### Design Consistency
- **Token Usage**: ✅/❌
- **Naming Conventions**: ✅/❌
- **Pattern Reuse**: ✅/❌

## Accessibility Audit

### WCAG Compliance
✅/❌ Color contrast specified
✅/❌ Focus indicators defined
✅/❌ Touch targets appropriate
✅/❌ Text alternatives documented

### Keyboard Navigation
✅/❌ All components keyboard accessible
✅/❌ Tab order defined
✅/❌ Focus management documented

### ARIA Implementation
✅/❌ ARIA roles specified
✅/❌ Labels for icon elements
✅/❌ Live regions identified

## Issues Found

### Critical Issues
[Must be fixed before proceeding]
1. [Issue description]
   - Component: [name]
   - Impact: [explanation]
   - Recommendation: [how to fix]

### Warnings
[Should be addressed but not blocking]
1. [Warning description]
   - Component: [name]
   - Impact: [explanation]
   - Recommendation: [improvement]

### Suggestions
[Nice to have improvements]
1. [Suggestion]
   - Benefit: [explanation]

## Recommendations
[Overall recommendations for the specifications]

## Conclusion
[Summary statement about specification readiness]
```

### Step 7: Determine Pass/Fail

**PASS Criteria**:
- All required components specified
- >90% of sections complete per component
- Accessibility requirements documented
- User story coverage >90%
- No critical issues

**FAIL Criteria**:
- Missing required components
- <90% section completeness
- Accessibility not addressed
- User story coverage <90%
- Critical issues present

## Important Notes
- Focus on specification completeness, not design quality
- Verify consistency across component set
- Ensure accessibility is prioritized
- Check framework alignment
- Validate responsive approach