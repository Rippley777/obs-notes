
# Setup and Configuration Quick Start Guide
## **Overview**
To set up an Azure Static Web App and use the free tier, follow these steps:

### **Step 1: Create the Static Web App**
1. **Navigate in Azure Portal**:
   - Go to **Azure** → **Create a Resource**.
   - Search for **Static Web App** (this step has moved from previous versions).
   
2. **For Dev: Choose Free Tier Setup**:
   - To use the free tier, opt to set up the **GitHub CI/CD action after creation**.

3. **Configure Settings**:
   - Fill out the required fields (e.g., name, region, etc.).
   - Customize additional settings as desired.

4. **Complete the Creation**:
   - Once the resource is created, navigate to the **Deployment Center**.
   - Link your **GitHub repository**. This will generate a GitHub Actions workflow file (`.yml`) in your repository that automatically deploys your app on `push`.

---

### **Step 2: Customize the GitHub Action**
- Edit the generated `.yml` file to customize the deployment configuration, such as targeting a specific branch for deployment.

---

### **Step 3: Add a `staticwebapp.config.json` File**
In the root of your GitHub repository, create a `staticwebapp.config.json` file to define platform and routing configurations.

#### **Sample Configuration**
```json
{
  "platform": {
    "nodeVersion": "20.x"
  },
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/images/*", "/static/*", "/favicon.ico"]
  },
  "routes": [
    {
      "route": "/*",
      "serve": "/index.html",
      "statusCode": 200
    }
  ]
}
```

---

### **Explanation of `staticwebapp.config.json`**
1. **Platform Configuration**:
   - `"nodeVersion"` specifies the Node.js runtime version to use, this can be many different formats (i.e., `20`, `20.x`, `20.18.1`).

2. **Navigation Fallback**:
   - Defines fallback behavior for single-page applications (SPAs).
   - Rewrites all unmatched routes to `/index.html` while excluding paths like `/images/*` and `/static/*`.

3. **Routes**:
   - Specifies individual routes, serving `/index.html` for all paths (`/*`) with a `200` status code.

---

### **Final Steps**
- Push changes to the GitHub repository.
- Verify the deployment by checking the Azure Portal or your app's live URL.
- Monitor the GitHub Actions workflow to confirm successful builds and deployments.

---

### **Next Steps**
- Explore further customization in Azure Static Web Apps (e.g., adding APIs, integrating custom domains, etc.).
- For more details on `staticwebapp.config.json`, refer to the [Azure Static Web Apps Documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/).
