# Requirements Output Guidelines

## Complexity Assessment Standards

### Assessment Process
1. **Analyze the product brief** against five complexity dimensions
2. **Score each dimension** using the defined scale (0-10 total)
3. **Select appropriate template** based on total score
4. **Document assessment** in preferences with justification
5. **Allow user override** if they prefer a different template

### Scoring Guidelines
- Be objective and consistent in scoring
- Consider the full scope described in the brief
- When in doubt, score conservatively (lower)
- Document specific evidence for each score

### Template Selection
- **0-3 points**: Minimal PRD (simple tools, utilities, single-purpose apps)
- **4-7 points**: Standard PRD (business applications, multi-user systems)
- **8-10 points**: Comprehensive PRD (complex systems, regulated systems)

### User Override
- User can request a different template than recommended
- Document the override reason in preferences
- Apply the user-selected template for all work

## Product Requirements Document (PRD) Standards

### Functional Requirements
- Each requirement must have a unique ID: `REQ-[SECTION]-[3CHAR]` where:
  - SECTION: Two-letter code for the PRD section (e.g., AC for Accounts, TR for Trading, MK for Market)
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
  - Examples: REQ-AC-K3M (accounts requirement), REQ-TR-P7R (trading requirement)
- Each requirement must be testable with clear pass/fail criteria
- User stories must follow: "As a [role], I want [feature] so that [benefit]"
- Business rules must have a unique ID: `BR-[SERVICE]-[3CHAR]` where:
  - SERVICE: Two-letter code for the service (e.g., AC for Accounts, TR for Trading, MK for Market)
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
  - Examples: BR-AC-Q2M (accounts business rule), BR-TR-L8K (trading business rule)
- Business rules must be unambiguous: "IF [condition] THEN [action]"
- Features must have a unique ID: `FEA-[SERVICE]-[3CHAR]` where:
  - SERVICE: Two-letter code for the service (e.g., AC for Accounts, TR for Trading, MK for Market)
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
  - Examples: FEA-AC-T5N (accounts feature), FEA-TR-M9J (trading feature)
- Features must include priority levels (P0 = Critical, P1 = Important, P2 = Nice-to-have)

### Non-Functional Requirements
- Performance metrics must be quantified (not "fast" but "< 100ms response time")
- Scalability must define concrete targets (users, transactions, data volume)
- Security requirements must reference specific standards or compliance needs
- All constraints must be measurable and verifiable

### Technical Specifications
- External dependencies must include version requirements and SLAs
- Integration points must specify protocols, data formats, and error handling
- Data requirements must include retention policies and privacy considerations

## Issues Report Structure

### Critical Issues Section
- **Issue Title**: Clear, descriptive name
- **Description**: What's wrong or contradictory
- **Impact**: Why this blocks development
- **Recommendation**: Suggested resolution

### Important Clarifications Section
- **Topic**: Area needing clarification
- **Current Statement**: What the brief says
- **Ambiguity**: What's unclear or incomplete
- **Questions**: Specific clarifications needed

### Minor Suggestions Section
- **Current**: What exists in the brief
- **Proposed**: Recommended improvement
- **Rationale**: Why this would be better

## Preferences Document Structure

### Entry Format
```markdown
## Entry [number]: [Topic]
**Type**: Question/Answer OR Directive
**Question**: [If Q&A: The question asked]
**User Input**: [The exact user response or directive]
**Context**: [Why this matters or what prompted this]
**Impact**: [How this affects the PRD or decisions]
**Date**: [YYYY-MM-DD]
```

### Document Organization
- Sequential numbering for traceability
- Clear type distinction (Q&A vs Directive)
- Verbatim user input capture
- Context and impact documentation

## Financial Service Considerations

For financial/trading services, pay special attention to:
- **Regulatory Compliance**: Identify all applicable regulations upfront
- **Audit Requirements**: Define what needs to be logged and for how long
- **Financial Calculations**: Specify precision requirements and rounding rules
- **Risk Management**: Include limits, controls, and monitoring requirements
- **Data Integrity**: Define transaction atomicity and consistency requirements

## Output Quality Checklist

Before finalizing the PRD, ensure:
- [ ] All product brief points are addressed
- [ ] All sections are complete
- [ ] Every requirement is testable
- [ ] Success metrics are measurable
- [ ] User roles and permissions are completely defined
- [ ] Business rules cover all scenarios
- [ ] External dependencies are fully specified
- [ ] The document is self-contained (no external knowledge required)

## Template-Specific Guidelines

### Minimal PRD Template
**When to use**: Simple applications with complexity score 0-3
- Focus on core functionality only
- Skip sections that don't apply
- Keep technical requirements basic
- Success criteria should be straightforward

### Standard PRD Template
**When to use**: Business applications with complexity score 4-7
- Use [N/A] for sections that don't apply
- Include user roles only if multiple types exist
- Focus on features that add business value
- Keep non-functional requirements relevant

### Comprehensive PRD Template
**When to use**: Complex systems with complexity score 8-10
- Fill all sections thoroughly
- Include all edge cases and scenarios
- Document all integrations and dependencies
- Specify detailed non-functional requirements

## Quality Checklist for Deliverables

### Complexity Assessment
- Scoring documented with justification
- Template selection explained
- User overrides captured if any
- Assessment saved in preferences

### PRD Completeness
- All sections from selected template are fully completed
- No missing product brief requirements
- All information is complete and specified
- [N/A] used appropriately in Standard template
- Changelog included for updates

### Requirements Quality
- Testable acceptance criteria
- Measurable success metrics
- Unambiguous business rules
- Complete user role definitions

### Technical Clarity
- External dependencies fully specified
- Integration points documented
- Data requirements complete
- Performance targets quantified