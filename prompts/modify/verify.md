# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

A modification has been requested and processed through the system. We need to verify that:
1. The modification was correctly classified and routed
2. The directive was properly recorded
3. The cascade was executed completely
4. The system remains consistent
5. The requested change is now present in the system

# Read

Read all relevant content to verify the modification:

## Core Documents
* `workspace/output/requirements/prd.md`: Check if requirements reflect the change
* `workspace/output/domain/domain_model.md`: Verify domain model consistency
* `workspace/output/stories/stories.md`: Check user story updates
* `workspace/output/architecture/architecture.md`: Verify architectural consistency
* Service specifications in `workspace/output/services/*/service.md`
* API specifications in `workspace/output/api/*.md`
* Code implementations in `workspace/code/*/`

## Preferences Files (Check for Directives)
* `workspace/output/requirements/preferences.md`
* `workspace/output/domain/preferences.md`
* `workspace/output/stories/preferences.md`
* `workspace/output/architecture/preferences.md`
* Service-level preferences in `workspace/output/services/preferences.md`
* API preferences in `workspace/output/api/preferences.md`
* Code preferences in `workspace/code/preferences.md`

**Important**: Focus on verifying the modification's proper application and system consistency.

# Verify

## 1. Directive Verification
Check that the modification directive was recorded correctly:
* Is the directive in the correct preferences file?
* Does it describe the CURRENT desired state (not history)?
* Are any conflicting old directives removed?
* Is the directive clear and actionable?
* Does it match what the user requested?

## 2. Classification Verification
Verify the modification was correctly classified:
* Was the entry point appropriate for the change?
* Should it have started at a different level?
* Were all affected levels identified?

## 3. Cascade Completeness
Check that the cascade was executed properly:
* Were all necessary steps updated?
* Were any steps incorrectly skipped?
* Did each step handle the modification appropriately?
* Are there any orphaned changes?

## 4. Consistency Verification
Ensure system-wide consistency:

### Cross-Document Consistency
* Do requirements align with domain model?
* Do user stories match the requirements?
* Does architecture support all stories?
* Do APIs match architecture boundaries?
* Do service specs implement their APIs?
* Does code match specifications?

### Semantic Consistency
* Are entity names consistent across documents?
* Are service names consistent throughout?
* Are API contracts properly honored?
* Are data models aligned?

### No Contradictions
* Check for conflicting requirements
* Verify no contradictory directives
* Ensure no incompatible changes

## 5. Modification Effectiveness
Verify the modification achieved its goal:
* Is the requested change present in the system?
* Are all aspects of the change implemented?
* Does the system behavior match the modification?
* Are there any missing pieces?

## 6. Side Effects Check
Look for unintended consequences:
* Were any unrelated features broken?
* Are there performance impacts?
* Were security considerations maintained?
* Are there new inconsistencies?

## 7. Documentation Quality
Verify documentation is updated:
* Are all changed sections documented?
* Is the modification clearly explained?
* Are impacts properly noted?
* Is the current state accurately reflected?

# Specific Verification Checks

## For Requirements Modifications
* PRD reflects new/changed requirements
* Success metrics updated if needed
* Constraints properly documented
* Features correctly specified

## For Domain Modifications
* Entities added/removed/modified correctly
* Relationships properly updated
* Domain boundaries adjusted
* Data ownership clear

## For Story Modifications
* User stories added/updated/removed
* Story IDs maintained properly
* Coverage complete for new features
* Platform hints adjusted if needed

## For Architecture Modifications
* Service boundaries updated
* Communication patterns adjusted
* New services properly defined
* Dependencies correctly mapped

## For API Modifications
* Endpoints added/modified/removed
* Data models updated
* Authentication adjusted if needed
* Documentation complete

## For Service Modifications
* Internal structure updated
* Modules properly defined
* Technology choices documented
* Implementation approach clear

## For Code Modifications
* Code reflects specifications
* Tests updated for changes
* No regressions introduced
* Performance maintained

# Output

Create a verification report at `workspace/cache/verify_modify_modification.md`:

```markdown
# Modification Verification Report

## Modification Summary
**Request**: [Original user request]
**Entry Point**: [Where modification started]
**Cascade Path**: [Steps that were updated]
**Date**: [YYYY-MM-DD]

## Directive Verification
- ✅/❌ Directive properly recorded in: [file path]
- ✅/❌ Describes current state (not history)
- ✅/❌ Conflicting directives removed
- ✅/❌ Clear and actionable

## Classification Assessment
- **Correctness**: [Correct/Incorrect - explain if incorrect]
- **Entry Point**: [Appropriate/Should have been X]
- **Scope**: [Correctly identified/Missed components]

## Cascade Execution
| Step | Status | Notes |
|------|--------|-------|
| Requirements | ✅/❌/⚪ | [Changes made or skipped] |
| Domain | ✅/❌/⚪ | [Changes made or skipped] |
| Stories | ✅/❌/⚪ | [Changes made or skipped] |
| Architecture | ✅/❌/⚪ | [Changes made or skipped] |
| API | ✅/❌/⚪ | [Changes made or skipped] |
| Services | ✅/❌/⚪ | [Changes made or skipped] |
| Development | ✅/❌/⚪ | [Changes made or skipped] |

Legend: ✅ Updated | ❌ Failed | ⚪ Skipped (correctly)

## Consistency Check
### Document Alignment
- ✅/❌ Requirements ↔ Domain
- ✅/❌ Domain ↔ Stories
- ✅/❌ Stories ↔ Architecture
- ✅/❌ Architecture ↔ APIs
- ✅/❌ APIs ↔ Services
- ✅/❌ Services ↔ Code

### Issues Found
[List any consistency issues discovered]

## Modification Effectiveness
- ✅/❌ Requested change is present
- ✅/❌ All aspects implemented
- ✅/❌ System behavior matches request
- ✅/❌ No missing pieces

## Side Effects
- ✅/❌ No unrelated features broken
- ✅/❌ Performance maintained
- ✅/❌ Security maintained
- ✅/❌ No new inconsistencies

## Critical Issues
[List any critical problems that need immediate attention]

## Recommendations
[Suggestions for any follow-up actions needed]

## Verification Result
**Status**: PASS / FAIL / PASS WITH WARNINGS

**Summary**: [Brief explanation of the verification outcome]

## Next Steps
[What should happen next based on verification results]
```

# Verification Criteria

The modification passes verification if:
- Directive is properly recorded
- Classification was appropriate
- Cascade executed completely
- System remains consistent
- Modification achieved its goal
- No critical side effects
- Documentation is current

The modification fails verification if:
- Directive is missing or incorrect
- Wrong entry point chosen
- Cascade incomplete or failed
- System inconsistencies introduced
- Modification goal not achieved
- Critical side effects present
- Documentation outdated

Pass with warnings if:
- Minor issues present but modification functional
- Non-critical inconsistencies found
- Documentation needs minor updates
- Performance slightly impacted but acceptable