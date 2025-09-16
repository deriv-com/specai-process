# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated a Domain Model & Data Architecture document based on the Product Requirements Document (PRD).
This domain model will guide platform boundaries and data distribution decisions.
I want you to thoroughly check this domain model and verify it before we proceed.

# Read

Read all the content related to domain modeling:
* `workspace/output/domain/domain_model.md`: The domain model and data architecture document.
* `workspace/output/domain/preferences.md`: The document with user directives and clarifications for domain modeling (if it exists).
* `workspace/output/requirements/prd.md`: The comprehensive product requirements document.
* `workspace/output/requirements/preferences.md`: The document with user directives and clarifications (if it exists).

**Important**: Focus your verification on the domain model quality and completeness. Do not read any other verify.md files.

# Verify

Read all of these at once and then check if the domain model is complete and ready:

## Entity Coverage
* Are all major business concepts from the PRD represented as entities?
* Are there any missing entities that should be included?
* Do entity names use appropriate business terminology?

## Relationship Accuracy
* Are all relationships between entities properly identified?
* Are cardinalities (one-to-one, one-to-many, etc.) correct?
* Do relationships reflect actual business rules?
* Are cascade behaviors properly documented?

## Domain Boundaries
* Are entities logically grouped into coherent domains?
* Do domain boundaries align with business capabilities?
* Are bounded contexts clearly defined?
* Is there appropriate separation of concerns?

## Data Ownership
* Is data ownership clearly established for each entity?
* Are there any conflicts in ownership assignments?
* Is the ownership strategy practical and maintainable?

## Consistency Patterns
* Are transaction boundaries properly identified?
* Is the distinction between strong and eventual consistency clear?
* Are cross-domain interactions properly planned?

## Conceptual Clarity
* Does the model stay at the conceptual level (no implementation details)?
* Is the model understandable to business stakeholders?
* Are all domain-specific terms defined in the glossary?

## Requirements Alignment
* Can all PRD requirements be supported by this domain model?
* Are there any requirements that don't map to entities?
* Does the model over-engineer beyond stated requirements?

## Specific Checks
* Are entity lifecycles clearly documented?
* Are business rules and constraints captured?
* Is the ER diagram accurate and helpful?
* Are shared concepts across domains identified?

# Output

Create a thorough report at `workspace/cache/verify_domain_model.md`. This should explain:
* What is working well in the domain model
* Any issues, gaps, or concerns that need to be addressed
* Specific recommendations for improvements
* Assessment of completeness compared to the PRD
* Overall readiness to proceed with platform definitions

Structure the report with these sections:
- **Summary**: Overall assessment (Ready/Not Ready)
- **Strengths**: What aspects of the domain model are well done
- **Critical Issues**: Must-fix problems before proceeding
- **Recommendations**: Specific improvements needed
- **Coverage Analysis**: Mapping of PRD requirements to domain entities
- **Domain Boundary Assessment**: Quality of domain groupings