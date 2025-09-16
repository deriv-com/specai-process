# User Stories Output Guidelines

## User Story Standards

### Story Format
- Use standard format: "As a [user type], I want to [action] so that [benefit]"
- Keep stories concise - single line format
- Focus on WHAT users need, not HOW it will be implemented
- Each story should represent one atomic user need

### Story ID Convention
- Format: `US-[SERVICE]-[3CHAR]` where:
  - SERVICE: Two-letter code derived from the story's primary domain
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
- Examples: US-AC-K3M (accounts), US-MK-P7R (market data)
- IDs must be unique and stable (don't change existing IDs during updates)

### Service Hint Mapping
- Add a service hint in parentheses after each story
- This helps guide service definition without being prescriptive
- Example: "(accounts)" for user management stories

## User Types Identification

### User Type Criteria
- Extract ALL distinct user types from the product specifications
- Consider both direct users (end-users) and indirect users (administrators, operators)
- Include system-to-system interactions if applicable
- User types should be clearly distinguishable by their goals and permissions

### User Type Documentation
- **User Type Name**: Clear, descriptive name
- **Description**: Role and primary goals (2-3 sentences)
- **Key Characteristics**: What distinguishes this user type
- **Access Level**: General permission scope

## Document Structure

### Executive Summary
Brief overview of the system's user base and primary interaction patterns.

### User Types Section
Comprehensive list of all identified user types with:
- User Type Name
- Description (role and primary goals)
- Key Characteristics
- Access Level

### User Stories by Type
For each user type, list all stories:
- Group stories by user type
- Within each group, organize by functional area
- Format: `[Story ID] As a [user type], I want to [action] so that [benefit] (service hint)`

### Cross-User Type Stories
Stories that involve multiple user types interacting:
- Collaboration scenarios
- Approval workflows
- Data sharing requirements

### Story Coverage Matrix
Map stories back to PRD requirements:
| PRD Section/Feature | Related Story IDs | User Types Involved |
|---------------------|-------------------|---------------------|

### Service Distribution Summary
Early indication of how stories might group into services:
- List service hints with story count
- Identify potential service boundaries
- Note cross-service story patterns

## Coverage Requirements

### Story Completeness
- Ensure all features from the PRD have corresponding stories
- Include edge cases and administrative functions
- Cover the full user journey from onboarding to advanced usage

### User Journey Coverage
- Onboarding process
- Core functionality usage
- Advanced features
- Administrative tasks
- Error handling scenarios
- System maintenance

## Quality Checklist

Before finalizing user stories:
- [ ] All user types from PRD are identified
- [ ] Each user type has clear description and characteristics
- [ ] All PRD features have corresponding user stories
- [ ] Stories follow standard format
- [ ] Story IDs are unique and properly formatted
- [ ] Service hints are logical and distributed
- [ ] Cross-user interactions are captured
- [ ] Story Coverage Matrix is complete
- [ ] Edge cases are included
- [ ] Administrative functions are covered

## Update Guidelines

When updating existing user stories:
- Preserve existing story IDs to maintain traceability
- Add new stories for new requirements
- Mark deprecated stories rather than deleting them
- Update story text if requirements have changed significantly
- Add changelog section documenting what was added/modified/deprecated
- Maintain existing document structure