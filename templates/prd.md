# Product Requirements Document (PRD) Template
## AI-Driven Development Version

---

# 1. EXECUTIVE SUMMARY

## 1.1 Product Vision
*[1-2 sentences describing what this product will achieve]*

## 1.2 Success Metrics
- **Primary KPI**: [Measurable outcome]
- **Secondary KPIs**: [List 2-3 additional metrics]

## 1.3 AI Development Constraints
- **Regulatory Compliance**: [List non-negotiable regulations]
- **Integration Requirements**: [External systems that must connect]
- **Performance Benchmarks**: [Critical performance requirements]

---

# 2. BUSINESS CONTEXT

## 2.1 Problem Statement
*[Clear description of the problem being solved]*

## 2.2 Target Users
| User Type | Primary Need | Success Criteria |
|-----------|--------------|------------------|
| [Type 1]  | [Need]       | [Metric]         |
| [Type 2]  | [Need]       | [Metric]         |

## 2.3 Business Constraints
- **Regulatory**: [Compliance requirements]
- **Security**: [Security standards required]
- **Operational**: [Business rules that cannot change]

---

# 3. FUNCTIONAL REQUIREMENTS

## 3.1 Core Features
*[Use this format for each feature. Each requirement within a feature should have a unique ID: REQ-[SECTION]-[3CHAR]]*

### Feature: [Feature Name] (FEA-[SERVICE]-[3CHAR])
- **Priority**: P0/P1/P2
- **User Story**: As a [user type], I want to [action] so that [outcome]
- **Acceptance Criteria**:
  - [Testable criterion 1]
  - [Testable criterion 2]
- **Constraints**: [Any specific limitations]
- **Dependencies**: [Other features or systems required]

## 3.2 User Roles & Permissions
| Role | Capabilities | Restrictions |
|------|--------------|--------------|
| [Role] | [List capabilities] | [List restrictions] |

## 3.3 Business Rules
*[Format: BR-[SERVICE]-[3CHAR]: Condition → Action]*
- BR-AC-X5M: IF [condition] THEN [action]
- BR-TR-N2K: IF [condition] THEN [action]

---

# 4. NON-FUNCTIONAL REQUIREMENTS

## 4.1 Performance
| Metric | Requirement | Critical Threshold |
|--------|-------------|-------------------|
| Response Time | [Target] | [Max acceptable] |
| Throughput | [Target] | [Min required] |
| Concurrent Users | [Target] | [Must support] |

## 4.2 Scalability
- **Horizontal Scaling**: [Requirements]
- **Data Volume**: [Expected growth]
- **Geographic Distribution**: [Requirements]

## 4.3 Security & Compliance
- **Data Protection**: [Standards required]
- **Authentication**: [Methods required]
- **Audit Trail**: [What must be logged]

---

# 5. EXTERNAL DEPENDENCIES

## 5.1 Data Sources
| Source | Data Type | Update Frequency | Criticality |
|--------|-----------|------------------|-------------|
| [Source] | [Type] | [Frequency] | [Critical/Important/Nice-to-have] |

## 5.2 Third-Party Integrations
| System | Purpose | API Type | SLA Required |
|--------|---------|----------|--------------|
| [System] | [Why needed] | [REST/GraphQL/etc] | [Uptime requirement] |

---

# 6. AI IMPLEMENTATION GUIDANCE

## 6.1 Optimization Priorities
1. **Primary**: [What to optimize first]
2. **Secondary**: [What to optimize next]
3. **Tertiary**: [Nice to have optimizations]

## 6.2 Decision Boundaries
### AI Can Decide:
- [List of decisions AI can make autonomously]

### AI Must Escalate:
- [List of decisions requiring human validation]

## 6.3 Quality Assurance
- **Automated Testing**: [Required coverage]
- **Performance Testing**: [Load testing requirements]
- **Compliance Validation**: [How to verify regulatory compliance]

---

# 7. ACCEPTANCE CRITERIA

## 7.1 Launch Criteria
- [Measurable criterion for launch readiness]
- [Regulatory approval obtained]
- [Performance benchmarks met]

## 7.2 Success Metrics (Post-Launch)
| Timeframe | Metric | Target |
|-----------|--------|--------|
| 30 days | [Metric] | [Target] |
| 90 days | [Metric] | [Target] |

---

# APPENDICES

## A. ID Conventions Reference
*Use these ID formats throughout the PRD for consistent tracking:*
- **Requirements**: `REQ-[SECTION]-[3CHAR]` (e.g., REQ-AC-K3M for accounts section)
- **Features**: `FEA-[SERVICE]-[3CHAR]` (e.g., FEA-TR-M9J for trading service)
- **Business Rules**: `BR-[SERVICE]-[3CHAR]` (e.g., BR-AC-Q2M for accounts service)
- **API Endpoints**: `API-[SERVICE]-[3CHAR]` (e.g., API-MK-R4K for market service)
- **Error Codes**: `ERR-[SERVICE]-[3CHAR]` (e.g., ERR-TR-V2L for trading service)
- **Test Cases**: `TC-[SERVICE]-[3CHAR]` (e.g., TC-AC-J6Q for accounts service)
- **User Stories**: `US-[SERVICE]-[3CHAR]` (e.g., US-MK-P7R for market service)

*Where:*
- `[SECTION]`: Two-letter code for PRD section (AC=Accounts, TR=Trading, MK=Market, etc.)
- `[SERVICE]`: Two-letter code for service
- `[3CHAR]`: Three random alphanumeric characters

## B. Glossary
| Term | Definition |
|------|------------|
| [Term] | [Clear definition] |

## C. Regulatory References
- [Regulation Name]: [Relevant sections]

## D. Technical Standards
- [Standard Name]: [Version and requirements]