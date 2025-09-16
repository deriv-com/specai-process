# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated a Product Requirements Document (PRD) based on the initial product brief from non-technical stakeholders.
This PRD will guide all subsequent platform development phases.
I want you to thoroughly check this PRD and verify it before we proceed.

# Read

Read all the content related to requirements:
* `workspace/output/requirements/prd.md`: The product requirements document.
* `workspace/output/requirements/preferences.md`: The document with user directives, decisions, and clarifications.
* `workspace/input/product_brief.md`: The original product brief from stakeholders.
* Determine which template was used by checking the complexity assessment in preferences
* Then read ONLY that specific PRD template:
  - If score was 0-3: Read `templates/prd_minimal.md`
  - If score was 4-7: Read `templates/prd_standard.md`
  - If score was 8-10: Read `templates/prd.md`

**Important**: Focus your verification on the PRD quality and completeness. Do not read any other verify.md files.

# Verify

Read all of these at once and then check if the PRD is complete and ready:

## Complexity Assessment Verification
* Was a complexity assessment performed and documented?
* Are the complexity scores (0-10) justified based on the product brief?
* Was the appropriate PRD template selected based on the total score?
* If user override was applied, is it documented with reasoning?
* Is the assessment saved in preferences.md?

## Template Compliance
* Does the PRD follow the structure of the selected template?
* For Minimal template: Are only essential sections included?
* For Standard template: Are [N/A] markers used appropriately for irrelevant sections?
* For Comprehensive template: Are all sections thoroughly completed?
* Is the level of detail appropriate for the complexity tier?

## Brief Coverage
* Does the PRD address all points from the original product brief?
* Are there any requirements from the brief that are missing?
* Has the analyst properly translated non-technical language into clear requirements?

## Issue Resolution
* Were all critical issues identified and addressed?
* Are there unresolved contradictions or ambiguities?
* Have all sections been completed with full information?
* Are all user directives properly applied?

## PRD Structure
* Does the PRD follow the selected template structure?
* Are all required sections for that template present and filled?
* Is each section detailed appropriately for the complexity level?
* Are sections marked [N/A] truly not applicable?

## Requirements Quality
* Are functional requirements clear and testable?
* Are acceptance criteria specific and measurable?
* Are business rules well-defined with clear conditions and actions?
* Are user stories properly formatted and complete?
* Is every section fully completed with specific information?

## Non-Functional Requirements
* Are performance requirements quantified?
* Are scalability needs clearly defined?
* Are security and compliance requirements specific?
* Are all external dependencies identified?

## Preferences Integration
* Are all user directives and decisions properly reflected in the PRD?
* Does the PRD reference relevant preference entries?
* Is there consistency between preferences and PRD content?
* Have all documented preferences been applied?

## Implementation Readiness
* Can developers understand what to build from this PRD?
* Are success metrics clearly defined?
* Are there any gaps that would block development?

## Specific Checks
* Are all user types and roles clearly defined?
* Are business constraints properly documented?
* Is the glossary complete for domain-specific terms?
* Are regulatory requirements clearly stated?

# Output

Create a thorough report at `workspace/cache/verify_requirements_prd.md`. This should explain:
* What is working well in the PRD
* Any issues, gaps, or concerns that need to be addressed
* Specific recommendations for improvements
* Assessment of completeness compared to the product brief
* Overall readiness to proceed with platform development

Structure the report with these sections:
- **Summary**: Overall assessment (Ready/Not Ready)
- **Complexity Assessment Review**:
  - Was assessment performed correctly?
  - Is template selection appropriate?
  - Any concerns with scoring?
- **Template Compliance**: How well the PRD follows the selected template
- **Strengths**: What aspects of the PRD are well done
- **Critical Issues**: Must-fix problems before proceeding
- **Recommendations**: Specific improvements needed
- **Coverage Analysis**: Mapping of brief requirements to PRD sections
- **Preferences Review**: Assessment of how well user directives were captured and applied