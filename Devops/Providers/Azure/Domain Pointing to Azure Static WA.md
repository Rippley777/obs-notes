

This guide explains how to configure a custom domain for your Azure [[Static Web App]] and update your DNS provider's settings to point the domain correctly.

---

## Steps to Point Your Domain to an Azure Static Web App

### 1. Add the Custom Domain in Azure
1. **Go to Your Static Web App**:
   - Open the [Azure Portal](https://portal.azure.com/).
   - Navigate to your Static Web App resource.

2. **Access the Custom Domains Section**:
   - In the left-hand menu, select **Custom domains**.

3. **Add a New Custom Domain**:
   - Click **Add** to start configuring your domain.
   - Enter your custom domain (e.g., `www.example.com`).

4. **Verify Ownership**:
   - Azure will display the DNS record required to verify ownership of the domain (usually a TXT or CNAME record).

---

### 2. Update Your DNS Records
1. **Log In to Your DNS Provider**:
   - Sign in to the service where your domain is registered (e.g., Namecheap, GoDaddy, Cloudflare).

2. **Add the Required DNS Record**:
   - **TXT Record**: Add the TXT record Azure provides to verify domain ownership.
     - **Name**: (e.g., `@` or `www`)
     - **Value**: The value Azure provides for verification.
   - **CNAME Record** (for subdomains):
     - **Name**: `www` (or the subdomain you're pointing).
     - **Value**: The Azure-provided CNAME (e.g., `mywebapp.azurestaticapps.net`).
   - **A Record** (for root domains):
     - If Azure provides an IP address, create an A record pointing your root domain to this IP address.
     - Add an **ALIAS** or **ANAME** record if your DNS provider supports it, pointing the root domain to the Azure-provided domain.

---

### 3. Complete Verification in Azure
1. **Verify the DNS Update**:
   - DNS changes may take some time to propagate (up to 48 hours, but usually much faster).

2. **Finish Adding the Domain**:
   - Return to the Azure Portal and click **Verify** or wait for Azure to detect the correct DNS settings automatically.

---

### 4. Enable HTTPS (Optional but Recommended)
1. **Automatic HTTPS**:
   - Once the domain is added, Azure automatically provisions an SSL certificate. Ensure the **Enable HTTPS** toggle is turned on in the custom domains settings.

2. **Custom SSL** (Optional):
   - If you have your own SSL certificate, you can upload it manually.

---

## DNS Examples

### For Subdomain (`www.example.com`)
- **CNAME Record**:
