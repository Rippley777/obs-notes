### 1. **Install Dependencies**

Run the following command to add `redux-persist` to your project:

bash

Copy code

`npm install redux-persist # or yarn add redux-persist`

---

### 2. **Configure the Redux Store**

Update your Redux store setup to include `redux-persist`. Here's an example:

#### `store.js`

javascript

Copy code

`import { configureStore } from '@reduxjs/toolkit'; import { persistStore, persistReducer } from 'redux-persist'; import storage from 'redux-persist/lib/storage'; // Default storage for web import rootReducer from './reducers'; // Combine your reducers here  // Persist Config const persistConfig = {   key: 'root', // Key for localStorage   storage,     // Storage type (e.g., localStorage) };  // Persist Reducer const persistedReducer = persistReducer(persistConfig, rootReducer);  // Configure Store const store = configureStore({   reducer: persistedReducer,   middleware: (getDefaultMiddleware) =>     getDefaultMiddleware({       serializableCheck: false, // Disable checks for non-serializable values (redux-persist)     }), });  // Persistor export const persistor = persistStore(store);  export default store;`

---

### 3. **Set Up the Provider in Your App**

Wrap your app in `PersistGate` to delay rendering until the persisted state has been rehydrated.

#### `index.js` or `main.jsx`

javascript

Copy code

`import React from 'react'; import ReactDOM from 'react-dom'; import { Provider } from 'react-redux'; import { PersistGate } from 'redux-persist/integration/react'; import store, { persistor } from './store'; import App from './App';  ReactDOM.render(   <Provider store={store}>     {/* PersistGate delays rendering until rehydration is complete */}     <PersistGate loading={<div>Loading...</div>} persistor={persistor}>       <App />     </PersistGate>   </Provider>,   document.getElementById('root') );`

---

### 4. **Verify Persistence**

- Start your app, modify the state, and refresh the page to verify that the state persists.
- By default, `redux-persist` stores the data in `localStorage` (web) or `AsyncStorage` (React Native).

---

### 5. **(Optional) Customize the Persistence**

- **Blacklist/Whitelist:** Use these in `persistConfig` to persist only certain slices of your state.
    
    javascript
    
    Copy code
    
    `const persistConfig = {   key: 'root',   storage,   blacklist: ['tempData'], // Don't persist this slice   // or   whitelist: ['user'], // Persist only this slice };`
    
- **Debugging:** Enable debugging by adding `debug: true` to `persistConfig`.

---

### 6. **Handling Store Resets**

To reset the persisted store when needed:

javascript

Copy code

`import { persistor } from './store';  // Clear persisted state persistor.purge();`