# Frontend Development Output Guidelines

## Development Principles

### Complexity-Based Implementation
The implementation structure must align with PRD complexity score:
- **0-3 (Simple)**: Minimal files, direct implementation
- **4-7 (Standard)**: Component-based, organized structure
- **8-10 (Complex)**: Full modular architecture with advanced patterns

### Architecture Compliance
- Follow the technology stack from frontend architecture
- Implement the component hierarchy as designed
- Use the specified state management approach
- Apply the routing structure defined
- Follow the build configuration specified

### UI Specification Adherence
- Implement ALL components from UI specifications
- Match visual designs exactly
- Include all specified states and variants
- Follow accessibility requirements
- Implement responsive behaviors as specified

## Code Organization Standards

### Directory Structure by Complexity

#### Simple (0-3)
```
frontend/
├── index.html
├── styles.css
├── script.js
├── assets/
│   └── images/
└── README.md
```

#### Standard (4-7)
```
frontend/
├── src/
│   ├── components/
│   │   ├── common/
│   │   ├── layout/
│   │   └── features/
│   ├── pages/
│   ├── services/
│   │   ├── api/
│   │   └── utils/
│   ├── hooks/ or composables/
│   ├── styles/
│   ├── App.jsx
│   └── main.jsx
├── public/
├── tests/
├── package.json
├── vite.config.js
├── .env.example
└── README.md
```

#### Complex (8-10)
```
frontend/
├── src/
│   ├── app/ or pages/
│   ├── components/
│   │   ├── ui/
│   │   ├── layout/
│   │   └── features/
│   ├── features/
│   │   └── [feature]/
│   │       ├── components/
│   │       ├── hooks/
│   │       └── services/
│   ├── services/
│   │   ├── api/
│   │   ├── auth/
│   │   └── utils/
│   ├── store/
│   ├── hooks/ or composables/
│   ├── types/
│   ├── styles/
│   └── config/
├── public/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── package.json
├── next.config.js or nuxt.config.js
├── .env.example
└── README.md
```

## Component Implementation Standards

### Component Structure
```jsx
// Component file structure
import React from 'react'; // or Vue imports
import PropTypes from 'prop-types'; // or TypeScript interfaces
import styles from './Component.module.css';

// Hooks/composables imports
import { useCustomHook } from '@/hooks';

// Component definition
const Component = ({ prop1, prop2, ...props }) => {
  // State management
  const [state, setState] = useState();
  
  // Side effects
  useEffect(() => {
    // Effect logic
  }, [dependencies]);
  
  // Event handlers
  const handleEvent = () => {
    // Handler logic
  };
  
  // Render
  return (
    <div className={styles.container}>
      {/* Component content */}
    </div>
  );
};

// Props validation
Component.propTypes = {
  prop1: PropTypes.string.required,
  prop2: PropTypes.number
};

// Default props
Component.defaultProps = {
  prop2: 0
};

export default Component;
```

### Naming Conventions
- **Components**: PascalCase (e.g., `UserProfile.jsx`)
- **Utilities**: camelCase (e.g., `formatDate.js`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `API_BASE_URL`)
- **CSS Classes**: kebab-case or BEM (e.g., `user-profile__avatar`)
- **Files**: Match component name or use kebab-case for utilities

## API Integration Standards

### API Client Implementation
```javascript
// services/api/client.js
class ApiClient {
  constructor(baseURL) {
    this.baseURL = baseURL;
    this.interceptors = {
      request: [],
      response: []
    };
  }

  // Request method with interceptors
  async request(config) {
    // Apply request interceptors
    let finalConfig = config;
    for (const interceptor of this.interceptors.request) {
      finalConfig = await interceptor(finalConfig);
    }
    
    // Make request
    const response = await fetch(this.baseURL + finalConfig.url, {
      method: finalConfig.method || 'GET',
      headers: finalConfig.headers,
      body: finalConfig.body ? JSON.stringify(finalConfig.body) : undefined
    });
    
    // Apply response interceptors
    let finalResponse = response;
    for (const interceptor of this.interceptors.response) {
      finalResponse = await interceptor(finalResponse);
    }
    
    return finalResponse;
  }
  
  // Convenience methods
  get(url, config) { /* ... */ }
  post(url, data, config) { /* ... */ }
  put(url, data, config) { /* ... */ }
  delete(url, config) { /* ... */ }
}
```

### Service Layer Pattern
```javascript
// services/api/users.service.js
import apiClient from './client';

export const usersService = {
  async getUsers(params) {
    return apiClient.get('/users', { params });
  },
  
  async getUser(id) {
    return apiClient.get(`/users/${id}`);
  },
  
  async createUser(data) {
    return apiClient.post('/users', data);
  },
  
  async updateUser(id, data) {
    return apiClient.put(`/users/${id}`, data);
  },
  
  async deleteUser(id) {
    return apiClient.delete(`/users/${id}`);
  }
};
```

## State Management Standards

### Local State
- Use for component-specific state
- Prefer hooks/composition API
- Keep state close to where it's used

