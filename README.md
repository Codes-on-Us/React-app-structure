
# React TypeScript App Structure & Clean Code Guidelines

## **React app sructure**


    src/
    ├─  assets/
    │   ├─ images/              # image files
    │   ├─ fonts/               # font files
    │   └─ global.css           # global styles
    │
    ├─  UIComponents/           # reusable UI primitives
    │   ├─  Button/
    │   │   ├─ Button.js
    │   │   ├─ Button.test.js
    │   │   ├─ Button.module.css
    │   │   └─ Button.stories.js
    │   └─  index.js             # barrel export
    │
    ├─  layouts/                 # master page shells + layout-specific features
    │   ├─  AdminLayout/
    │   │   ├─  AdminLayout.js
    │   │   ├─  AdminLayout.test.js
    │   │   ├─  AdminLayout.css
    │   │   └─  features/        # AdminLayout-specific UI bits
    │   │       ├─ SidebarLinks.js
    │   │       ├─ UserMenu.js
    │   │       └─ NotificationsBell.js
    │   │
    │   └─  LoginLayout/
    │       ├─ LoginLayout.js
    │       ├─ LoginLayout.test.js
    │       ├─ LoginLayout.css
    │       └─ features/        # LoginLayout-specific UI bits
    │           ├─ LoginForm.js
    │           ├─ OAuthButtons.js
    │           └─ ForgotPasswordLink.js
    │
    ├─  store/                  # Redux Toolkit setup & slices
    │   ├─ index.js             # configureStore + root reducer
    │   ├─ authSlice.js
    │   ├─ dashboardSlice.js
    │   └─ middleware.js
    ├─  Components/             # common components
    ├─  pages/                  # route-level modules (one folder per route)
    │   ├─  HomePage/
    │   │   ├─ HomePage.tsx      # entry component
    │   │   ├─ HomePage.test.ts
    │   │   ├─ HomePage.module.scss
    │   │   ├─ Stores/          # Redux slices
	│   │   ├─ Types/
    │   │   ├─ logic/           # page-specific business logic & custom hooks
    │   │   │   ├─ useHomePage.ts
    │   │   │   └─ useHomeData.ts
    │   │   ├─ utils/           # page-specific utilities & helpers
    │   │   │   ├─ homeHelpers.ts
    │   │   │   └─ homeValidation.ts
    │   │   ├─ Components /     # sub-components for home
    │   │   │   ├─ HeroBanner.ts
    │   │   |   ├─ HeroBanner.module.scss
    │   │   │   └─ FeaturedList.ts
    ├─  Hooks /
	├─  utils /                  # app-wide helpers & constants
    │   ├─ Extensions/
    │   ├─ data/                 # static data
    |   |   ├─ countryList.ts     
    |   |   └─ staticData.ts
    │   ├─ Assistances /
    │   ├─ formatDate.ts
    │   ├─ apiClient.ts
    │   └─ constants.ts
    ├─ Types/           #shared and global types
    │   ├── Auth/
    │   │   ├── dto.ts
    │   │   ├── model.ts
    │   │   └── index.ts
    │   ├── User/
    │   │   ├── permissions.ts
    │   │   ├── profile.ts
    │   │   └── index.ts
    ├─ i18n/                    # internationalization setup
    │   ├─ index.ts            # i18n configuration
    │   ├─ locales/            # translation files
    │   │   ├─ en/
    │   │   │   ├─ common.json
    │   │   │   ├─ auth.json
    │   │   │   └─ dashboard.json
    │   │   ├─ es/
    │   │   │   ├─ common.json
    │   │   │   ├─ auth.json
    │   │   │   └─ dashboard.json
    │   │   └─ fr/
    │   │       ├─ common.json
    │   │       ├─ auth.json
    │   │       └─ dashboard.json
    │   └─ utils/
    │       ├─ detectLanguage.ts
    │       └─ formatters.ts
    ├─  App.ts                   # application shell: router + providers
    └─  index.ts                 # ReactDOM.render + global CSS imports



### Absolute Imports

Instead of using relative imports like this:

    import  { Button }  from  "../../ui/button";

Use absolute imports to avoid guesswork and simplify refactoring:

    import  { Button }  from  "@features/ui/button";

Set up absolute imports with a  `jsconfig.json`  or  `tsconfig.json`  file.

    {
      "compilerOptions":  {
      "baseUrl":  ".",
      "paths":  {
	      "@features/*":  ["src/features/*"]
			}
		}
    }


### branches

