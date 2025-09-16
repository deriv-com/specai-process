# API Specification Output Guidelines

## API Design Principles

### API Types
- **Public APIs**: Design for external consumers (web apps, mobile apps, third parties)
- **Internal APIs**: Design for service-to-service communication

### Base Configuration
- Base URL, protocol (REST, RPC), content types, versioning
- Authentication & Authorization approach
- Error handling standards

### Feature Extraction Requirements
Before proceeding with implementation, perform systematic feature extraction:

#### For Public APIs
- Extract ALL features from the PRD and frontend features that this service should expose publicly
- Map UI features to specific API endpoints
- Consider mobile app and third-party integration needs
- Create a list of features and propose specific API endpoints (Method + Path)

#### For Internal APIs
- Read the Inter-Service Communication Matrix from `workspace/output/architecture/architecture.md`
- Extract ALL requirements where this service is the provider
- Read consumer service architectures to understand their context
- Map each required capability to specific internal API endpoints
- Ensure ALL consumer-defined requirements are addressed
- Create a list of required services and propose specific API endpoints

#### Endpoint Coverage Confirmation
- Review proposed endpoints against extracted features
- Ensure comprehensive coverage of all identified needs
- Verify alignment with service boundaries and responsibilities
- Confirm no functionality is duplicated or missing

## Document Structure

### Core Sections (Required for All APIs)

#### Overview
Brief statement of the API's purpose, scope, and target consumers

#### Authentication & Authorization
- For public APIs: OAuth, API keys, JWT tokens, etc.
- For internal APIs: Service-to-service authentication approach

#### Base Configuration
- Base URL
- Protocol (REST, RPC)
- Content types
- Versioning strategy

#### Table of Endpoints
Quick-reference table with:
| Method | Path | Summary |
|--------|------|---------|

#### Endpoints & Methods
For each endpoint include:
- Unique endpoint ID: `API-[SERVICE]-[3CHAR]` where:
  - SERVICE: Two-letter code for the service (e.g., AC for Accounts, TR for Trading, MK for Market)
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
  - Examples: API-AC-R4K (accounts API endpoint), API-TR-N7P (trading API endpoint)
- URI path and HTTP method
- Purpose and request/response schemas
- Success/error responses
- One example request/response (not required for every endpoint)

#### Data Models & Schemas
All data structures used in requests/responses

#### Error Handling
- Standard error format
- Error codes must have unique IDs: `ERR-[SERVICE]-[3CHAR]` where:
  - SERVICE: Two-letter code for the service (e.g., AC for Accounts, TR for Trading, MK for Market)
  - 3CHAR: Three random alphanumeric characters (e.g., A1B, X9Z)
  - Examples: ERR-AC-V2L (accounts error), ERR-TR-K8M (trading error)
- Common error codes
- Service-specific codes

### Additional Sections (Based on API Type)

#### For Public APIs Only
- **Integration Guide**: Getting started instructions and best practices
- **Changelog**: Version history and migration notes

#### For Both (If Applicable)
- **Webhooks/Events**: Only if service uses async notification mechanisms

## Special Considerations

### For Public APIs
- Design for external consumers (web apps, mobile apps, third parties)
- Include comprehensive examples and tutorials
- Consider backward compatibility carefully
- Implement proper rate limiting and abuse prevention
- Design for discoverability and ease of use

### For Internal APIs
- Design for service-to-service communication
- Focus on efficiency and performance
- Include service discovery information
- Document SLAs and reliability guarantees
- Consider eventual consistency patterns

## API Design Standards

### RESTful Principles (if using REST)
- Use proper HTTP methods (GET, POST, PUT, DELETE, PATCH)
- Resource-oriented URLs
- Stateless communication
- Proper status codes
- HATEOAS where appropriate

### Request/Response Format
- Consistent field naming conventions
- Standard date/time formats
- Pagination standards
- Filtering and sorting conventions
- Field selection capabilities

### Versioning Strategy
- Version in URL path (e.g., /v1/) or headers
- Deprecation policy
- Migration guides between versions

## Quality Checklist

Before finalizing API specifications:
- [ ] All required features have corresponding endpoints
- [ ] Authentication/authorization is clearly defined
- [ ] Base configuration is complete
- [ ] Endpoint table provides quick reference
- [ ] Each endpoint has complete documentation
- [ ] Data models are comprehensive
- [ ] Error handling is standardized
- [ ] Examples are helpful and accurate
- [ ] For public APIs: Integration guide is included
- [ ] For internal APIs: Service discovery is documented
- [ ] API follows consistent design principles
- [ ] No functionality is duplicated
- [ ] Service boundaries are respected

## Update Guidelines

When updating existing API specifications:
- Maintain existing structure unless changes are necessary
- Preserve valuable existing content that remains accurate
- Add new endpoints or modify existing ones as needed
- Update data models and schemas to reflect current requirements
- Add a note in the changelog section documenting what was modified
- Ensure backward compatibility for public APIs
- Document any breaking changes clearly