# Modification Guidelines

## Core Philosophy

Modifications represent **evolution** of the system, not patches or fixes. Each modification moves the system from one valid state to another valid state. We maintain the CURRENT desired state, not a history of changes.

## Modification vs Bug Fix

### Modifications (Handled by this process)
- Adding new features or removing features
- Changing business rules or logic
- Modifying user workflows or permissions
- Altering system architecture or boundaries
- Updating technology choices
- Changing data models or relationships
- Adjusting performance requirements
- Modifying API contracts

### Bug Fixes (NOT handled by this process)
- Code that doesn't work as specified
- Syntax errors or runtime errors
- Logic errors that violate specifications
- Performance issues not meeting stated requirements
- Security vulnerabilities
- Memory leaks or resource issues

**Rule**: If the specification is correct but the code is wrong → Bug fix (just fix the code)
If the specification needs to change → Modification (use this process)

## Directive Recording Principles

### 1. State, Not History
❌ **Wrong**: "Changed button color from blue to green"
✅ **Right**: "Primary action buttons should be green"

❌ **Wrong**: "Added support for Word documents"
✅ **Right**: "System supports PDF and Word document conversion"

### 2. Replace, Don't Accumulate
When a new directive conflicts with an old one:
- Replace the old directive entirely FOR THE SAME SERVICE
- In shared files, only replace directives with matching service labels
- Don't keep both versions of the same directive
- Don't track the change history
- The new directive IS the truth for that service
- Directives for different services can coexist

**Example in shared file:**
```markdown
# Before
### Directive 1: [trading] - Use PostgreSQL
### Directive 2: [accounts] - Use MongoDB

# After modification for trading service
### Directive 1: [trading] - Use MongoDB  # Replaced
### Directive 2: [accounts] - Use MongoDB  # Unchanged
```

### 3. Be Specific and Actionable
❌ **Vague**: "Improve performance"
✅ **Specific**: "API response time should be under 200ms for all endpoints"

❌ **Vague**: "Make it more user-friendly"
✅ **Specific**: "Add tooltips to all form fields explaining expected input format"

## Classification Guidelines

### Determining the Entry Point

Use the **highest applicable level** when a modification could fit multiple levels:

1. **Requirements Level** - Changes WHAT the system does
   - New business capabilities
   - Different user types
   - Changed regulatory requirements
   - Modified success metrics

2. **Domain Level** - Changes the conceptual model
   - New business entities
   - Different relationships
   - Changed data ownership
   - Modified consistency boundaries

3. **Stories Level** - Changes HOW users interact
   - New user workflows
   - Different permissions
   - Changed user journeys
   - Modified interaction patterns

4. **Architecture Level** - Changes system structure
   - Service boundary changes
   - Communication pattern changes
   - Data distribution changes
   - Scalability approach changes

5. **API Level** - Changes external contracts
   - Endpoint modifications
   - Data format changes
   - Authentication changes
   - Rate limit changes

6. **Service Level** - Changes internal design
   - Module reorganization
   - Algorithm changes
   - Technology switches
   - Performance optimizations

7. **Development Level** - Changes implementation only
   - Code refactoring
   - Better error handling
   - Improved logging
   - Code style improvements

### Decision Tree

```
Does it change business rules or features?
  ├─ YES → Requirements Level
  └─ NO → Does it change the data model?
      ├─ YES → Domain Level
      └─ NO → Does it change user interactions?
          ├─ YES → Stories Level
          └─ NO → Does it change service boundaries?
              ├─ YES → Architecture Level
              └─ NO → Does it change external APIs?
                  ├─ YES → API Level
                  └─ NO → Does it change internal design?
                      ├─ YES → Service Level
                      └─ NO → Development Level
```

## Cascade Management

### Update Mode Behavior
When running updates after a modification:
- Updates should be **smart** - only change what's affected
- Preserve unaffected work
- Maintain consistency across all artifacts
- Report what changed and why

### Cascade Optimization
Not every modification needs to cascade through all steps:
- **Requirements change** → Usually cascades through everything
- **API change** → May only affect Service and Development
- **Service implementation change** → May only affect Development
- **Development change** → No cascade needed

### Skip Conditions
A step can be skipped if:
1. The modification doesn't affect that step's domain
2. The existing artifacts remain valid
3. No inconsistencies would be introduced

## Conflict Resolution

### Types of Conflicts

1. **Direct Conflicts** - New directive contradicts old directive
   - Resolution: New directive wins, old is replaced

2. **Indirect Conflicts** - New directive makes other directives invalid
   - Resolution: Identify all affected directives, update or remove them

3. **Constraint Conflicts** - New directive violates system constraints
   - Resolution: Reject modification or negotiate compromise

