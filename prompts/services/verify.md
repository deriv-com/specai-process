# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated a service specification for a specific domain service.
We will use this specification to guide the implementation of the complete service.
I want you to thoroughly check this service specification and verify it before we proceed.

**Note**: You will be provided with a specific parameter:
- `service_name`: The **clean service name** (e.g., `trading`, `accounts`) - NOT service ID

Focus your verification ONLY on the specified service.

# Read

Read all the content related to the specified service:
* Service specification: `workspace/output/services/{service_name}/service.md`
* Service preferences: `workspace/output/services/preferences.md` (if it exists)
* `workspace/output/architecture/architecture.md`: Overall service architecture
* `workspace/output/requirements/prd.md`: The comprehensive product requirements document
* For services with APIs, also read:
  - Public API: `workspace/output/api/{service_name}_public.md`
  - Internal API: `workspace/output/api/{service_name}_internal.md`

**Important**: Do not read any other verify.md files to avoid influence on your judgment.

# Verify

Check if the service specification is complete and ready:

## Service Alignment
* Does the service implementation align with the service architecture?
* Are all architectural requirements for this service addressed?
* Does it stay within service boundaries?
* Are all required modules included (APIs, persistence, business logic)?

## Module Architecture
* Is the module breakdown logical and complete?
* Do modules have clear, non-overlapping responsibilities?
* Are all service functionalities covered by modules?
* Is the implementation order reasonable?
* Are module interactions well-defined?

## File Structure
* Is the directory structure complete and logical?
* Does it follow standard project organization for the chosen tech stack?
* Are all necessary files accounted for?

## API Implementation (for services with APIs)
* Do API modules cover all endpoints from the API specifications?
* Are request/response handling properly defined?
* Is authentication/authorization addressed?

## Persistence Patterns
* Are domain-oriented interfaces well-defined?
* Is data integrity properly managed?
* Are all data operations covered?
* Is the database design appropriate?

## Business Logic
* Is business logic clearly specified across modules?
* Are validation rules comprehensive?
* Are error scenarios properly handled?
* Are business rules from PRD implemented?

## Technical Quality
* Are error codes well-defined and consistent?
* Is configuration management addressed?
* Are dependencies clearly identified?
* Is the tech stack appropriate for requirements?

## Service Integration
* For services calling other services: Are external APIs properly referenced?
* Are internal module dependencies clear?
* Is the service properly isolated from other services?

## Operational Readiness
* Are monitoring points identified?
* Is the deployment model clear?
* Are performance requirements addressed?
* Is the security architecture comprehensive?

## Specific Checks
* Are all required sections present in service.md?
* Is the level of detail sufficient for implementation?
* Are there any contradictions or ambiguities?
* Can a developer implement this without further clarification?
* Does it cover all user stories assigned to this service?

# Output

Create a thorough report using **clean service name** in file path: `workspace/cache/verify_service_{service_name}.md`.

**IMPORTANT**: Use the clean service name (e.g., `trading`) in file paths, NOT service IDs (e.g., `SVC-TR-K3M`).

The report should explain:
* What is working well in the service specification
* Any issues, gaps, or concerns that need to be addressed
* Specific recommendations for improvements
* Assessment of alignment with service architecture
* Overall readiness for implementation

Structure the report with clear sections:
- **Summary**: Pass/Fail status with brief explanation
- **Strengths**: What is well-specified
- **Issues Found**: Detailed list of problems (if any)
- **Recommendations**: Specific actions to address issues
- **Conclusion**: Overall assessment

Focus on actionable feedback that will improve the specification quality.