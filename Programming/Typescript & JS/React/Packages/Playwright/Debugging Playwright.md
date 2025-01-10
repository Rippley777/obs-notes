### 1. **Run with `--debug`**

Playwright provides a `--debug` flag that pauses the execution and opens the Inspector UI, allowing you to step through your tests interactively.

`npx playwright test --debug`

When you use this, Playwright runs your test in a non-headless browser, and the Inspector UI is launched.

---

### 2. **Use the Debug Mode Programmatically**

You can add the following line in your test to pause execution and debug interactively:

`await page.pause();`

For example:

```
const { test } = require('@playwright/test');

test('debug example', async ({ page }) => {
    await page.goto('http://example.com');
    await page.pause(); // Opens the Playwright Inspector
    await page.click('text=More information...');
});

```

When the test reaches `await page.pause()`, it stops and opens the Inspector, where you can execute commands, explore the DOM, and continue the test.

---

### 3. **Run in Non-Headless Mode**

By default, Playwright runs tests in headless mode. To see the browser window, run tests in non-headless mode:

`npx playwright test --headed`

This is particularly useful when debugging visually.

---

### 4. **Use the `PWDEBUG` Environment Variable**

Set the `PWDEBUG` environment variable to enable debugging features, such as pausing on errors or opening the Playwright Inspector:

`PWDEBUG=1 npx playwright test`

This works similarly to the `--debug` flag but is more flexible since it pauses automatically when an error occurs or when `await page.pause()` is encountered.

---

### 5. **Enable Debugging Logs**

To get detailed logs of what's happening during your test, set the `DEBUG` environment variable:

`DEBUG=pw:api npx playwright test`

This logs all Playwright API calls to the console, helping you trace the sequence of actions.

---

### 6. **Use the Playwright Inspector**

The Playwright Inspector can be opened programmatically by calling `await page.pause()` or by enabling `PWDEBUG=1`. Once opened, you can:

- Step through tests.
- Explore the DOM and modify it live.
- See detailed API calls and test progression.

---

### Example Workflow for Debugging

1. **Write Your Test**:
```
const { test } = require('@playwright/test');

test('debugging test', async ({ page }) => {
    await page.goto('http://example.com');
    await page.pause(); // Pause here to inspect
    await page.click('text=More information...');
});

```
    
2. **Run in Debug Mode**:
 
    `npx playwright test --debug`
    
3. **Interact with the Inspector**:
    
    - Inspect elements.
    - Step through code.
    - Continue execution as needed.

---

### 7. **Pause Only on Errors**

Set the `PWDEBUG=console` environment variable to pause only when an error occurs:

`PWDEBUG=console npx playwright test`

This is useful for debugging failing tests without manually adding breakpoints.

---

### 8. **Use Breakpoints in VS Code**

If you're using Visual Studio Code, you can debug Playwright tests by:

1. Adding a `launch.json` file in your `.vscode` directory:

    ```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Playwright Debug",
            "type": "node",
            "request": "launch",
            "program": "${workspaceFolder}/node_modules/@playwright/test/lib/cli.js",
            "args": ["test", "--project=chromium"],
            "cwd": "${workspaceFolder}",
            "env": {
                "PWDEBUG": "1"
            }
        }
    ]
	}

```
    
2. Start debugging by pressing `F5` or selecting "Playwright Debug" from the Debug panel.