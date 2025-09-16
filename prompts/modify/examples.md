# Modification Examples

This document provides concrete examples of how different types of modifications are handled by the Modification Router.

## Example 1: Adding Email Notifications (New Feature)

### User Request
"I want to add email notifications when PDF conversions are completed"

### Router Analysis
- **What's changing**: New feature - email notifications
- **Classification**: Level 1 - Requirements Change
- **Entry Point**: Requirements
- **Cascade Path**: Requirements → Domain → Stories → Architecture → API → Service → Development

### Directive Recording
In `workspace/output/requirements/preferences.md`:
```markdown
### Directive 5: Email Notifications
**Type**: Modification
**Current State**: System sends email notifications to users when PDF conversions complete successfully or fail
**Context**: User requested notification feature for better user experience
**Impact**: Converter service needs email capability, new notification preferences in user settings
**Date**: 2024-01-15
```

### Cascade Execution
1. **Requirements**: Add notification feature to PRD
2. **Domain**: Add NotificationPreference entity if needed
3. **Stories**: Add stories for notification settings and delivery
4. **Architecture**: May need notification service or integrate with existing
5. **API**: Add endpoints for notification preferences
6. **Service**: Update converter service to trigger notifications
7. **Development**: Implement the code changes

---

## Example 2: Changing Database Technology

### User Request
"Change the user service from PostgreSQL to MongoDB"

### Router Analysis
- **What's changing**: Technology stack within a service
- **Classification**: Level 6 - Service Implementation Change
- **Entry Point**: Service Specifications
- **Cascade Path**: Service → Development

### Directive Recording
In `workspace/output/services/preferences.md`:
```markdown
### Directive 3: Database Technology
**Type**: Modification
**Current State**: User service uses MongoDB for data persistence with document-based schema
**Context**: Changed from PostgreSQL for better flexibility with user profile data
**Impact**: Data access layer, migration scripts, query patterns
**Date**: 2024-01-15
```

### Cascade Execution
1. **Service**: Update persistence strategy in service.md
2. **Development**: Refactor data access code, update queries, migrate data

---

## Example 3: Splitting a Monolithic Service

### User Request
"Split the trading service into separate order management and execution services"

### Router Analysis
- **What's changing**: Service boundaries and architecture
- **Classification**: Level 4 - Architecture Change
- **Entry Point**: Architecture
- **Cascade Path**: Architecture → API → Service → Development

### Directive Recording
In `workspace/output/architecture/preferences.md`:
```markdown
### Directive 2: Trading Service Split
**Type**: Modification
**Current State**: Trading functionality is split into two services: order service handles order lifecycle, execution service handles matching and execution
**Context**: Improved scalability and separation of concerns
**Impact**: New service boundaries, updated communication patterns, data ownership changes
**Date**: 2024-01-15
```

### Cascade Execution
1. **Architecture**: Define new service boundaries, update communication matrix
2. **API**: Create APIs for both new services
3. **Service**: Create specifications for both services
4. **Development**: Implement both services, migrate code

---

## Example 4: Changing API Authentication Method

### User Request
"Change the public API from API keys to OAuth 2.0"

### Router Analysis
- **What's changing**: API authentication mechanism
- **Classification**: Level 5 - API Contract Change
- **Entry Point**: API Specifications
- **Cascade Path**: API → Service → Development

### Directive Recording
In `workspace/output/api/preferences.md`:
```markdown
### Directive 1: Authentication Method
**Type**: Modification
**Current State**: Public API uses OAuth 2.0 with JWT tokens for authentication
**Context**: Moved from API keys for better security and standard compliance
**Impact**: All public endpoints, client applications, documentation
**Date**: 2024-01-15
```

### Cascade Execution
1. **API**: Update authentication sections in all public API specs
2. **Service**: Update authentication modules in affected services
3. **Development**: Implement OAuth flow, update middleware

---

## Example 5: Adding New User Role

### User Request
"Add a 'Reviewer' role that can view but not modify documents"

### Router Analysis
- **What's changing**: User types and permissions
- **Classification**: Level 3 - User Interaction Change
- **Entry Point**: User Stories
- **Cascade Path**: Stories → Architecture → API → Service → Development

### Directive Recording
In `workspace/output/stories/preferences.md`:
```markdown
### Directive 4: Reviewer Role
**Type**: Modification
**Current State**: System supports Admin, Editor, Viewer, and Reviewer roles. Reviewer can view documents and add comments but cannot modify content
**Context**: Need for quality review process without edit permissions
**Impact**: Permission system, user stories, API authorization
**Date**: 2024-01-15
```

### Cascade Execution
1. **Stories**: Add reviewer user stories
2. **Architecture**: Update if affects service boundaries
3. **API**: Update authorization logic
4. **Service**: Implement reviewer permissions
5. **Development**: Code the new role logic

---

## Example 6: Performance Requirement Change

### User Request
"API response time must be under 100ms instead of 500ms"

### Router Analysis
- **What's changing**: Non-functional requirement
- **Classification**: Level 1 - Requirements Change
- **Entry Point**: Requirements
- **Cascade Path**: Requirements → Architecture → Service → Development

