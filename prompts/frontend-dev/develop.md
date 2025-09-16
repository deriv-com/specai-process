# Frontend Development Implementation

## Goal
Implement the complete frontend application based on frontend architecture and UI specifications, translating designs into working code that integrates with backend APIs.

## Operational Modes

### Mode Detection
First, check if implementation exists in `workspace/code/frontend/`:
- **EXISTS**: Enter `update` or `review` mode based on task
- **DOES NOT EXIST**: Enter `new` mode

## Preparation

### PREFERENCE HIERARCHY (Check in this order)
1. **Workspace Preferences** (`workspace/preferences.md`):
   - Check if exists: Contains overarching defaults for this workspace
   - Use for: Testing frameworks, code organization, build optimization
   - Persists across project resets
2. **Phase Preferences** (`workspace/code/frontend/preferences.md`):
   - Always check: Contains frontend development-specific decisions
   - Has highest precedence for conflicts
   - Gets cleared on project resets

**IMPORTANT**: When making frontend implementation decisions, check preferences in order: Workspace → Phase. Use the most specific preference found.


### Required Reading
1. **INSTRUCTION FILES**
   - `workspace/output/frontend/architecture.md`: Technology stack and patterns
   - `workspace/output/frontend/ui/`: All UI specifications
   - `prompts/frontend-dev/guideline.md`: Development standards

2. **API SPECIFICATIONS**
   - Read all public APIs from `workspace/output/api/*_public.md`
   - Note authentication requirements
   - Understand data models

3. **EXISTING WORK** (for update/review modes)
   - `workspace/code/frontend/`: Current implementation
   - `workspace/code/frontend/preferences.md`: Previous decisions

## Mode: New

### Step 1: Project Setup
Based on architecture complexity:

#### Simple (0-3)
```bash
workspace/code/frontend/
├── index.html
├── styles.css
├── script.js
└── README.md
```

#### Standard (4-7)
```bash
# React/Vue project structure
workspace/code/frontend/
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── hooks/ (React) or composables/ (Vue)
│   ├── utils/
│   ├── App.jsx/vue
│   └── main.jsx/js
├── public/
├── package.json
├── vite.config.js
└── README.md
```

#### Complex (8-10)
```bash
# Next.js/Nuxt structure
workspace/code/frontend/
├── src/
│   ├── app/ or pages/
│   ├── components/
│   ├── features/
│   ├── services/
│   ├── store/
│   ├── hooks/ or composables/
│   ├── utils/
│   └── types/
├── public/
├── package.json
├── next.config.js or nuxt.config.js
└── README.md
```

### Step 2: Generate API Client SDK

Create API client based on specifications:

```javascript
// src/services/api/client.js
const API_BASE_URL = process.env.NEXT_PUBLIC_API_URL || 'http://localhost:3000';

class ApiClient {
  constructor() {
    this.baseURL = API_BASE_URL;
    this.token = null;
  }

  setAuthToken(token) {
    this.token = token;
  }

  async request(endpoint, options = {}) {
    const url = `${this.baseURL}${endpoint}`;
    const config = {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        ...options.headers,
        ...(this.token && { Authorization: `Bearer ${this.token}` })
      }
    };

    const response = await fetch(url, config);
    
    if (!response.ok) {
      throw new ApiError(response.status, await response.json());
    }
    
    return response.json();
  }

  // Generate methods for each API endpoint
  // Based on API specifications
}

export default new ApiClient();
```

### Step 3: Implement Component Library

Based on UI specifications, create components:

#### Design Tokens
```css
/* src/styles/tokens.css */
:root {
  /* Colors from UI specs */
  --color-primary: #0066CC;
  --color-secondary: #6C757D;
  
  /* Typography from UI specs */
  --font-family: 'Inter', sans-serif;
  --font-size-base: 1rem;
  
  /* Spacing from UI specs */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  /* ... */
}
```

#### Core Components
For each component in UI specs:
```jsx
// src/components/Button/Button.jsx
import styles from './Button.module.css';

const Button = ({ 
  variant = 'primary',
  size = 'medium',
  loading = false,
  disabled = false,
  onClick,
  children,
  ...props 
}) => {
  const className = `
    ${styles.button}
    ${styles[variant]}
    ${styles[size]}
    ${loading ? styles.loading : ''}
  `;

  return (
    <button
      className={className}
      disabled={disabled || loading}
      onClick={onClick}
      aria-busy={loading}
      {...props}
    >
      {loading && <Spinner />}
      {children}
    </button>
  );
};

export default Button;
```

### Step 4: Implement Pages/Routes

Based on user stories and navigation:

