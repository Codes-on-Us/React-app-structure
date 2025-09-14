
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

```typescript
// ✅ Good - Descriptive naming
const userAuthToken = getAuthToken();
const isUserLoggedIn = checkAuthStatus();
const hasUserPermission = validateUserAccess();
const canUserEditProfile = checkEditPermissions();

const handleUserProfileUpdate = (userData: User) => { ... };
const fetchUserOrderHistory = async (userId: string) => { ... };

// ❌ Bad - Generic, unclear naming
const token = getToken();
const status = check();
const flag = validate();

const handle = (data: any) => { ... };
const fetch = async (id: string) => { ... };
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

