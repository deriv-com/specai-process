# Service-Specific Labeling Guidelines

## Overview

With the new preference structure where multiple services/APIs share single preference files, proper labeling is essential for clarity and maintainability. This document provides comprehensive guidelines for labeling directives in shared preference files.

## File Structure and Locations

| Phase | Preference File | Scope |
|-------|----------------|-------|
| Requirements | `workspace/output/requirements/preferences.md` | System-wide |
| Domain | `workspace/output/domain/preferences.md` | System-wide |
| Stories | `workspace/output/stories/preferences.md` | System-wide |
| Architecture | `workspace/output/architecture/preferences.md` | System-wide |
| **API** | `workspace/output/api/preferences.md` | **All services' APIs** |
| **Services** | `workspace/output/services/preferences.md` | **All service specs** |
| **Development** | `workspace/code/preferences.md` | **All service implementations** |
| Frontend Architecture | `workspace/output/frontend/preferences.md` | Frontend-wide |
| UI | `workspace/output/frontend/ui/preferences.md` | All UI components |
| Frontend Dev | `workspace/code/frontend/preferences.md` | Frontend implementation |

## Labeling Convention

### For Shared Preference Files (API, Services, Development)

#### API Preferences (`workspace/output/api/preferences.md`)

**Format**: `[service-type]`
- `service`: Clean, lowercase service name
- `type`: Either `public` or `internal`

**Examples**:
```markdown
### Directive 1: [trading-public] - Add Real-time Quotes
### Directive 2: [trading-internal] - New Event Format
### Directive 3: [accounts-public] - OAuth Integration
### Directive 4: [gateway-public] - WebSocket Support
### Directive 5: [analytics-internal] - Batch Processing API
```

#### Service Specifications (`workspace/output/services/preferences.md`)

**Format**: `[service]`
- Use clean, lowercase service name only

**Examples**:
```markdown
### Directive 1: [trading] - Event-Driven Architecture
### Directive 2: [accounts] - MongoDB Migration
### Directive 3: [gateway] - Rate Limiting Module
### Directive 4: [analytics] - Spark Integration
```

#### Development (`workspace/code/preferences.md`)

**Format**: `[service]`
- Use clean, lowercase service name only

**Examples**:
```markdown
### Directive 1: [trading] - Async Processing
### Directive 2: [accounts] - Redis Caching
### Directive 3: [gateway] - Circuit Breaker Pattern
### Directive 4: [analytics] - Memory Optimization
```

## Rules for Managing Directives

### 1. Service Name Consistency
- Always use the same service name across all files
- Service names should be:
  - Lowercase
  - Single word (no hyphens or underscores)
  - Consistent with architecture documentation

**Good**: `trading`, `accounts`, `gateway`, `analytics`
**Bad**: `Trading`, `trading-service`, `trading_svc`, `TRD`

### 2. Directive Replacement Rules

When adding a new directive that conflicts with an existing one:

#### Same Service - Replace
```markdown
# Before
### Directive 1: [trading] - Use PostgreSQL
### Directive 2: [accounts] - Use MongoDB

# After (trading service changes to MongoDB)
### Directive 1: [trading] - Use MongoDB  # REPLACED
### Directive 2: [accounts] - Use MongoDB  # UNCHANGED
```

#### Different Services - Coexist
```markdown
# Multiple services can have different approaches
### Directive 1: [trading] - Event-Driven Architecture
### Directive 2: [accounts] - RESTful Architecture
### Directive 3: [gateway] - GraphQL Federation
```

### 3. Organizing Directives

Group directives by service for better readability:

```markdown
## Modification Directives

### Trading Service Directives
### Directive 1: [trading] - High-Performance Requirements
### Directive 2: [trading] - Real-time Processing
### Directive 3: [trading] - Event Sourcing

### Accounts Service Directives  
### Directive 4: [accounts] - GDPR Compliance
### Directive 5: [accounts] - Multi-tenancy Support

### Gateway Service Directives
### Directive 6: [gateway] - API Rate Limiting
### Directive 7: [gateway] - Request Validation
```

### 4. Cross-Service Directives

For directives that affect multiple services, create separate entries:

```markdown
# System-wide audit logging requirement
### Directive 10: [trading] - Implement Audit Logging
**Service/API**: trading
**Type**: Modification
**Current State**: Comprehensive audit logging for all operations
**Context**: Compliance requirement
**Impact**: All endpoints and state changes
**Date**: 2024-01-16

### Directive 11: [accounts] - Implement Audit Logging
**Service/API**: accounts
**Type**: Modification
**Current State**: Comprehensive audit logging for all operations
**Context**: Compliance requirement
**Impact**: All endpoints and state changes
**Date**: 2024-01-16
```

## Search and Update Patterns

### Finding Service-Specific Directives

When updating directives for a specific service:

1. **Search for existing directives**:
   - Look for `[service]` or `[service-type]` patterns
   - Check all directives with matching service label

2. **Identify conflicts**:
   - Only directives with the same service label can conflict
   - Different services' directives are independent

3. **Update or add**:
   - Replace conflicting directives for the same service
   - Add new directives with proper labeling
   - Preserve directives for other services

### Example Update Workflow

**Scenario**: Updating the trading service to use MongoDB

1. **Search** in `workspace/output/services/preferences.md`:
   ```
   Find: [trading]
   ```

2. **Found**:
   ```markdown
   ### Directive 3: [trading] - Use PostgreSQL
   ```

3. **Replace with**:
   ```markdown
   ### Directive 3: [trading] - Use MongoDB
   **Service/API**: trading
   **Type**: Modification
   **Current State**: Trading service uses MongoDB for high-performance document storage
   **Context**: Performance optimization for market data
   **Impact**: Data access layer, query patterns, indexes
   **Date**: 2024-01-20
   ```

## Special Cases

### 1. Service Renames
If a service is renamed:
- Update all directives with the old service name
- Use the new name consistently
- Document the rename in architecture preferences

### 2. Service Splits
When splitting a service:
- Create new directives for each resulting service
- Mark old service directives as superseded
- Reference the split in the directive context

### 3. Service Merges
When merging services:
- Combine relevant directives under the new service name
- Remove redundant directives
- Document the merge context

## Validation Checklist

Before saving any preference file:

- [ ] Service names are consistent and lowercase
- [ ] Labels follow the correct format for the file type
- [ ] Conflicting directives for the same service are replaced
- [ ] Different services' directives are preserved
- [ ] Cross-references use the same service names
- [ ] Dates are current
- [ ] Context clearly explains the modification

## Quick Reference

| File | Label Format | Example |
|------|-------------|---------|
| `api/preferences.md` | `[service-type]` | `[trading-public]` |
| `services/preferences.md` | `[service]` | `[trading]` |
| `code/preferences.md` | `[service]` | `[trading]` |

## Common Mistakes to Avoid

1. ❌ Using service IDs instead of names: `[SVC-TR-001]`
2. ❌ Inconsistent casing: `[Trading]` vs `[trading]`
3. ❌ Missing type for APIs: `[trading]` instead of `[trading-public]`
4. ❌ Removing other services' directives when updating
5. ❌ Not replacing conflicting directives for the same service
6. ❌ Using underscores or hyphens in service names: `[trading_service]`

## Benefits of This Approach

1. **Clear Ownership**: Easy to identify which service a directive affects
2. **Conflict Prevention**: Different services can have different approaches
3. **Easy Searching**: Can quickly find all directives for a service
4. **Maintainability**: Reduced file count while maintaining clarity
5. **Consistency**: Same labeling pattern across related phases