```jsx
// src/pages/Dashboard.jsx
import { useState, useEffect } from 'react';
import { Layout } from '@/components/Layout';
import { DataTable } from '@/components/DataTable';
import api from '@/services/api';

const DashboardPage = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchDashboardData();
  }, []);

  const fetchDashboardData = async () => {
    try {
      const response = await api.getDashboard();
      setData(response);
    } catch (error) {
      console.error('Failed to fetch dashboard:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <Layout>
      <h1>Dashboard</h1>
      {loading ? (
        <LoadingState />
      ) : (
        <DataTable data={data} />
      )}
    </Layout>
  );
};

export default DashboardPage;
```

### Step 5: Implement State Management

Based on architecture decisions:

```javascript
// src/store/auth.js (Zustand example)
import { create } from 'zustand';
import api from '@/services/api';

const useAuthStore = create((set) => ({
  user: null,
  isAuthenticated: false,
  loading: false,
  
  login: async (credentials) => {
    set({ loading: true });
    try {
      const response = await api.login(credentials);
      api.setAuthToken(response.token);
      set({ 
        user: response.user,
        isAuthenticated: true,
        loading: false 
      });
    } catch (error) {
      set({ loading: false });
      throw error;
    }
  },
  
  logout: () => {
    api.setAuthToken(null);
    set({ user: null, isAuthenticated: false });
  }
}));

export default useAuthStore;
```

### Step 6: Implement Authentication

```jsx
// src/components/ProtectedRoute.jsx
import { Navigate } from 'react-router-dom';
import useAuthStore from '@/store/auth';

const ProtectedRoute = ({ children }) => {
  const isAuthenticated = useAuthStore(state => state.isAuthenticated);
  
  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }
  
  return children;
};
```

### Step 7: Add Error Handling

```jsx
// src/components/ErrorBoundary.jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };
  
  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('Error caught:', error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      return <ErrorFallback error={this.state.error} />;
    }
    
    return this.props.children;
  }
}
```

### Step 8: Configure Build

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
      },
    },
  },
});
```

### Step 9: Add Tests

```javascript
// src/components/Button/Button.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import Button from './Button';

describe('Button Component', () => {
  test('renders with text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });
  
  test('calls onClick when clicked', () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click</Button>);
    fireEvent.click(screen.getByText('Click'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
  
  test('is disabled when loading', () => {
    render(<Button loading>Loading</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### Step 10: Create Documentation

```markdown
# Frontend Application

## Setup
\```bash
npm install
npm run dev
\```

## Environment Variables
Create `.env.local`:
\```
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_APP_NAME=MyApp
\```

## Project Structure
[Document the structure]

## Available Scripts
- `npm run dev`: Start development server
- `npm run build`: Build for production
- `npm run test`: Run tests
- `npm run lint`: Lint code

## Component Library
[List components and usage]

## API Integration
[Document API client usage]
```

### Step 11: Create Preferences
Document decisions in `workspace/code/frontend/preferences.md`:
```markdown
# Frontend Development Preferences

## Implementation Decisions
- **Framework**: [Actual choice made]
- **State Management**: [Library used]
- **Routing**: [Solution used]
- **Styling**: [Approach taken]
- **Testing**: [Framework used]

## Patterns Used
- **Component Pattern**: [Functional/Class]
- **State Pattern**: [Local/Global approach]
- **Error Handling**: [Strategy used]

## Performance Optimizations
- **Code Splitting**: [Approach]
- **Lazy Loading**: [Implementation]
- **Caching**: [Strategy]
```

## Mode: Update

### Step 1: Read Current Implementation
- Load existing code structure
- Understand current patterns
- Read preferences

### Step 2: Identify Required Changes
- New features from user stories
- API endpoint changes
- UI specification updates
- Bug fixes needed

### Step 3: Implement Updates
- Add new components
- Update existing components
- Integrate new API endpoints
- Fix identified issues

### Step 4: Update Tests
- Add tests for new features
- Update tests for changes
- Ensure coverage maintained

### Step 5: Update Documentation
- Document new features
- Update environment variables
- Revise setup instructions

## Mode: Review

### Step 1: Interactive Review
Engage with user about:
1. **Code Quality**:
   - Is code maintainable?
   - Following best practices?
   - Performance issues?

2. **Feature Completeness**:
   - All features working?
   - Any missing functionality?
   - Edge cases handled?

3. **User Experience**:
   - Is the UI responsive?
   - Loading states smooth?
   - Error messages helpful?

### Step 2: Document Feedback
Record user feedback and preferences for improvements

## Completion

After implementation:
- Verify all UI specs implemented
- Ensure API integration complete
- Confirm authentication working
- Test responsive behavior
- Report: "development succeeded" or "development failed" with reason

## Important Notes
- Never start from scratch if code exists
- Follow the architecture decisions
- Implement ALL UI specifications
- Include comprehensive error handling
- Optimize for performance
- Write clean, maintainable code