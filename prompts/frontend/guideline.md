# Frontend Architecture Output Guidelines

## Architecture Design Principles

### Complexity-Based Design
The frontend architecture must align with the PRD complexity score:
- **0-3 (Simple)**: Minimal structure, direct implementation
- **4-7 (Standard)**: Component-based with clear separation
- **8-10 (Complex)**: Full architectural patterns with advanced features

### API-First Approach
- Architecture driven by available backend APIs
- Design components around API endpoints
- Plan data flow based on API responses
- Consider API limitations in UI design

### User Story Alignment
- Every UI component maps to user stories
- Navigation reflects user workflows
- Features prioritized by story importance
- Accessibility included from the start

## Document Structure

### Frontend Architecture (`workspace/output/frontend/architecture.md`)

#### 1. Executive Summary
Brief overview of the frontend approach (3-4 lines):
- Chosen framework and justification
- Architecture pattern (SPA, SSR, SSG, PWA)
- Key design decisions
- Target platforms

#### 2. Technology Stack
List all major technologies with justification:
```markdown
## Technology Stack

### Core Framework
- **Framework**: [React/Vue/Angular/Vanilla]
- **Version**: [Specific version]
- **Justification**: [Why this choice for this complexity]

### Build Tools
- **Bundler**: [Vite/Webpack/Parcel]
- **Package Manager**: [npm/yarn/pnpm]
- **TypeScript**: [Yes/No and why]

### Styling
- **CSS Framework**: [Tailwind/Bootstrap/Material-UI/Custom]
- **CSS-in-JS**: [If applicable]
- **Design System**: [Custom/Third-party]

### State Management
- **Solution**: [Redux/Pinia/Context/Zustand]
- **Async State**: [React Query/SWR/Apollo]

### Testing
- **Unit Tests**: [Jest/Vitest]
- **E2E Tests**: [Cypress/Playwright]
- **Component Tests**: [Testing Library]
```

#### 3. Architecture Overview
High-level architecture diagram and explanation:
```markdown
## Architecture Overview

### Pattern
[SPA/MPA/SSR/SSG/PWA] architecture with [describe key characteristics]

### Diagram
\```mermaid
graph TB
    subgraph "Frontend Application"
        UI[UI Components]
        State[State Management]
        Router[Router]
        API[API Client]
    end
    
    subgraph "Backend Services"
        Gateway[API Gateway]
        Services[Microservices]
    end
    
    UI --> State
    UI --> Router
    State --> API
    API --> Gateway
    Gateway --> Services
\```

### Data Flow
[Describe how data flows through the application]
```

#### 4. Component Architecture
Detailed component hierarchy and organization:
```markdown
## Component Architecture

### Component Hierarchy
\```
App
├── Layout
│   ├── Header
│   │   ├── Navigation
│   │   └── UserMenu
│   ├── Sidebar
│   └── Footer
├── Pages
│   ├── HomePage
│   ├── DashboardPage
│   └── [Other Pages]
├── Features
│   ├── Authentication
│   ├── [Feature Modules]
│   └── [Domain Components]
└── Shared
    ├── UIComponents
    ├── Hooks
    └── Utils
\```

### Component Categories
- **Layout Components**: Application structure
- **Page Components**: Route-level components  
- **Feature Components**: Business logic components
- **UI Components**: Reusable presentation components
- **Utility Components**: HOCs, providers, guards
```

#### 5. State Management
State management strategy and data flow:
```markdown
## State Management

### Strategy
[Describe overall approach]

### State Structure
\```typescript
interface AppState {
  auth: AuthState;
  user: UserState;
  [domain]: DomainState;
  ui: UIState;
}
\```

### State Categories
- **Local State**: Component-specific state
- **Global State**: Application-wide state
- **Server State**: Cached API responses
- **Form State**: Form data and validation
- **UI State**: Modals, notifications, loading
```

#### 6. API Integration
How the frontend integrates with backend services:
```markdown
## API Integration

### API Client Architecture
- **Base Client**: [Axios/Fetch/Generated SDK]
- **Request Interceptors**: [Auth, logging, retry]
- **Response Interceptors**: [Error handling, transformation]

### Service Layer
\```typescript
services/
├── api/
│   ├── client.ts
│   ├── auth.service.ts
│   └── [domain].service.ts
├── models/
└── validators/
\```

### Data Fetching Patterns
- **Pattern**: [REST/GraphQL/RPC]
- **Caching**: [Strategy and TTL]
- **Optimistic Updates**: [Yes/No]
- **Real-time**: [WebSockets/SSE if needed]
```

#### 7. Routing Structure
Application routing and navigation:
```markdown
## Routing Structure

### Route Definition
\```typescript
const routes = [
  { path: '/', component: HomePage, public: true },
  { path: '/dashboard', component: Dashboard, protected: true },
  { path: '/[feature]', component: FeaturePage, protected: true },
];
\```

### Navigation Patterns
- **Public Routes**: [List accessible without auth]
- **Protected Routes**: [List requiring auth]
- **Nested Routes**: [Describe hierarchy]
- **Dynamic Routes**: [Parameter-based routes]
```