### Conflict Detection
Check for conflicts at each level:
- Requirements conflicts with regulations or constraints
- Domain conflicts with data integrity rules
- Architecture conflicts with scalability requirements
- API conflicts with backward compatibility
- Service conflicts with technology limitations

## Documentation Standards

### Directive Format

#### For Single-Service Preference Files
```markdown
### Directive N: [Clear Title]
**Type**: Modification
**Current State**: [Complete description of desired state]
**Context**: [Why this was requested - brief]
**Impact**: [What components/features are affected]
**Constraints**: [Any limitations or requirements]
**Date**: [YYYY-MM-DD]
```

#### For Multi-Service Preference Files (API, Services, Development)
```markdown
### Directive N: [Service Label] - [Clear Title]
**Service/API**: [service-name or service-type]
**Type**: Modification
**Current State**: [Complete description of desired state]
**Context**: [Why this was requested - brief]
**Impact**: [What components/features are affected]
**Constraints**: [Any limitations or requirements]
**Date**: [YYYY-MM-DD]
```

### Service Labeling Convention
When multiple services share a preference file:

**API Preferences** (`workspace/output/api/preferences.md`):
- Format: `[service-type]` where type is `public` or `internal`
- Examples: `[trading-public]`, `[accounts-internal]`, `[gateway-public]`

**Service Specifications** (`workspace/output/services/preferences.md`):
- Format: `[service]`
- Examples: `[trading]`, `[accounts]`, `[gateway]`

**Development** (`workspace/code/preferences.md`):
- Format: `[service]`
- Examples: `[trading]`, `[accounts]`, `[gateway]`

### Conflict Resolution in Shared Files
When working with shared preference files:
1. **Search for existing directives** for the specific service first
2. **Replace conflicting directives** only for the same service
3. **Preserve directives** for other services
4. **Maintain clear separation** between service-specific sections

### Modification Report Format
```markdown
# Modification Report: [Title]

## Request
[Original user request]

## Analysis
- Entry Point: [Level and step]
- Scope: [What's affected]
- Complexity: [Simple/Medium/Complex]

## Changes Applied
- [Step 1]: [What was changed]
- [Step 2]: [What was changed]

## Verification
- [ ] All tests passing
- [ ] No regressions introduced
- [ ] Documentation updated
- [ ] Consistency maintained

## Result
[Summary of successful modification]
```

## Best Practices

### DO:
- ✅ Validate modifications before applying
- ✅ Check for ripple effects
- ✅ Maintain system consistency
- ✅ Document the current state clearly
- ✅ Test after each cascade step
- ✅ Report progress to user
- ✅ Handle errors gracefully

### DON'T:
- ❌ Keep historical directives
- ❌ Allow contradictory directives
- ❌ Skip impact analysis
- ❌ Make assumptions about user intent
- ❌ Cascade blindly without checking
- ❌ Mix bug fixes with modifications
- ❌ Ignore validation failures

## Special Cases

### Cross-Cutting Modifications
When a modification affects multiple services:
1. Start at Architecture level
2. Update service boundaries if needed
3. Cascade to affected services
4. Coordinate API changes
5. Ensure consistency across services

### Technology Migrations
When changing technology stack:
1. Document at Service level
2. Update implementation approach
3. Maintain API contracts
4. Ensure no functional regression
5. Update deployment configuration

### Performance Modifications
When changing performance requirements:
1. Update at Requirements level if business-driven
2. Update at Service level if optimization-driven
3. Cascade to Development for implementation
4. Add performance tests
5. Document new benchmarks

## Quality Assurance

### Pre-Modification Checklist
- [ ] Current system state understood
- [ ] Modification clearly defined
- [ ] Entry point correctly identified
- [ ] Impact analysis complete
- [ ] Conflicts identified and resolved
- [ ] User approval obtained

### Post-Modification Checklist
- [ ] All directives updated
- [ ] Cascade completed successfully
- [ ] System remains consistent
- [ ] Tests passing
- [ ] Documentation current
- [ ] User notified of completion

## Error Recovery

### Rollback Strategy
If a modification fails mid-cascade:
1. Identify the failure point
2. Assess whether partial changes are valid
3. Either:
   - Complete the remaining cascade
   - Rollback to previous state
   - Fix and retry from failure point

### Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Conflicting requirements discovered | Resolve with user input |
| Technical impossibility found | Propose alternative approach |
| Cascade breaks consistency | Adjust modification scope |
| Performance degradation | Add optimization requirements |
| API breaking changes | Version the API or negotiate |

## Success Metrics

A successful modification:
- Achieves the requested change
- Maintains system consistency
- Preserves unaffected functionality
- Documents the current state
- Completes without errors
- Satisfies user expectations