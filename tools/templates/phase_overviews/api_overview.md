# API Specifications Phase Overview

## Purpose
Creates comprehensive API specifications using a **consumer-driven approach** where consumers define what they need from providers, ensuring APIs are built based on actual requirements rather than assumptions.

## Key Concepts
- **API Types**:
  - Public APIs: For external consumers (web apps, mobile apps, third parties)
  - Internal APIs: For service-to-service communication
- **Consumer-Driven Design**: Consumers incrementally build provider APIs based on actual needs
- **Service Hierarchy**: Process from consumers to providers (top to bottom)
- **Smart Deduplication**: Avoid redundant endpoints across multiple consumers
- **Consumer Annotations**: Track which consumer needs which endpoint

## Process Flow
1. Build service dependency hierarchy from architecture
2. Start with Level 0 (public-facing services)
3. Process Level 1 (pure consumers) who define provider needs
4. Continue level by level down the hierarchy
5. Consumers expand provider APIs incrementally
6. Providers harmonize similar endpoints from multiple consumers
7. Bottom level providers implement accumulated requirements
8. Run verification for completeness

## Critical Features
- Consumer-driven API expansion capability
- Service hierarchy building and processing
- Mode detection (new/update/consumer_expand/review) per API
- Endpoint ID generation (API-XX-XXX)
- Error code standardization (ERR-XX-XXX)
- Smart duplicate detection for endpoints
- Consumer annotation and tracking
- Self-review phase for quality

## Files Involved
- **Input**: `workspace/output/architecture/architecture.md`, service specifications
- **Guidelines**: `prompts/api/guideline.md`
- **Output**: `workspace/output/api/{service}_public.md`, `{service}_internal.md`
- **Preferences**: `workspace/output/api/preferences.md` (single file for all APIs)
- **Verification**: Creates `workspace/cache/verify_api_{service}_{type}.md`

## Workflow Orchestration
- Build service dependency hierarchy
- Process levels from consumers to providers
- Consumer expansion mode for defining provider APIs
- Mode determination per API (new/update/consumer_expand/review)
- Development → Self-review → Verification → Issue resolution
- Summary reporting after each API
- Progression through hierarchy levels

## Key Deliverables
- Base configuration (protocol, versioning, auth)
- Endpoint table for quick reference
- Complete endpoint specifications
- Data models and schemas
- Error handling standards
- Integration guides (for public APIs)
- Service discovery info (for internal APIs)
- Consumer requirements matrix (for internal APIs)
- Consumer annotations per endpoint

## Consumer-Driven Order
1. **Level 0**: Public-facing services with external APIs
2. **Level 1**: Pure consumer services (define provider needs)
3. **Level 2+**: Mixed services (both consume and provide)
4. **Bottom**: Core provider services (implement accumulated specs)

## Common Modifications at This Level
- New endpoints or removed endpoints
- Changed request/response formats
- Modified authentication methods
- Different error codes
- New webhook events
- Rate limit adjustments
- Consumer requirement changes

## Important Guidelines
- **Consumer-first design**: Let consumers define what they need
- **No speculation**: Don't guess provider API requirements
- **Incremental building**: APIs grow as consumers define needs
- Not all services need both API types
- Public APIs need comprehensive examples
- Internal APIs built by consumer requirements
- Smart deduplication across consumers
- Document consumer-provider relationships

## Quality Checklist
- All required features have endpoints
- Authentication clearly defined
- Base configuration complete
- Endpoint table accurate
- Data models comprehensive
- Error handling standardized
- Examples helpful
- No functionality duplicated
- Consumer requirements tracked
- Smart duplicate detection working