# Domain Modeling Phase Overview

## Purpose
Transforms the Product Requirements Document into a comprehensive domain model that captures core business entities, their relationships, and data architecture to guide service boundaries and data distribution.

## Key Concepts
- **Entity Identification**: Extract business entities from requirements (nouns representing core concepts)
- **Relationship Mapping**: Define associations, aggregations, compositions, and inheritance
- **Domain Boundaries**: Group related entities into coherent bounded contexts
- **Data Ownership**: Determine which domain owns which entities
- **Consistency Patterns**: Define transaction boundaries and eventual consistency needs

## Process Flow
1. Read PRD from `workspace/output/requirements/prd.md`
2. Extract all business entities and concepts
3. Map relationships with cardinalities
4. Group entities into logical domains
5. Define domain boundaries based on business capabilities
6. Establish data ownership strategies
7. Document consistency requirements
8. Run verification for completeness

## Critical Features
- Entity extraction from business requirements
- Relationship diagram generation (Mermaid.js)
- Domain boundary definition aligned with business capabilities
- Data ownership matrix creation
- Consistency pattern documentation
- Mode-aware updates preserving existing work

## Files Involved
- **Input**: `workspace/output/requirements/prd.md`
- **Guidelines**: `prompts/domain/guideline.md`
- **Output**: `workspace/output/domain/domain_model.md`, `workspace/output/domain/preferences.md`
- **Verification**: Creates `workspace/cache/verify_domain_model.md`

## Key Deliverables
- Executive summary of domain model
- Core business entities with IDs (ENT-XX-XXX)
- Entity relationship diagram
- Domain boundaries and bounded contexts
- Data ownership strategy
- Consistency patterns documentation
- Glossary of domain terms

## Common Modifications at This Level
- Adding or removing entities
- Changing entity relationships
- Modifying domain boundaries
- Adjusting data ownership
- Changing consistency requirements

## Important Guidelines
- Use business terminology from PRD
- Focus on conceptual model (no implementation details)
- Entities should have identity and lifecycle
- Respect aggregate root boundaries
- Document shared concepts across domains
- Consider transaction boundaries when grouping

## Quality Checklist
- All major business concepts represented
- Entities use consistent terminology
- Relationships reflect business rules
- Domain boundaries align with capabilities
- Data ownership clearly established
- Consistency requirements documented
- No implementation details leaked
- Model supports all PRD requirements