### Global State
- Use for cross-component state
- Follow chosen state management pattern
- Keep stores focused and modular

### Server State
- Cache API responses appropriately
- Implement optimistic updates where suitable
- Handle loading and error states consistently

## Testing Standards

### Unit Tests
```javascript
// Component.test.jsx
describe('Component', () => {
  it('should render correctly', () => {
    const { getByText } = render(<Component prop="value" />);
    expect(getByText('Expected text')).toBeInTheDocument();
  });
  
  it('should handle user interaction', () => {
    const handleClick = jest.fn();
    const { getByRole } = render(<Component onClick={handleClick} />);
    fireEvent.click(getByRole('button'));
    expect(handleClick).toHaveBeenCalled();
  });
});
```

### Integration Tests
- Test API integration
- Test state management flows
- Test routing behavior

### E2E Tests
- Test critical user paths
- Test form submissions
- Test authentication flows

## Performance Standards

### Code Splitting
```javascript
// Lazy load routes
const Dashboard = lazy(() => import('./pages/Dashboard'));

// Lazy load heavy components
const Chart = lazy(() => import('./components/Chart'));
```

### Image Optimization
- Use appropriate formats (WebP, AVIF)
- Implement lazy loading
- Provide responsive images
- Optimize file sizes

### Bundle Optimization
- Tree shaking enabled
- Minimize bundle size
- Extract vendor chunks
- Use production builds

## Security Standards

### Authentication
- Store tokens securely (httpOnly cookies preferred)
- Implement token refresh
- Clear tokens on logout
- Handle token expiration

### Data Protection
- Sanitize user inputs
- Validate data client-side and server-side
- Use HTTPS in production
- Implement CSP headers

### XSS Prevention
- Escape user-generated content
- Use framework's built-in protections
- Avoid dangerouslySetInnerHTML
- Validate and sanitize inputs

## Accessibility Standards

### WCAG Compliance
- Ensure WCAG 2.1 AA compliance minimum
- Test with screen readers
- Verify keyboard navigation
- Check color contrast ratios

### Implementation Requirements
```jsx
// Semantic HTML
<nav role="navigation" aria-label="Main">
  {/* Navigation content */}
</nav>

// ARIA labels
<button aria-label="Close dialog">×</button>

// Focus management
useEffect(() => {
  if (isOpen) {
    dialogRef.current?.focus();
  }
}, [isOpen]);

// Live regions
<div role="alert" aria-live="polite">
  {errorMessage}
</div>
```

## Documentation Standards

### README Requirements
```markdown
# Project Name

## Description
[Brief project description]

## Setup
\```bash
npm install
cp .env.example .env.local
npm run dev
\```

## Environment Variables
- `NEXT_PUBLIC_API_URL`: Backend API URL
- `NEXT_PUBLIC_APP_NAME`: Application name

## Scripts
- `dev`: Start development server
- `build`: Build for production
- `test`: Run tests
- `lint`: Lint code

## Project Structure
[Document structure]

## Key Features
[List main features]

## API Integration
[Document API usage]

## Deployment
[Deployment instructions]
```

### Component Documentation
```jsx
/**
 * Button component with multiple variants and states
 * @param {Object} props - Component props
 * @param {'primary'|'secondary'|'danger'} props.variant - Button variant
 * @param {'small'|'medium'|'large'} props.size - Button size
 * @param {boolean} props.loading - Loading state
 * @param {boolean} props.disabled - Disabled state
 * @param {Function} props.onClick - Click handler
 * @param {ReactNode} props.children - Button content
 * @returns {JSX.Element} Button component
 */
```

## Quality Checklist

Before completing frontend development:
- [ ] All UI specifications implemented
- [ ] API integration complete and working
- [ ] Authentication flows functional
- [ ] State management consistent
- [ ] Routing works correctly
- [ ] Forms validate properly
- [ ] Error handling comprehensive
- [ ] Loading states smooth
- [ ] Responsive design working
- [ ] Accessibility standards met
- [ ] Performance optimized
- [ ] Tests passing
- [ ] Documentation complete
- [ ] Environment variables documented
- [ ] Build process working
- [ ] No console errors in development
- [ ] Security measures in place

## Development Preferences Structure

### Preferences Document (`workspace/code/frontend/preferences.md`)
```markdown
# Frontend Development Preferences

## Technology Choices
- **Framework**: [Actual framework used]
- **State Management**: [Library chosen]
- **Routing**: [Solution implemented]
- **Styling**: [Approach taken]
- **Build Tool**: [Tool used]
- **Testing**: [Frameworks used]

## Implementation Patterns
- **Component Pattern**: [Functional/Class]
- **State Pattern**: [Local/Global strategy]
- **API Pattern**: [Service layer/Direct]
- **Error Pattern**: [Boundary/Try-catch]

## Performance Decisions
- **Code Splitting**: [Strategy]
- **Lazy Loading**: [Approach]
- **Caching**: [Method]
- **Optimization**: [Techniques]

## Development Decisions Log
- **Decision 1**: [What and why]
- **Decision 2**: [What and why]
[Continue as needed]