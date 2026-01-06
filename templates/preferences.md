# Preferences Document Template

This template should be used for all preferences.md files across the platform development workflow.

## Structure

```markdown
# [Step Name] Preferences

## Overview
This document tracks all user directives, decisions, and clarifications that affect [step name].
**Important**: This document represents the CURRENT desired state, not a history of changes.

## Mode History
- [Date]: [Mode] - [Summary of actions taken]

## Modification Directives
This section contains directives that represent the current desired state after modifications.
Each directive REPLACES any conflicting previous directive - we only keep the current state.

### Directive [number]: [Brief Title]
**Type**: Modification
**Current State**: [What the system should be/do NOW - complete description]
**Context**: [Why this was requested - brief]
**Impact**: [What components/features are affected]
**Date**: [YYYY-MM-DD]

## User Input Log

### Entry [number]: [Topic]
**Type**: Question/Answer OR Directive OR Modification
**Question**: [If Q&A: The question asked by AI]
**Final User Decision**: [The final choice/preference user settled on after discussion]
**Context**: [Why this was asked or what prompted this]
**Impact**: [How this affects the output]
**Date**: [YYYY-MM-DD]

**Note**: Record only the final settled decision, not every back-and-forth exchange during the discussion.

## Decision Categories

### [Category Name]
**Decision**: [The specific decision made]
**Rationale**: [Why this approach was chosen]
**Alternatives Considered**: [Other options discussed]
**Trade-offs**: [Pros and cons acknowledged]
**Related Entries**: [Entry numbers that influenced this decision]

## Step-Specific Sections
[Add sections specific to each step as needed]
```

## Usage Guidelines

### CRITICAL RULES FOR PREFERENCES:

**ONLY record these in preferences.md:**
1. **Questions you explicitly ask the user** and their answers
2. **Direct commands or preferences** the user provides without being asked

### Entry Types
- **Question/Answer**: When AI asks a question and user settles on a final decision (after potential back-and-forth discussion)
- **Directive**: When user provides unprompted guidance or commands
- **Modification**: When user requests changes to existing system (recorded as current state directives)

### Important: Record Current State, Not History
- Record the **current desired state** of the system
- When modifications conflict with previous directives, **replace the old directive**
- Do NOT accumulate history of changes - only what the system should be NOW
- Record only the **final settled preference/choice** that the user decided on
- Do NOT log every single exchange in a back-and-forth conversation
- If a discussion happens about a topic, summarize the final outcome as the user's decision
- The goal is to capture the current system state and user preferences, not conversation transcripts

### Handling Modification Directives
When recording modifications:
1. **State, Not Change**: Describe what the system should be, not what changed
   - ❌ Wrong: "Changed button from blue to green"
   - ✅ Right: "Primary buttons should be green"
2. **Replace Conflicts**: If new directive conflicts with old, replace the old entirely
3. **Be Complete**: Describe the full current state, not just the delta
4. **Clear Impact**: Document what parts of the system are affected

### Categories by Step

#### Requirements Step
- Scope Decisions
- Feature Priorities
- Business Rules
- Technical Constraints

#### Domain Modeling Step
- Entity Boundaries
- Domain Groupings
- Data Ownership Strategy
- Consistency Patterns

#### User Stories Step
- User Type Definitions
- Platform Hint Strategy
- Coverage Strategy
- Story Priorities

#### Architecture Step
- Service Boundaries
- Communication Patterns
- Data Strategy
- Technology Preferences

#### API Specifications Step
- Endpoint Design Patterns
- Data Model Strategy
- Error Handling
- Authentication Methods

#### Service Components Step
- Module Structure
- File Ownership
- Technology Choices
- Implementation Guidelines

### Best Practices
1. Always capture verbatim user input
2. Document context to understand future decisions
3. Link related entries for traceability
4. Group similar decisions into categories
5. Track mode history for audit trail
6. **For modifications**: Replace conflicting directives, don't accumulate history
7. **Current state focus**: Always describe what the system should be NOW
8. **Clear directives**: Make directives actionable and specific