
### **Install Playwright**

First, you'll need to install Playwright and its test runner. You can do this via npm or yarn. It's recommended to use the Playwright Test runner for full integration:

`npm install --save-dev @playwright/test`

This command installs the Playwright package, which includes the test runner and browser binaries for Chromium, Firefox, and WebKit.

### 2. **Set Up Your Test Environment**

After installing, you can set up your test environment. Playwright offers a command that prepares everything you need to start writing tests:

`npx playwright install`

This command installs the necessary browser binaries.

### 3. **Create a Basic Test**

Create a test file, for instance `tests/example.spec.js`, and write a simple test. Here’s an example test that navigates to a website and checks if a certain text is present:

`// tests/example.spec.js const { test, expect } = require('@playwright/test');  test('example test - check for text on the page', async ({ page }) => {     await page.goto('https://example.com');     const pageTitle = await page.title();     expect(pageTitle).toBe('Example Domain');      const content = await page.textContent('h1');     expect(content).toBe('Example Domain'); });`

### 4. **Configure Playwright**

Optionally, you can create a configuration file for Playwright to customize settings such as test directories, browser options, and more. To generate a default configuration file, run:

`npx playwright test --init`

This command will create a `playwright.config.js` file where you can specify various options. Here's an example configuration:

```
// playwright.config.js
const { devices } = require('@playwright/test');

module.exports = {
  use: {
    // Define the base URL for all tests
    baseURL: 'https://example.com',
  },
  projects: [
    {
      name: 'Chromium',
      use: { ...devices['Desktop Chrome'] },
    },
    {
      name: 'Firefox',
      use: { ...devices['Desktop Firefox'] },
    },
    {
      name: 'WebKit',
      use: { ...devices['Desktop Safari'] },
    },
  ],
  // Other configurations like testDir, snapshotDir etc.
};

```
```
// Example test using baseURL
const { test, expect } = require('@playwright/test');

test('example test with baseURL', async ({ page }) => {
    // No need to specify the full URL, just the path
    await page.goto('/login');
    // Continue with your test steps...
});

```
### 5. **Run Your Tests**

Finally, run your tests using the Playwright command:

`npx playwright test`

This command will execute the tests according to the configurations provided. Playwright will run tests in all configured browsers unless specified otherwise.

### 6. **View Test Results**

Playwright provides a command to serve a web server where you can view detailed test results:

`npx playwright show-report`

This will start a local server showing the test results in a more detailed and visual format.



## Screenshot Testing

### **Set Up Screenshot Capturing**

First, modify your tests to take screenshots. This can be done using the `page.screenshot()` function provided by Playwright. Here's an example of how to capture a screenshot within a test:


```
// tests/screenshot.spec.js
const { test, expect } = require('@playwright/test');

test('home page should look the same', async ({ page }) => {
    await page.goto('https://example.com');
    const screenshot = await page.screenshot();
    expect(screenshot).toMatchSnapshot('homepage.png');
});

```

### 2. **Configure Snapshots Directory**

Configure where Playwright should store and look for snapshots by adding configurations in your `playwright.config.js`. You can specify the snapshot directory like this:

```
// playwright.config.js
module.exports = {
  testDir: './tests',
  snapshotDir: './tests/__snapshots__',
  use: {
    // other configurations
  }
};

```

### 3. **Baseline Snapshots**

When you run your tests for the first time, Playwright saves the screenshots as baseline images in the specified snapshot directory. These images are what future tests will compare against.

### 4. **Run and Review Tests**

Run your tests with:

`npx playwright test`

If the screenshots do not match the baseline images (for instance, if there are visual changes or regressions), the tests will fail, and Playwright will provide an output indicating the differences.

### 5. **Handling Visual Differences**

When a test fails due to a visual difference, you can:

- Review the generated diff images to see if the change is expected or is a genuine regression.
- Update the baseline images if the change is intentional and should be the new "source of truth".

To update the baseline images, simply delete the old snapshots and re-run the tests. The new snapshots will replace the old ones.

### 6. **Advanced Configuration**

For more complex scenarios, such as dynamic content, animations, or date and time variations, you might need to configure Playwright to ignore certain differences. This can be done by setting options in the `page.screenshot()` method:

```
const screenshot = await page.screenshot({
    fullPage: true, // Capture the full page
    omitBackground: true, // Make the background transparent
    threshold: 0.2 // Tolerance for color differences
});

```

### 7. **Integration with CI/CD**

Integrate screenshot tests into your Continuous Integration/Continuous Deployment (CI/CD) pipeline to automatically catch visual regressions. Ensure your baseline images are stored and managed correctly in your version control system to maintain consistency across different environments.