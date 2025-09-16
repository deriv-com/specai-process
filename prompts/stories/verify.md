# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated user stories that capture all user interactions with the system.
These stories will guide the platform architecture and ensure all user needs are addressed.
I want you to thoroughly check these user stories and verify them before we proceed.

# Read

Read all the content related to user stories:
* `workspace/output/stories/stories.md`: The user stories document.
* `workspace/output/requirements/prd.md`: The comprehensive product requirements document.
* `workspace/output/requirements/preferences.md`: The document with user directives and clarifications (if it exists).

**Important**: Focus your verification on the user stories and their alignment with product requirements. Do not read any other verify.md files.

# Verify

Read all of these at once and then check if the user stories are complete and ready:

## User Type Coverage
* Are all types of users who interact with the system identified?
* Are there any missing user types (administrators, operators, integrators)?
* Is each user type clearly described with distinct characteristics?

## Story Completeness
* Do stories cover all features from the PRD?
* Are edge cases and administrative functions included?
* Is the complete user journey represented (onboarding to advanced usage)?
* Are cross-user interactions captured?

## Story Quality
* Are stories in the standard format: "As a [user], I want to [action] so that [benefit]"?
* Are stories atomic (one need per story)?
* Are stories focused on WHAT users need, not HOW it's implemented?
* Are story IDs unique and following the US-[SERVICE]-[3CHAR] format?

## Service Hints
* Do service hints make logical sense?
* Are hints distributed across multiple services (not centralized)?
* Do hints align with good micro-service boundaries?

## Traceability
* Can all PRD features be traced to user stories?
* Is the Story Coverage Matrix complete and accurate?
* Are there any PRD requirements without corresponding stories?

## Story Organization
* Are stories well-organized by user type?
* Within each type, are they grouped by functional area?
* Is the structure easy to navigate?

# Output

Create a thorough report at `workspace/cache/verify_stories_stories.md`. This should explain:
* What is working well in the user stories
* Any issues, gaps, or concerns that need to be addressed
* Specific recommendations for improvements
* Assessment of coverage completeness
* Overall readiness to proceed with service definitions