![Branchs Approach
](https://raw.githubusercontent.com/Codes-on-Us/React-app-structure/refs/heads/main/branchsApproach.png)

### New future

 1. Clone live branch
 2. Template for branch name : {Task number} - {Task title}
 3. Move task to test column or add test tag to test by tester.



### Clean Code Principles

#### Single Responsibility Principle
Each file should contain only one class or one function component. Avoid placing multiple function components in a single file to maintain clarity and improve maintainability.

```typescript
// ✅ Good - One component per file
// UserProfile.tsx
export const UserProfile: React.FC<UserProfileProps> = ({ user }) => {
  return <div>{user.name}</div>;
};

// ❌ Bad - Multiple components in one file
// UserComponents.tsx
export const UserProfile = ({ user }) => <div>{user.name}</div>;
export const UserList = ({ users }) => <div>{users.length}</div>;
export const UserCard = ({ user }) => <div>{user.email}</div>;
```

#### Type Safety and Organization
- Store all types in the correct location within the `Types/` directory structure
- Use proper TypeScript types throughout the project
- **Never use `any` type** - always define specific interfaces and types
- Import types from their designated locations using absolute imports

```typescript
// ✅ Good - Proper type usage
import { User } from '@/Types/User';
import { ApiResponse } from '@/Types/Api';

interface UserProfileProps {
  user: User;
  onUpdate: (user: User) => Promise<ApiResponse<User>>;
}

// ❌ Bad - Using any type
interface UserProfileProps {
  user: any;
  onUpdate: (user: any) => any;
}
```

#### Naming Conventions
Use clear, descriptive, and consistent naming conventions throughout the project to improve code readability and maintainability.

**Components & Files:**
- Use PascalCase for component names and file names
- Use descriptive names that clearly indicate the component's purpose
- Avoid abbreviations and generic names

```typescript
// ✅ Good - Clear, descriptive names
UserProfileCard.tsx
OrderConfirmationModal.tsx
ProductCatalogFilter.tsx

// ❌ Bad - Unclear, abbreviated names
UPC.tsx
Modal.tsx
Filter.tsx
```

**Variables & Functions:**
- Use camelCase for variables, functions, and methods
- Use descriptive names that explain what the variable holds or what the function does
- Boolean variables should start with `is`, `has`, `can`, or `should`
- Custom hooks must start with `use` prefix

```typescript
// ✅ Good - Descriptive naming
const userAuthToken = getAuthToken();
const isUserLoggedIn = checkAuthStatus();
const hasUserPermission = validateUserAccess();
const canUserEditProfile = checkEditPermissions();

const handleUserProfileUpdate = (userData: User) => { ... };
const fetchUserOrderHistory = async (userId: string) => { ... };

// ✅ Good - Custom hooks with 'use' prefix
const useUserAuth = () => { ... };
const useApiRequest = (url: string) => { ... };
const useLocalStorage = (key: string) => { ... };

// ❌ Bad - Generic, unclear naming
const token = getToken();
const status = check();
const flag = validate();

const handle = (data: any) => { ... };
const fetch = async (id: string) => { ... };

// ❌ Bad - Custom hooks without 'use' prefix
const userAuth = () => { ... };
const apiRequest = (url: string) => { ... };
```

**Constants & Enums:**
- Use UPPER_SNAKE_CASE for constants
- Use PascalCase for enums with descriptive names

```typescript
// ✅ Good - Clear constant and enum naming
const API_BASE_URL = 'https://api.example.com';
const MAX_RETRY_ATTEMPTS = 3;
const DEFAULT_PAGE_SIZE = 20;

enum UserRole {
  ADMIN = 'admin',
  MODERATOR = 'moderator',
  USER = 'user'
}

enum OrderStatus {
  PENDING = 'pending',
  PROCESSING = 'processing',
  SHIPPED = 'shipped',
  DELIVERED = 'delivered'
}

// ❌ Bad - Generic naming
const URL = 'https://api.example.com';
const MAX = 3;

enum Status {
  A = 'admin',
  M = 'moderator',
  U = 'user'
}
```

#### Separation of Concerns - UI Logic
Keep complex business logic separate from UI components to maintain clean, testable, and maintainable code.

**Extract Complex Logic from Components:**
- Move business logic to custom hooks
- Use utility functions for data processing
- Keep components focused on rendering and user interactions
- Separate API calls from UI components

```typescript
// ❌ Bad - Complex logic mixed with UI
const UserProfile: React.FC = () => {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (formData: FormData) => {
    setLoading(true);
    try {
      // Complex validation logic
      if (!formData.email || !formData.email.includes('@')) {
        throw new Error('Invalid email');
      }
      if (formData.password.length < 8) {
        throw new Error('Password too short');
      }

      // API call logic
      const response = await fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(formData)
      });

      if (!response.ok) throw new Error('Failed to update');
      const updatedUser = await response.json();
      setUser(updatedUser);

      // Complex data transformation
      const processedData = {
        ...updatedUser,
        fullName: `${updatedUser.firstName} ${updatedUser.lastName}`,
        isVerified: updatedUser.emailVerified && updatedUser.phoneVerified
      };

    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  return <form onSubmit={handleSubmit}>{/* UI code */}</form>;
};

// ✅ Good - Separated concerns
// Custom hook for business logic
const useUserProfile = () => {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(false);

  const updateUser = async (formData: FormData) => {
    setLoading(true);
    try {
      const validatedData = validateUserData(formData);
      const updatedUser = await userService.updateUser(validatedData);
      const processedUser = transformUserData(updatedUser);
      setUser(processedUser);
    } catch (error) {
      handleUserError(error);
    } finally {
      setLoading(false);
    }
  };

  return { user, loading, updateUser };
};

// UI Component - focused only on rendering
const UserProfile: React.FC = () => {
  const { user, loading, updateUser } = useUserProfile();

  return (
    <form onSubmit={updateUser}>
      {loading ? <LoadingSpinner /> : <UserForm user={user} />}
    </form>
  );
};

// Separate utility functions
const validateUserData = (formData: FormData): ValidatedUserData => {
  // Validation logic
};

const transformUserData = (user: User): ProcessedUser => {
  // Data transformation logic
};
```

**Benefits of Separating UI Logic:**
- **Testability**: Business logic can be tested independently
- **Reusability**: Custom hooks can be shared across components
- **Maintainability**: Changes to logic don't affect UI structure
- **Readability**: Components are easier to understand and debug

