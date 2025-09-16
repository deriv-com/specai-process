# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have implemented a service based on its specification.
This service should meet all requirements from the specification and follow our development guidelines.
I want you to thoroughly verify this implementation before we proceed.

**Note**: You will be provided with a specific parameter:
- `service_name`: The service name (e.g., `trading`, `accounts`)

Focus your verification ONLY on the specified service.

# Read

Read all the content related to the specified service:
* Service implementation: All files in `workspace/code/{service_name}/`
* Service specification: `workspace/output/services/{service_name}/service.md`
* Development preferences: `workspace/code/preferences.md` (if it exists)
* `workspace/output/architecture/architecture.md`: Overall service architecture
* `workspace/output/requirements/prd.md`: The comprehensive product requirements document
* `workspace/output/requirements/preferences.md`: To get the PRD complexity score
* `prompts/develop/guideline.md`: Development standards to verify against
* For services with APIs, also read:
  - Public API: `workspace/output/api/{service_name}_public.md`
  - Internal API: `workspace/output/api/{service_name}_internal.md`

**Important**: Do not read any other verify.md files to avoid influence on your judgment.

**Note**: The `list_files` tool can be buggy. If it reports that files or directories don't exist, double-check with Linux commands like `ls` or `find`.

# Verify

Check if the service implementation is complete and ready:

## Service Alignment
* Does the implementation align with the service specification?
* Are all components from service.md implemented?
* Does it stay within service boundaries?
* Is the structure appropriate for the PRD complexity score?

## Code Structure
* For simple services (0-3): Is it appropriately flat/minimal?
* For standard services (4-7): Is there light modular organization?
* For complex services (8-10): Are modules well-defined?
* Is the directory structure complete and logical?
* Does it follow standard project organization for the chosen tech stack?

## API Implementation (for services with APIs)
* Do API implementations match the specifications exactly?
* Are all endpoints from the API specifications implemented?
* Are request/response formats correct?
* Is authentication/authorization properly implemented?

## Functionality Coverage
* Are all features from service.md implemented?
* Is business logic complete and correct?
* Are validation rules comprehensive?
* Are error scenarios properly handled?
* Are all user stories addressed?

## Code Quality
* Does code follow language-specific standards?
* Is error handling comprehensive?
* Are inputs validated properly?
* Is logging implemented appropriately?
* Are there any security vulnerabilities?

## Testing
* Are unit tests comprehensive?
* Do integration tests cover API endpoints?
* Are test cases well-organized?
* Is test coverage adequate?
* Do all tests pass?

## Integration
* For services calling others: Are internal APIs used correctly?
* Are service dependencies properly handled?
* Is retry/timeout logic implemented?
* Are connection failures handled gracefully?

## Documentation
* Is code well-documented with clear comments?
* Are complex algorithms explained?
* Is configuration documented?
* Are API endpoints documented?

## Development Standards
* Does implementation follow prompts/develop/guideline.md?
* Are security measures implemented?
* Is performance adequate?
* Are resources managed properly?

## Specific Checks
* Can a developer understand and maintain this code?
* Are there any code smells or anti-patterns?
* Is the implementation production-ready?
* Are there any hardcoded values that should be configurable?

# Output

Create a thorough report at: `workspace/cache/verify_develop_{service_name}.md`.

The report should include:

```markdown
# Verification Report: {service_name}

## Summary
Overall assessment: PASS/FAIL
Brief explanation of the decision

## Strengths
What is implemented well:
- [List specific strengths]

## Issues Found
| Severity | File:Line | Issue | Recommendation |
|----------|-----------|-------|----------------|
| Critical/High/Medium/Low | path/to/file:123 | Specific issue | How to fix |

## Coverage Analysis

### Service Specification Coverage
- [ ] All components from service.md implemented
- [ ] Complexity-appropriate structure
- [ ] Complete functionality

### API Coverage (if applicable)
- [ ] All public API endpoints implemented
- [ ] All internal API endpoints implemented
- [ ] Request/response formats match specs

### Testing Coverage
- [ ] Unit tests comprehensive
- [ ] Integration tests complete
- [ ] All tests passing

### Code Quality
- [ ] Follows language standards
- [ ] Proper error handling
- [ ] Security measures in place
- [ ] Well-documented

## Recommendations
1. [Priority fixes if any]
2. [Improvements to consider]

## Conclusion
[Final assessment and readiness for production]
```

Focus on actionable feedback that will improve the implementation quality.
