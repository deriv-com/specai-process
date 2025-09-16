# Mode

**This task should be run in `roo-verify` custom mode.**

# Goal

We have generated a Docker Compose-based integration setup for running all services together locally.
This integration environment should enable developers to run and test the complete system.
I want you to thoroughly verify this integration setup before we proceed.

# Read

Read all the content related to integration:
* Integration configuration: All files in `workspace/code/integration/`
* `workspace/output/architecture/architecture.md`: To understand service relationships
* `workspace/output/services/*/service.md`: For deployment requirements
* `workspace/code/*/Dockerfile`: To verify Docker configurations exist
* `workspace/code/*/.env.example`: To check environment documentation
* `prompts/integration/guideline.md`: Integration standards to verify against

**Important**: Focus verification on the integration setup quality and completeness.

# Verify

Check if the integration setup is complete and ready:

## Docker Compose Configuration
* Is docker-compose.yml properly structured?
* Are all implemented services included?
* Are build contexts correctly pointing to service directories?
* Is the version compatible with common Docker installations?

## Service Definitions
* Does each service have proper configuration?
* Are ports mapped without conflicts?
* Are environment variables properly set?
* Are health checks defined and realistic?
* Are dependencies correctly specified?

## Database Setup
* Are database services properly configured?
* Do initialization scripts exist for schema creation?
* Are volumes configured for data persistence?
* Are database credentials properly managed?

## Networking
* Is a custom network defined for service isolation?
* Can services communicate by container name?
* Are only necessary ports exposed to host?
* Is network segmentation appropriate?

## Environment Management
* Does .env.example exist with all variables?
* Are all required variables documented?
* Are sensible defaults provided?
* Are secrets properly handled (not committed)?

## Startup Dependencies
* Is service startup order correct?
* Do health checks ensure proper sequencing?
* Are circular dependencies avoided?
* Will services wait for dependencies?

## Utility Scripts
* Do start/stop scripts exist and work?
* Is there a health check script?
* Is there a reset script for development?
* Are scripts executable and cross-platform compatible?

## Documentation
* Is README.md comprehensive?
* Are prerequisites clearly listed?
* Does quick start guide work?
* Are all services and ports documented?
* Is troubleshooting section helpful?

## Testing Setup
* Are smoke tests provided?
* Can inter-service communication be verified?
* Are integration test scripts included?
* Do health checks actually work?

## Development Experience
* Can the entire system start with one command?
* Are logs easily accessible?
* Is debugging straightforward?
* Does hot reload work where applicable?

## Specific Checks
* No hardcoded passwords in docker-compose.yml?
* All services from architecture included?
* Volumes for data persistence configured?
* Network isolation working properly?
* Can run without external dependencies?

# Output

Create a thorough report at: `workspace/cache/verify_integration.md`.

The report should include:

```markdown
# Integration Verification Report

## Summary
Overall assessment: PASS/FAIL
Brief explanation of the decision

## Configuration Review

### Docker Compose
- ✅/❌ Valid YAML syntax
- ✅/❌ Appropriate version
- ✅/❌ All services included
- ✅/❌ Proper structure

### Service Configurations
| Service | Build | Ports | Health Check | Dependencies |
|---------|-------|-------|--------------|--------------|
| [name] | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ |

### Database Setup
- ✅/❌ Database services configured
- ✅/❌ Init scripts present
- ✅/❌ Volumes configured
- ✅/❌ Credentials managed

### Networking
- ✅/❌ Custom network defined
- ✅/❌ Service communication possible
- ✅/❌ Port mappings correct
- ✅/❌ Network isolation

## Environment Management
- ✅/❌ .env.example complete
- ✅/❌ All variables documented
- ✅/❌ Defaults provided
- ✅/❌ Secrets handled properly

## Scripts and Tools
- ✅/❌ Start script works
- ✅/❌ Stop script works
- ✅/❌ Health check script
- ✅/❌ Reset script
- ✅/❌ Scripts are executable

## Documentation Quality
- ✅/❌ README comprehensive
- ✅/❌ Prerequisites listed
- ✅/❌ Quick start works
- ✅/❌ Service table complete
- ✅/❌ Troubleshooting helpful

## Issues Found
| Severity | Component | Issue | Recommendation |
|----------|-----------|-------|----------------|
| Critical/High/Medium/Low | Component | Specific issue | How to fix |

## Recommendations
1. [Priority improvements]
2. [Enhancements to consider]

## Conclusion
[Final assessment and readiness for use]
```

Focus on actionable feedback that will improve the integration setup.