# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated an API specification for a specific domain service (either public or internal API).
We will use this specification to guide the implementation of the API.
I want you to thoroughly check this API specification and verify it before we proceed.

**Note**: You will be provided with specific parameters:
- `service_name`: The **clean service name** (e.g., `trading`, `accounts`) - NOT service ID
- `api_type`: Either "public" or "internal"

Focus your verification ONLY on the specified API.

# Read

Read all the content related to the specified API:
* API Specification:
  - For public: `workspace/output/api/{service_name}_public.md`
  - For internal: `workspace/output/api/{service_name}_internal.md`
* API Preferences: `workspace/output/api/preferences.md` (if it exists)
* `workspace/output/architecture/architecture.md`: Overall service architecture
* `workspace/output/requirements/prd.md`: The comprehensive product requirements document
* `workspace/output/requirements/preferences.md`: The document with user directives and clarifications (if it exists)
* For internal APIs: Check service architecture to verify inter-service needs

**Important**: Focus verification on the specified API. Do not read other API specs or verify.md files.

# Verify

Check if the API specification is complete and ready:

## API Coverage
* Does the API cover all required functionality for its type?
* For public APIs: Are all UI features properly supported?
* For internal APIs: Are all inter-service needs addressed?
* Are there any missing endpoints?

## API Design
* Is the API design consistent and logical?
* Are endpoints well-organized and RESTful (if REST)?
* Are naming conventions followed consistently?
* Is the authentication approach appropriate?

## Data Models
* Are all data models clearly defined?
* Are schemas complete and unambiguous?
* Do models align with service architecture?
* Are there any missing or redundant models?

## Service Boundaries
* Does the API respect service boundaries?
* Are there any endpoints that belong to other services?
* Is functionality properly scoped to this service?

## Technical Quality
* Are error responses comprehensive?
* Is versioning strategy clear and maintainable?
* Are rate limits appropriate (for public APIs)?
* Are examples helpful and accurate?

## Specific Checks
* Are all required sections present?
* Is the endpoint table complete and accurate?
* Are request/response examples provided?
* Is the changelog maintained (for updates)?

# Output

Create a thorough report using **clean service names** in file paths:
- For public: `workspace/cache/verify_api_{service_name}_public.md`
- For internal: `workspace/cache/verify_api_{service_name}_internal.md`

**IMPORTANT**: Use the clean service name (e.g., `trading`) in file paths, NOT service IDs (e.g., `SVC-TR-K3M`).

The report should explain:
* What is working well in the API specification
* Any issues, gaps, or concerns
* Specific recommendations for improvements
* Assessment of API completeness for its intended purpose
* Overall readiness for implementation