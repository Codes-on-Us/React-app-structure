
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
    │   │   ├─ HomePage.js      # entry component
    │   │   ├─ HomePage.test.js
    │   │   ├─ HomePage.actions.js     
    │   │   ├─ HomePage.module.scss
    │   │   ├─ Stores/          # Redux slices
    │   │   ├─ Components /     # sub-components for home
    │   │   │   ├─ HeroBanner.js 
    │   │   |   ├─ HeroBanner.module.scss    
    │   │   │   └─ FeaturedList.js
    ├─  utils /                  # app-wide helpers & constants
    │   ├─ Extensions/
    │   ├─ Assistances /
    │   ├─ formatDate.js         
    │   ├─ apiClient.js          
    │   └─ constants.js          
    ├── types/
    │   ├── Auth/
    │   │   ├── dto.ts
    │   │   ├── model.ts
    │   │   └── index.ts
    │   ├── User/
    │   │   ├── permissions.ts
    │   │   ├── profile.ts
    │   │   └── index.ts
    ├─  App.js                   # application shell: router + providers
    └─  index.js                 # ReactDOM.render + global CSS imports





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
    