#### 8. Authentication & Authorization
Security implementation:
```markdown
## Authentication & Authorization

### Authentication Flow
1. [Login process]
2. [Token management]
3. [Session handling]
4. [Logout process]

### Authorization
- **Role-Based**: [If applicable]
- **Permission-Based**: [If applicable]
- **Route Guards**: [Implementation]
- **Component Guards**: [Conditional rendering]
```

#### 9. Performance Strategy
Performance optimization approach:
```markdown
## Performance Strategy

### Optimization Techniques
- **Code Splitting**: [Route-based/Component-based]
- **Lazy Loading**: [Images, components, routes]
- **Bundle Optimization**: [Tree shaking, minification]
- **Caching**: [Service worker, HTTP cache]

### Performance Targets
- **First Contentful Paint**: < [X]ms
- **Time to Interactive**: < [X]s
- **Bundle Size**: < [X]KB
- **Lighthouse Score**: > [X]
```

#### 10. Responsive Design
Multi-device support strategy:
```markdown
## Responsive Design

### Breakpoints
- **Mobile**: 320px - 767px
- **Tablet**: 768px - 1023px  
- **Desktop**: 1024px - 1439px
- **Large**: 1440px+

### Approach
- **Mobile-First**: [Yes/No]
- **Adaptive**: [Specific layouts per device]
- **Fluid**: [Flexible sizing]
```

#### 11. Build Configuration
Build and deployment setup:
```markdown
## Build Configuration

### Build Process
\```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "test": "vitest",
    "lint": "eslint"
  }
}
\```

### Environment Configuration
- **Development**: Local development settings
- **Staging**: Pre-production testing
- **Production**: Live environment
```

#### 12. Testing Strategy
Testing approach and coverage:
```markdown
## Testing Strategy

### Test Pyramid
- **Unit Tests**: 70% (business logic, utilities)
- **Integration Tests**: 20% (API, state)
- **E2E Tests**: 10% (critical user flows)

### Coverage Targets
- **Statements**: > 80%
- **Branches**: > 75%
- **Functions**: > 80%
- **Lines**: > 80%
```

#### 13. Deployment Architecture
Deployment and hosting strategy:
```markdown
## Deployment Architecture

### Hosting
- **Platform**: [Vercel/Netlify/AWS/Custom]
- **CDN**: [CloudFlare/Fastly/CloudFront]
- **Domains**: [Production, staging URLs]

### CI/CD Pipeline
1. Code push to repository
2. Run tests and linting
3. Build application
4. Deploy to environment
5. Run smoke tests
```

#### 14. Development Guidelines
Standards and best practices:
```markdown
## Development Guidelines

### Code Standards
- **Style Guide**: [Airbnb/Standard/Custom]
- **Linting**: ESLint configuration
- **Formatting**: Prettier configuration

### Component Guidelines
- **Naming**: PascalCase for components
- **Structure**: Consistent file organization
- **Props**: TypeScript interfaces
- **Hooks**: Custom hooks for logic reuse

### Git Workflow
- **Branching**: [GitFlow/GitHub Flow]
- **Commits**: [Conventional Commits]
- **PRs**: [Review requirements]
```

## Preferences Document Structure

### Frontend Preferences (`workspace/output/frontend/preferences.md`)

Track all architectural decisions:
```markdown
# Frontend Architecture Preferences

## Framework Decision
- **Choice**: [Framework]
- **Alternatives Considered**: [List]
- **Decision Factors**: [Complexity, team experience, ecosystem]

## State Management Decision
- **Choice**: [Solution]
- **Rationale**: [Why this approach]

## Styling Decision
- **Choice**: [CSS solution]
- **Rationale**: [Why this approach]

## Build Tool Decision
- **Choice**: [Bundler]
- **Rationale**: [Speed, features, compatibility]

## Component Library Decision
- **Build vs Buy**: [Custom/Third-party]
- **Choice**: [If third-party, which one]
- **Rationale**: [Time, quality, customization]

## Testing Framework Decision
- **Unit Tests**: [Framework]
- **E2E Tests**: [Framework]
- **Rationale**: [Features, speed, ecosystem]

## Deployment Platform Decision
- **Choice**: [Platform]
- **Rationale**: [Cost, features, scalability]
```

## Quality Checklist

Before finalizing frontend architecture:
- [ ] Framework appropriate for complexity score
- [ ] All API endpoints have integration patterns
- [ ] Component hierarchy is logical and scalable
- [ ] State management supports all features
- [ ] Routing covers all user stories
- [ ] Authentication flow is secure
- [ ] Performance targets are defined
- [ ] Responsive design strategy is clear
- [ ] Build configuration is optimized
- [ ] Testing strategy is comprehensive
- [ ] Deployment process is defined
- [ ] Development guidelines are clear
- [ ] All decisions are documented in preferences

## Update Guidelines

When updating existing frontend architecture:
- Preserve working patterns that meet requirements
- Document reasons for architectural changes
- Ensure changes don't break existing features
- Update preferences with new decisions
- Consider migration path for breaking changes
- Update all affected documentation sections