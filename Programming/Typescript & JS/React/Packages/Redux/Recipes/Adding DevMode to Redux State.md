### 1. **Define Dev State**

Create a separate slice of state or an extended version of your initial state for development purposes.

`// state.ts const initialState = {   user: null,   settings: {     theme: "light",     notifications: true,   },   // Other default state };  const devState = {   user: {     id: "12345",     name: "Dev Tester",     email: "dev@test.com",   },   settings: {     theme: "dark",     notifications: false,   },   // Add other mock data or state goodies };`

---

### 2. **Inject Dev State**

Use a `process.env.NODE_ENV` check or a custom environment variable to decide when to load the dev state.

`const isDevMode = process.env.NODE_ENV === "development";  const preloadedState = isDevMode ? devState : initialState;`

---

### 3. **Configure Store**

Pass the `preloadedState` when creating your Redux store.

`import { configureStore } from '@reduxjs/toolkit'; import rootReducer from './reducers';  const store = configureStore({   reducer: rootReducer,   preloadedState, });  export default store;`

---

### 4. **Add a Toggle (Optional)**

You can add a feature toggle or a dev tools action to switch between states dynamically.

#### Action:

`// devSlice.ts import { createSlice } from '@reduxjs/toolkit';  const devSlice = createSlice({   name: 'dev',   initialState: initialState,   reducers: {     loadDevState: () => devState,     resetState: () => initialState,   }, });  export const { loadDevState, resetState } = devSlice.actions; export default devSlice.reducer;`

#### Usage in Component:

`import { useDispatch } from 'react-redux'; import { loadDevState, resetState } from './devSlice';  const DevTools = () => {   const dispatch = useDispatch();    return (     <div>       <button onClick={() => dispatch(loadDevState())}>Load Dev State</button>       <button onClick={() => dispatch(resetState())}>Reset State</button>     </div>   ); };`

---

### 5. **Party Goodies**

Fill the dev state with mock data like:

- Fake users
- Pre-configured settings
- Sample tasks, notifications, or whatever your app handles

For instance:

`const devState = {   user: {     id: "12345",     name: "Dev Mode Hero",     email: "hero@devmode.com",   },   tasks: [     { id: "task1", title: "Fix all bugs 🐛", completed: false },     { id: "task2", title: "Refactor Redux state", completed: true },   ], };`


## Alternate/Advanced Configurations:
## To Always have the devMode show in the store
	- in slice
```
const devModeSlice = createSlice({
	name: 'devMode', initialState: {
		devMode: false, ...initialState
	}, 
	reducers: { 
	enableDevMode(state) { 
		state.devMode = true; 
		Object.assign(state, devState); // Merge devState into the current state
	},
	disableDevMode(state) { 
		state.devMode = false; 
		Object.assign(state, initialState); // Reset to initial state 
	}, 
}, });
```
	- in store
```const store = configureStore({ reducer: { devMode: devModeReducer, // Other reducers... }, });
```
## Only show devMode in dev environment
	Add this to the top of the redux slice
	
		`const isDevEnvironment = process.env.NODE_ENV === "development";`
	- inside the reducer function, add the check for devEnv
	
	enableDevMode(state) { 
	if (!isDevEnvironment) return; // Ensure this is a no-op outside development
		state.devMode = true; 
		Object.assign(state, devState); // Merge devState into the current state
	},

### Ensure root reducer
	```
	// store.ts
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './reducers'; // Your other reducers
import devModeReducer from './devModeSlice';

const isDevEnvironm
ent = process.env.NODE_ENV === "development";

const store = configureStore({
  reducer: {
    ...rootReducer,
    ...(isDevEnvironment && { devMode: devModeReducer }), // Add devMode reducer only in development
  },
});

export default store;

### Toggle DevMode

```
import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { enableDevMode, disableDevMode } from './devModeSlice';

const DevTools = () => {
  const dispatch = useDispatch();
  const devMode = useSelector((state) => state.devMode?.devMode);

  if (process.env.NODE_ENV !== "development") return null; // Hide in production

  return (
    <div>
      <h3>Dev Mode: {devMode ? "Enabled" : "Disabled"}</h3>
      <button onClick={() => dispatch(enableDevMode())}>Enable Dev Mode</button>
      <button onClick={() => dispatch(disableDevMode())}>Disable Dev Mode</button>
    </div>
  );
};

export default DevTools;

```
### **Prevent Dev State in Production**

By wrapping the logic in `process.env.NODE_ENV === "development"`, you ensure that:

1. **Reducers are excluded in production.**
2. **The `DevTools` component is hidden in production.**
3. **Dev-specific data like `devState` cannot be toggled outside the development environment.**