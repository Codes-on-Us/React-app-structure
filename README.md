
## **React app sructure**

      
    src/
    ├─  assets/           
    │   ├─ images/              # image files
    │   ├─ fonts/               # font files
    │   └─ global.css           # global styles
    │
    ├─  components/             # reusable UI primitives
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
    │
    ├─  pages/                  # route-level modules (one folder per route)
    │   ├─  HomePage/            
    │   │   ├─ HomePage.js      # entry component
    │   │   ├─ HomePage.test.js
    │   │   ├─ HomePage.actions.js     
    │   │   ├─ HomePage.module.scss  
    │   │   ├─ modules /        # sub-components for home
    │   │   │   ├─ HeroBanner.js 
    │   │   |   ├─ HeroBanner.module.scss    
    │   │   │   └─ FeaturedList.js
    ├─  utils /                  # app-wide helpers & constants
    │   ├─ formatDate.js         
    │   ├─ apiClient.js          
    │   └─ constants.js          
    │
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
