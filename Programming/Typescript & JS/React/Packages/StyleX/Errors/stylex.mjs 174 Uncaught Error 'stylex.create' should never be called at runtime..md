`stylex.mjs:174 Uncaught Error: 'stylex.create' should never be called at runtime. It should be compiled away by '@stylexjs/babel-pluginThe error message you're seeing indicates that `stylex.create` is being called at runtime, which should not happen if `@stylexjs/babel-plugin` is correctly configured. This plugin is supposed to compile away `stylex.create` calls during the build process. Here’s how you can troubleshoot and fix this issue:

### Steps to Resolve the Issue

**Check Babel Configuration**: Ensure that `@stylexjs/babel-plugin` is included in your Babel configuration file (e.g., `.babelrc`, `babel.config.js`).

Example configuration:


```json
{
  "plugins": ["@stylexjs/babel-plugin"]
}

```

**Verify Plugin Installation**: Make sure `@stylexjs/babel-plugin` is installed in your project.



```bash
yarn add @stylexjs/babel-plugin --dev

```

- **Ensure Proper File Extensions**: Ensure that your Babel configuration is applied to the files using `stylex.create`. Sometimes, specific file extensions might be excluded.
    
- **Check Babel Loader in Webpack (if used)**: If you’re using Webpack, ensure that the Babel loader is correctly configured to process your JavaScript/TypeScript files.
    
    Example `webpack.config.js`:

```javascript
module: {
  rules: [
    {
      test: /\.jsx?$/,
      exclude: /node_modules/,
      use: {
        loader: 'babel-loader',
        options: {
          plugins: ['@stylexjs/babel-plugin']
        }
      }
    }
  ]
}

```
- **Inspect Compilation Output**: Check the compiled output to ensure that `stylex.create` calls are replaced as expected.
    
- **Check Babel Version Compatibility**: Ensure that the version of `@stylexjs/babel-plugin` is compatible with your Babel setup.
    
- **Clear Build Cache**: Sometimes, clearing the build cache can resolve issues with stale configurations.



```bash
rm -rf node_modules/.cache

```

**Debugging**:

- **Log Compilation Process**: Enable verbose logging in your build tool to see if the plugin is being applied.
- **Manual Babel Compilation**: Try running Babel manually on a file to see if `stylex.create` is being transformed correctly.
### Example of Complete `.babelrc` Configuration


```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"],
  "plugins": ["@stylexjs/babel-plugin"]
}

```

### Troubleshooting Checklist

- [ ]  **Babel configuration includes `@stylexjs/babel-plugin`.**
- [ ]  **`@stylexjs/babel-plugin` is installed and up-to-date.**
- [ ]  **Webpack (if used) is properly configured to use Babel.**
- [ ]  **No caching issues (clear cache if necessary).**
- [ ]  **Check output to ensure `stylex.create` is compiled away.**

If you follow these steps and still encounter issues, it might be helpful to share more details about your setup, such as your Babel and Webpack configuration files, to diagnose further.