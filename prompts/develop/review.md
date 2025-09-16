# Mode

**This task should be run in `roo-man` custom mode.**

# Goal

We have implemented and verified a service. The verification phase confirmed the code meets all requirements and specifications. Now we need to perform a thorough architectural and security review to ensure the implementation meets our quality standards, security requirements, and best practices - regardless of what the requirements specified.

**Key Distinction from Verification:**
- **Verification (`verify.md`)**: Does the code do what the requirements asked for?
- **Review (`review.md`)**: Is the code production-ready, secure, and maintainable?

**Note**: You will be provided with specific parameters:
- `service_name`: The service name (e.g., `trading`, `accounts`)
- `verification_status`: The result from verification phase (should be PASS to reach this step)

Focus your review ONLY on the specified service.

# Read

Read all the content related to the specified service:
* Service implementation: All files in `workspace/code/{service_name}/`
* Service specification: `workspace/output/services/{service_name}/service.md`
* Verification report: `workspace/cache/verify_develop_{service_name}.md`
* `workspace/output/architecture/architecture.md`: To understand architectural constraints
* `prompts/develop/guideline.md`: Development standards

**Important**: Focus on architectural quality, security, and design patterns rather than functional correctness (already verified). Even if the code perfectly meets requirements, it may still have security vulnerabilities, performance issues, or maintainability problems that need addressing.

**Note**: The `list_files` tool can be buggy. If it reports that files or directories don't exist, double-check with Linux commands like `ls` or `find`.

# Review Focus Areas

## 1. Security Review
**Look for concrete security issues that need fixing (regardless of requirements):**
- Input validation vulnerabilities (SQL injection, XSS, command injection)
- Authentication/authorization flaws (even if not specified in requirements)
- Insecure data handling or storage (passwords in plaintext, unencrypted PII)
- Exposed sensitive information in logs, errors, or responses
- Missing security headers or protections (CORS, CSP, rate limiting)
- Unsafe dependencies or libraries with known vulnerabilities
- Race conditions or timing attacks
- Hardcoded credentials or API keys
- Insufficient entropy in random number generation
- Missing audit logs for sensitive operations

## 2. Architectural Review
**Assess production readiness and system design (beyond requirements):**
- Service boundary violations (doing too much or too little)
- Improper coupling with other services (tight coupling, chatty interfaces)
- Scalability bottlenecks (single points of failure, state management issues)
- Performance anti-patterns (N+1 queries, synchronous when async would be better)
- Resource leaks or inefficient usage (unclosed connections, memory leaks)
- Missing resilience patterns (retries, circuit breakers, timeouts, fallbacks)
- Inadequate monitoring/observability hooks (no metrics, insufficient logging)
- Missing health checks or readiness probes
- No graceful shutdown handling
- Lack of idempotency where needed

## 3. Code Quality Review
**Identify design and maintainability issues (even if code works):**
- Complex code that's hard to understand (cognitive complexity)
- Missing abstraction where needed (DRY violations, repeated logic)
- Over-engineering for simple services (unnecessary complexity)
- Inconsistent patterns within the service (mixed paradigms)
- Poor error propagation (swallowing exceptions, generic error messages)
- Inadequate logging for debugging (not enough context, wrong log levels)
- Missing or misleading documentation (outdated comments, no README)
- Magic numbers and hardcoded values
- Poor naming conventions (unclear variable/function names)
- Dead code or commented-out code blocks

## 4. Best Practices Review
**Check adherence to industry standards (regardless of project requirements):**
- Language-specific idioms and conventions (PEP 8, ESLint rules, etc.)
- Framework best practices (proper use of framework features)
- Testing patterns and coverage (unit tests, integration tests, edge cases)
- Configuration management (externalized config, no hardcoded environments)
- Dependency management (pinned versions, security updates, minimal dependencies)
- Build and deployment readiness (Dockerfile, CI/CD compatibility)
- Version control practices (no secrets in code, proper .gitignore)
- API versioning and backward compatibility considerations
- Proper use of async/await and concurrency patterns
- Database best practices (indexes, query optimization, migrations)

# Review Process

1. **Read the verification report** to understand what has already been checked
2. **Analyze the implementation** focusing on the areas above
3. **Identify concrete issues** that require developer action
4. **Prioritize findings** by severity and impact
5. **Provide specific recommendations** for each issue

# Output

Create a thorough review report at: `workspace/cache/review_develop_{service_name}.md`.

The report should include:

```markdown
# Architecture & Security Review: {service_name}

## Executive Summary
Overall assessment of the service implementation quality, security posture, and architectural alignment.

## Security Findings
| Severity | File:Line | Issue | Fix |
|----------|-----------|-------|-----|
| Critical/High | path/to/file:123 | Specific vulnerability with code snippet | Concrete fix |

*Only include actual security vulnerabilities that need fixing*

## Architectural Concerns
| Severity | Component | Issue | Recommendation |
|----------|-----------|-------|----------------|
| High/Medium | Component name | Specific architectural problem | How to address |

*Focus on scalability, resilience, and maintainability issues*

## Code Quality Issues
| Severity | File:Line | Issue | Improvement |
|----------|-----------|-------|-------------|
| Medium/Low | path/to/file:456 | Specific quality issue | Suggested refactoring |

*Include only issues that significantly impact maintainability*

## Best Practices Violations
| Area | Current Practice | Recommended Practice | Priority |
|------|-----------------|---------------------|----------|
| Testing/Config/etc | What's wrong | What's right | High/Medium/Low |

## Positive Findings
Brief mention of what's done well (1-2 sentences). Focus on exemplary practices that could be adopted elsewhere.

## Top 5 Priority Actions
1. [Most critical issue to fix]
2. [Second priority]
3. [Third priority]
4. [Fourth priority]
5. [Fifth priority]

## Conclusion
- Review Status: PASS/FAIL (independent of requirement compliance)
- Production Readiness: YES/NO (with conditions if any)
- Security Posture: SECURE/NEEDS_ATTENTION/CRITICAL_ISSUES
- Technical Debt Assessment: LOW/MEDIUM/HIGH
- Next Steps: Clear actions needed before deployment
```

**Important Guidelines:**
- Report only concrete problems that require action
- Every finding must include exact location and fix
- Prioritize security and architectural issues
- Keep feedback actionable and specific
- Avoid commenting on working code
- Focus on what needs to change, not what's already good
