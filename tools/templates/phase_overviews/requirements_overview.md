# Requirements Phase Overview

## Purpose
Transforms non-technical product briefs from stakeholders into comprehensive Product Requirements Documents (PRDs) that guide all subsequent development phases.

## Key Concepts
- **Complexity Assessment**: Scores projects 0-10 to select appropriate PRD template
  - 0-3: Minimal template for simple applications
  - 4-7: Standard template for business applications  
  - 8-10: Comprehensive template for complex systems
- **Operational Modes**: 
  - New: Creates PRD from scratch
  - Update: Gap analysis between existing PRD and new requirements
  - Review: Helps user modify preferences and decisions
- **Preference Tracking**: Records user decisions as current state directives (not history)

## Process Flow
1. Read product brief from `workspace/input/product_brief.md`
2. Perform complexity assessment with scoring justification
3. Select appropriate PRD template based on score
4. Identify gaps, contradictions, and missing information
5. Ask clarifying questions in batches to minimize iterations
6. Generate comprehensive PRD with all sections complete
7. Run verification to ensure quality and completeness

## Critical Features
- Intelligent template selection based on complexity
- Question batching to minimize back-and-forth interaction
- Directive recording in preferences.md as current state
- Mode detection for handling existing work
- User Input Checkpoint for first-time runs
- Iterative refinement (2 iterations for new mode)

## Files Involved
- **Input**: `workspace/input/product_brief.md`
- **Templates**: `templates/prd*.md`, `templates/preferences.md`
- **Output**: `workspace/output/requirements/prd.md`, `workspace/output/requirements/preferences.md`
- **Verification**: Creates `workspace/cache/verify_requirements_prd.md`

## Common Modifications at This Level
- Adding new features or removing features
- Changing business rules or constraints
- Updating regulatory or compliance requirements
- Modifying success metrics or KPIs
- Changing user types or permissions

## Important Guidelines
- Always check existing preferences before asking questions
- Document complexity assessment in preferences
- Use specific requirement IDs (REQ-XX-XXX format)
- Avoid scope creep beyond product brief
- Focus on WHAT, not HOW (leave implementation to later phases)

## Quality Checklist
- All product brief points addressed
- Complexity assessment documented
- Template appropriately selected
- All sections complete
- Requirements testable
- Success metrics measurable
- User roles defined
- Business rules clear