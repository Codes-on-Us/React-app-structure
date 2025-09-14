
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

### HTTPS Development Setup

For secure local development, use `mkcert` to generate trusted SSL certificates for localhost.

#### Installation

**macOS (using Homebrew):**
```bash
brew install mkcert
```

**Windows (using Chocolatey):**
```bash
choco install mkcert
```

**Linux (using wget):**
```bash
wget -O mkcert https://github.com/FiloSottile/mkcert/releases/download/v1.4.4/mkcert-v1.4.4-linux-amd64
chmod +x mkcert
sudo mv mkcert /usr/local/bin/
```

#### Generate Certificates

```bash
# Install the local CA
mkcert -install

# Generate certificate for localhost
mkcert localhost 127.0.0.1 ::1
```

This creates two files:
- `localhost+2.pem` (certificate)
- `localhost+2-key.pem` (private key)

#### Package.json Configuration

```json
{
  "scripts": {
    "start": "react-scripts start",
    "start:https": "HTTPS=true SSL_CRT_FILE=localhost+2.pem SSL_KEY_FILE=localhost+2-key.pem react-scripts start",
    "dev": "npm run start:https"
  }
}
```

**For Windows users:**
```json
{
  "scripts": {
    "start": "react-scripts start",
    "start:https": "set HTTPS=true && set SSL_CRT_FILE=localhost+2.pem && set SSL_KEY_FILE=localhost+2-key.pem && react-scripts start",
    "dev": "npm run start:https"
  }
}
```

#### Usage

```bash
# Start development server with HTTPS
npm run dev

# Your app will be available at: https://localhost:3000
```

**Benefits:**
- ✅ Trusted certificates (no browser warnings)
- ✅ Test HTTPS-only features (Service Workers, Web APIs)
- ✅ Match production environment behavior
- ✅ Required for some modern web APIs

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

#### String Interpolation Safety
Always handle null and undefined values when using variables in string interpolation to prevent displaying "null" or "undefined" in UI.

**Safe String Interpolation:**
- Use optional chaining and nullish coalescing
- Provide fallback values for null/undefined variables
- Validate data before string interpolation

```typescript
// ❌ Bad - Can display "null" or "undefined" in UI
const UserGreeting: React.FC<{ user: User }> = ({ user }) => {
  return (
    <div>
      <h1>Welcome ${user.firstName} ${user.lastName}!</h1>
      <p>Email: ${user.email}</p>
      <p>Phone: ${user.phone}</p>
    </div>
  );
};

// ❌ Bad - Template literal with potential null/undefined
const message = `Hello ${user.name}, your balance is ${user.account.balance}`;

// ✅ Good - Safe string interpolation with fallbacks
const UserGreeting: React.FC<{ user: User }> = ({ user }) => {
  return (
    <div>
      <h1>Welcome {user.firstName ?? ""} {user.lastName ?? ""}!</h1>
      <p>Email: {user.email ?? 'Not provided'}</p>
      <p>Phone: {user.phone ?? 'Not available'}</p>
    </div>
  );
};

// ✅ Good - Safe template literals
const message = `Hello ${user.name ?? ""}, your balance is ${user.account?.balance ?? "0.00"}`;

// ✅ Good - Simple empty string fallback to avoid displaying null/undefined
const displayName = `${user.firstName ?? ""} ${user.lastName ?? ""}`.trim();
const userInfo = `Name: ${user.name ?? ""} | Email: ${user.email ?? ""}`;

// ✅ Good - Using utility function for safe string formatting
const formatUserName = (firstName?: string, lastName?: string): string => {
  const first = firstName?.trim() || '';
  const last = lastName?.trim() || '';
  return [first, last].filter(Boolean).join(' ') || 'Guest';
};

const UserGreeting: React.FC<{ user: User }> = ({ user }) => {
  return (
    <div>
      <h1>Welcome {formatUserName(user.firstName, user.lastName)}!</h1>
      <p>Email: {user.email || 'Not provided'}</p>
    </div>
  );
};
```

**Best Practices for String Safety:**
- **Use nullish coalescing (`??`)** for default values
- **Use optional chaining (`?.`)** for nested properties
- **Create utility functions** for complex string formatting
- **Validate data types** before string operations
- **Use TypeScript strict mode** to catch potential null/undefined issues

#### State Management - Avoid Prop Drilling
Don't pass React state through multiple nested components. Instead, use Redux slices or global state management for shared data.

**Use Redux Slices Instead of Prop Drilling:**
- Store shared state in Redux slices
- Use selectors to access state in components
- Avoid passing state through multiple component levels
- Keep components decoupled from parent state

```typescript
// ❌ Bad - Passing state through multiple nested components
const App: React.FC = () => {
  const [user, setUser] = useState<User | null>(null);
  const [orders, setOrders] = useState<Order[]>([]);
  const [notifications, setNotifications] = useState<Notification[]>([]);

  return (
    <Dashboard
      user={user}
      orders={orders}
      notifications={notifications}
      onUpdateUser={setUser}
    />
  );
};

const Dashboard: React.FC<DashboardProps> = ({ user, orders, notifications, onUpdateUser }) => {
  return (
    <div>
      <Header user={user} notifications={notifications} />
      <Sidebar user={user} />
      <MainContent user={user} orders={orders} onUpdateUser={onUpdateUser} />
    </div>
  );
};

const MainContent: React.FC<MainContentProps> = ({ user, orders, onUpdateUser }) => {
  return (
    <div>
      <UserProfile user={user} onUpdateUser={onUpdateUser} />
      <OrderList orders={orders} user={user} />
    </div>
  );
};

// ✅ Good - Using Redux slices for shared state
// store/userSlice.ts
export const userSlice = createSlice({
  name: 'user',
  initialState: { user: null as User | null },
  reducers: {
    setUser: (state, action) => {
      state.user = action.payload;
    }
  }
});

// store/ordersSlice.ts
export const ordersSlice = createSlice({
  name: 'orders',
  initialState: { orders: [] as Order[] },
  reducers: {
    setOrders: (state, action) => {
      state.orders = action.payload;
    }
  }
});

// Components access state directly without prop drilling
const App: React.FC = () => {
  return <Dashboard />;
};

const Dashboard: React.FC = () => {
  return (
    <div>
      <Header />
      <Sidebar />
      <MainContent />
    </div>
  );
};

const UserProfile: React.FC = () => {
  const user = useSelector((state: RootState) => state.user.user);
  const dispatch = useDispatch();

  const handleUpdateUser = (userData: User) => {
    dispatch(userSlice.actions.setUser(userData));
  };

  return <div>{/* User profile UI */}</div>;
};

const OrderList: React.FC = () => {
  const orders = useSelector((state: RootState) => state.orders.orders);
  const user = useSelector((state: RootState) => state.user.user);

  return <div>{/* Order list UI */}</div>;
};
```

**Benefits of Using Redux Slices:**
- **No Prop Drilling**: Components access state directly
- **Better Performance**: Components only re-render when their specific state changes
- **Cleaner Code**: Less prop passing and interface definitions
- **Maintainability**: Easier to add/remove state without changing component signatures
- **Testability**: Components can be tested independently of parent state

