Setting up an Azure Web App instance and adding a GitHub deployment link afterward while staying within the free or main tier involves these steps:

---

### **1. Create an Azure Web App Instance**

1. **Log in to the Azure Portal**.
    
2. Navigate to **"Create a Resource"** → **"Web App"**.
    
3. Fill in the details:
    
    - **Subscription**: Choose your active subscription.
    - **Resource Group**: Create a new one or use an existing group.
    - **Name**: Provide a globally unique name for your web app.
    - **Publish**: Select **Code** if you're deploying from GitHub.
    - **Runtime Stack**: Choose the language and version of your application.
    - **Region**: Select the closest region with free-tier availability.
    - **Pricing Plan**: Choose the **F1 (Free)** tier or a plan within the "Main" tier.
4. Click **Review + Create** to validate and then click **Create**.
    

---

### **2. Configure GitHub Deployment Link**

After setting up the Web App, you can configure a GitHub Actions workflow for continuous deployment.

#### **Option A: Using Azure Portal**

1. **Navigate to Your Web App**:
    
    - Go to the **"App Service"** section in the Azure Portal and select your newly created Web App.
2. **Set Up Deployment Center**:
    
    - On the left sidebar, find **"Deployment Center"** and click it.
    - Choose **GitHub** as the source.
    - Authenticate with your GitHub account and select the repository and branch you want to deploy from.
3. **Build Provider**:
    
    - Choose **GitHub Actions**.
    - Confirm the runtime and framework settings to ensure compatibility.
    - Azure will automatically set up a GitHub Actions workflow in your repository for the deployment.
4. **Review and Save**:
    
    - Once you've configured the details, review and apply the changes. Azure will begin deploying your application.

---

#### **Option B: Manually Add GitHub Actions**

1. **Get Deployment Credentials**:
    
    - In the Azure Portal, go to your Web App and navigate to **Deployment Center**.
    - Under **Settings**, retrieve the **Deployment Credentials** (username, password, and publishing URL).
2. **Set Up GitHub Actions in Your Repo**:
    
    - In your GitHub repository, create a `.github/workflows/azure-webapp.yml` file.
    - Add the following sample workflow, customizing it for your app's details:
```
name: Deploy to Azure Web App

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Set up Node.js (or your runtime)
      uses: actions/setup-node@v3
      with:
        node-version: '16' # Change as per your runtime

    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: <YOUR-WEB-APP-NAME>
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}

```


3. **Add Azure Publish Profile to GitHub**:
    
    - Download your app's **Publish Profile** from the Azure Portal (under Deployment Center → Publish Profile).
    - Add it to GitHub as a secret named `AZURE_WEBAPP_PUBLISH_PROFILE`.
4. **Push Changes to Main Branch**:
    
    - Any new changes pushed to the `main` branch will now trigger the GitHub Actions workflow.

---

### **3. Test and Monitor**

- Once deployed, access your app via the provided Azure URL.
- Monitor deployments and logs in the **Deployment Center** and **Log Stream** sections of the Azure Portal.