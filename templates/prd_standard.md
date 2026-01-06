# Product Requirements Document (PRD) - Standard Template
## For Business Applications

---

# 1. EXECUTIVE SUMMARY

## 1.1 Product Vision
*[1-2 sentences describing what this product will achieve]*

## 1.2 Success Metrics
- **Primary KPI**: [Measurable outcome]
- **Secondary KPIs**: [List 1-2 additional metrics]

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
*[Mark as [N/A] if section not applicable]*
- **Regulatory**: [Compliance requirements or N/A]
- **Security**: [Security standards required]
- **Operational**: [Business rules that cannot change]

---

# 3. FUNCTIONAL REQUIREMENTS

## 3.1 Core Features
*[Each feature should have a unique ID: FEA-[APP]-[3CHAR]]*

### Feature: [Feature Name] (FEA-[APP]-[3CHAR])
- **Priority**: P0/P1/P2
- **User Story**: As a [user type], I want to [action] so that [outcome]
- **Acceptance Criteria**:
  - [Testable criterion 1]
  - [Testable criterion 2]
- **Dependencies**: [Other features or systems required, or N/A]

## 3.2 User Roles & Permissions
*[Mark as [N/A] if single user type]*
| Role | Capabilities | Restrictions |
|------|--------------|--------------|
| [Role] | [List capabilities] | [List restrictions] |

## 3.3 Business Rules
*[Mark as [N/A] if no complex business rules]*
- BR-[APP]-[3CHAR]: IF [condition] THEN [action]

---

# 4. NON-FUNCTIONAL REQUIREMENTS

## 4.1 Performance
*[Include only if specific performance requirements exist]*
| Metric | Requirement | Critical Threshold |
|--------|-------------|-------------------|
| Response Time | [Target] | [Max acceptable] |
| Concurrent Users | [Target] | [Must support] |

## 4.2 Security
- **Authentication**: [Method required]
- **Data Protection**: [Basic requirements]
- **Access Control**: [How permissions are managed]

---

# 5. TECHNICAL SPECIFICATIONS

## 5.1 Technology Choices
- **Frontend**: [Framework/approach]
- **Backend**: [Language/framework]
- **Database**: [Type and specific technology]
- **Hosting**: [Cloud/on-premise requirements]

## 5.2 External Dependencies
*[Mark as [N/A] if none]*
| System | Purpose | Integration Type |
|--------|---------|------------------|
| [System] | [Why needed] | [REST API/Library/etc] |

## 5.3 Data Requirements
- **Data Volume**: [Expected size]
- **Backup**: [Frequency and retention]
- **Privacy**: [Any PII handling requirements]

---

# 6. IMPLEMENTATION GUIDANCE

## 6.1 Development Priorities
1. [What to build first]
2. [What to build next]
3. [Nice to have features]

## 6.2 Key Decisions
*[Important technical or business decisions that affect implementation]*
- [Decision 1]
- [Decision 2]

---

# 7. ACCEPTANCE CRITERIA

## 7.1 Definition of Done
- [All features implemented and tested]
- [Security requirements met]
- [Performance targets achieved]
- [User documentation complete]

## 7.2 Launch Readiness
- [ ] All P0 features complete
- [ ] Security review passed
- [ ] User acceptance testing complete

---

# APPENDICES

## A. Glossary
*[Include only if domain-specific terms are used]*
| Term | Definition |
|------|------------|
| [Term] | [Clear definition] |

## B. Mockups/Wireframes
*[Reference to design files or basic sketches if available]*

## C. Technical Standards
*[Only if specific standards must be followed]*
- [Standard Name]: [Version and requirements]