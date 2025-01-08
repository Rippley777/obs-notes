Depending on your configuration this will require different steps. 


## For [[Node]]: (I've never actually had to use this yet but seems like a good last resort to try) 
#### Step 1: Update `package.json`

Add an alias using `"_moduleAliases"` and install `module-alias`:

`yarn add module-alias`

Update `package.json`:

`{   "_moduleAliases": {     "@": "src"   } }`

#### Step 2: Enable in Entry File

Add this to your entry point (e.g., `index.ts`):
`import 'module-alias/register';`

## For [[Typescript]]:
#### inside `tsconfig.json`
##### Add a `paths` alias for TypeScript to recognize `src`
```
	{ "compilerOptions": { "baseUrl": ".", "paths": { "@/*": ["src/*"] } } }
```
### Optional:
##### Update `eslint` for Path Mapping (Optional)

If you're using ESLint, configure `eslint-import-resolver-typescript`:

	`yarn add eslint-import-resolver-typescript -D`

Update `.eslintrc.js`:

```
	module.exports = {
		settings: {
			'import/resolver': {     
				 typescript: {      
				    project: './tsconfig.json',    
				   },
	     }, 
		},
	};
```
		

### For [[Webpack]]:
#### inside `webpack.config.ts`
##### Add an alias for the `src` directory
```
	const path = require('path');
	module.exports = { 
		resolve: {
			alias: { '@': path.resolve(__dirname, 'src'), }, 
		}, 
	};
```

For [[ Vite ]]