### Directive Recording
In `workspace/output/requirements/preferences.md`:
```markdown
### Directive 6: API Performance
**Type**: Modification
**Current State**: All API endpoints must respond within 100ms for 95th percentile of requests
**Context**: Improved performance requirements for better user experience
**Impact**: Caching strategy, database optimization, possible architecture changes
**Date**: 2024-01-15
```

### Cascade Execution
1. **Requirements**: Update performance requirements in PRD
2. **Architecture**: May need caching layer or service optimization
3. **Service**: Update performance strategies
4. **Development**: Implement optimizations

---

## Example 7: Adding Data Export Feature

### User Request
"Users should be able to export their data in CSV format"

### Router Analysis
- **What's changing**: New feature for data export
- **Classification**: Level 1 - Requirements Change
- **Entry Point**: Requirements
- **Cascade Path**: Requirements → Domain → Stories → Architecture → API → Service → Development

### Directive Recording
In `workspace/output/requirements/preferences.md`:
```markdown
### Directive 7: Data Export
**Type**: Modification
**Current State**: Users can export their data in CSV, JSON, and XML formats with filtering options
**Context**: Data portability requirement for compliance and user control
**Impact**: New export endpoints, data formatting logic, UI changes
**Date**: 2024-01-15
```

---

## Complex Scenario: Multiple Related Changes

### User Request
"We're expanding to Europe, need GDPR compliance, data residency in EU, and support for multiple currencies"

### Router Analysis
This is a complex modification affecting multiple levels:
1. **GDPR Compliance**: Requirements level (regulatory)
2. **Data Residency**: Architecture level (infrastructure)
3. **Multi-currency**: Domain level (data model) and Requirements level (feature)

### Approach
Start at the HIGHEST level (Requirements) and let changes cascade naturally.

### Directive Recording
In `workspace/output/requirements/preferences.md`:
```markdown
### Directive 8: European Expansion
**Type**: Modification
**Current State**: System supports European operations with GDPR compliance, EU data residency, and multi-currency transactions (EUR, GBP, CHF)
**Context**: Business expansion to European market
**Impact**: Data privacy features, infrastructure changes, currency handling throughout system
**Date**: 2024-01-15
```

### Cascade Execution
1. **Requirements**: Update compliance requirements, add multi-currency feature
2. **Domain**: Add currency to relevant entities
3. **Stories**: Add GDPR-related user stories (consent, deletion, export)
4. **Architecture**: Design for data residency, privacy services
5. **API**: Add GDPR endpoints, currency parameters
6. **Service**: Implement privacy features, currency conversion
7. **Development**: Code all changes

---

## Edge Cases and Special Situations

### Conflicting Directives
**Scenario**: User previously requested "Store all data in US" and now requests "Store EU user data in Europe"

**Resolution**: The new directive replaces the old one:
```markdown
### Directive 9: Data Residency
**Type**: Modification
**Current State**: User data is stored based on user location: US users in US regions, EU users in EU regions
**Context**: Compliance with data residency requirements
**Impact**: Multi-region deployment, data routing logic
**Date**: 2024-01-16
```

### Modification That Becomes Invalid
**Scenario**: User requests "Use technology X" but during implementation, technical limitations are discovered

**Handling**:
1. Stop the cascade at the point of discovery
2. Document the issue
3. Propose alternatives to the user
4. Record the final decision as a new directive

### Cross-Service Modifications
**Scenario**: "Add audit logging to all services"

**Approach**:
1. Start at Architecture level (affects all services)
2. Create a directive for the system-wide change
3. Cascade to each service specification (multiple directives in shared file)
4. Implement in each service

**Example directive in `workspace/output/services/preferences.md`:**
```markdown
### Directive 10: [trading] - Add Audit Logging
**Service/API**: trading
**Type**: Modification
**Current State**: Trading service implements comprehensive audit logging for all state changes
**Context**: Compliance requirement for financial operations
**Impact**: All service endpoints, database schema for audit trail
**Date**: 2024-01-16

### Directive 11: [accounts] - Add Audit Logging
**Service/API**: accounts
**Type**: Modification
**Current State**: Accounts service implements comprehensive audit logging for all state changes
**Context**: Compliance requirement for financial operations
**Impact**: All service endpoints, database schema for audit trail
**Date**: 2024-01-16
```

---

## Key Patterns to Remember

### Pattern 1: Feature Addition
Requirements → Domain (if new entities) → Stories → Architecture (if service changes) → API → Service → Development

### Pattern 2: Technology Change
Service → Development (if internal only)
OR
Architecture → Service → Development (if affects multiple services)

### Pattern 3: API Modification
API → Service → Development

### Pattern 4: Performance/Security Requirements
Requirements → Architecture (if structural changes needed) → Service → Development

### Pattern 5: User Role/Permission Changes
Stories → Architecture (if affects boundaries) → API → Service → Development

---

## Best Practices from Examples

1. **Start High**: When in doubt, start at a higher level and let changes cascade
2. **Replace, Don't Accumulate**: Each directive represents current state
3. **Be Specific**: Directives should be actionable and clear
4. **Document Impact**: Always note what parts of the system are affected
5. **Consider Ripples**: Think about downstream effects before recording directive
6. **Validate Feasibility**: Ensure modifications are technically possible before cascading