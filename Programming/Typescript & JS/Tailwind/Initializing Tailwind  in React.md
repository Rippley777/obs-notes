---

### 1. **Install Required Dependencies**

Make sure you have TailwindCSS, PostCSS, and Autoprefixer installed in your project:

bash

Copy code

`yarn add -D tailwindcss postcss autoprefixer`

---

### 2. **Initialize TailwindCSS**

If you haven’t already, create a Tailwind configuration file:

bash

Copy code

`npx tailwindcss init`

---

### 3. **Configure TailwindCSS**

Edit `tailwind.config.js` to include Storybook’s paths for content scanning:

javascript

Copy code

`/** @type {import('tailwindcss').Config} */ module.exports = {   content: [     './src/**/*.{js,jsx,ts,tsx}', // Your app files     './.storybook/**/*.{js,jsx,ts,tsx}', // Storybook files     './stories/**/*.{js,jsx,ts,tsx}',    // Storybook stories   ],   theme: {     extend: {},   },   plugins: [], };`

---

### 4. **Add Tailwind to Storybook**

#### Option 1: For Webpack-based Storybook

1. Install the `@storybook/addon-postcss` addon:
    
    bash
    
    Copy code
    
    `yarn add -D @storybook/addon-postcss`
    
2. Update `.storybook/main.js` to include the PostCSS plugin:
    
    javascript
    
    Copy code
    
    `module.exports = {   stories: ["../src/**/*.stories.@(js|jsx|ts|tsx)"],   addons: [     "@storybook/addon-links",     "@storybook/addon-essentials",     "@storybook/addon-postcss",   ],   framework: "@storybook/react", };`
    
3. Create a `postcss.config.js` file if it doesn’t exist:
    
    javascript
    
    Copy code
    
    `module.exports = {   plugins: {     tailwindcss: {},     autoprefixer: {},   }, };`
    
4. Import Tailwind’s base styles in your Storybook's `preview.js` file:
    
    javascript
    
    Copy code
    
    `import '../src/index.css'; // Adjust the path to your Tailwind CSS entry file`
    

---

#### Option 2: For Vite-based Storybook

If you’re using Storybook with Vite, follow these steps:

1. Add the necessary dependencies:
    
    bash
    
    Copy code
    
    `yarn add -D @storybook/addon-postcss vite-plugin-tailwindcss`
    
2. Update `.storybook/main.js` to enable Vite with PostCSS and Tailwind:
    
    javascript
    
    Copy code
    
    `module.exports = {   stories: ["../src/**/*.stories.@(js|jsx|ts|tsx)"],   addons: [     "@storybook/addon-links",     "@storybook/addon-essentials",     "@storybook/addon-postcss",   ],   framework: "@storybook/react-vite",   async viteFinal(config) {     config.css = config.css || {};     config.css.postcss = {       plugins: [         require('tailwindcss'),         require('autoprefixer'),       ],     };     return config;   }, };`
    
3. Import Tailwind styles in your `preview.js` file:
    
    javascript
    
    Copy code
    
    `import '../src/index.css'; // Adjust the path to your Tailwind CSS entry file`
    

---

### 5. **Verify the Integration**

Start Storybook to ensure Tailwind styles are applied:

bash

Copy code

`yarn storybook`

---

### 6. **Testing Tailwind Classes in Stories**

Here’s an example story that uses Tailwind classes:

tsx

Copy code

``import React from "react"; import { Meta, StoryFn } from "@storybook/react";  const Button = ({ label, className }: { label: string; className: string }) => (   <button className={`p-2 rounded ${className}`}>{label}</button> );  export default {   title: "Components/Button",   component: Button,   argTypes: {     className: { control: 'text' },   }, } as Meta;  const Template: StoryFn = (args) => <Button {...args} />;  export const Primary = Template.bind({}); Primary.args = {   label: "Primary Button",   className: "bg-blue-500 text-white hover:bg-blue-600", };``

---

### Debugging Tips

- **Missing Styles**: If Tailwind classes aren’t working, ensure `tailwind.config.js` includes all relevant Storybook paths under `content`.
- **PostCSS Issues**: Verify that `postcss.config.js` exists and is properly configured.
- **Build Issues**: Clear caches by removing `node_modules` and `.storybook` cache:
    
    bash
    
    Copy code
    
    `rm -rf node_modules rm -rf .storybook/.cache yarn install`