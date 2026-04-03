## Deployment (internal Google Workspace add-on)

### 1. Set up a GCP project

1. Create a project at [console.cloud.google.com](https://console.cloud.google.com)
2. Note the **project number** (shown on the project dashboard)
3. Enable these APIs: **Gmail API**, **Google Workspace Add-ons API**, **Google Workspace Marketplace SDK**
4. Go to **APIs & Services → OAuth consent screen**
   - User Type: **Internal**
   - Fill in app name and email fields
   - Skip the Scopes step (Apps Script handles these automatically)

### 2. Link GCP project to Apps Script

1. Open the script at [script.google.com](https://script.google.com)
2. **Project Settings → Google Cloud Platform (GCP) Project → Change project**
3. Enter your GCP **project number**

### 3. Set Script Properties

In the Apps Script editor: **Project Settings → Script Properties**, add:

| Property | Value |
|---|---|
| `WOOCOMMERCE_HOST` | Domain only, e.g. `vitalseeds.co.uk` |
| `WOOCOMMERCE_CONSUMER_KEY` | Starts with `ck_` |
| `WOOCOMMERCE_CONSUMER_SECRET` | Starts with `cs_` |

Generate key and secretat `WooCommerce → Settings → Advanced → REST API` in WordPress admin.

### 4. Push and deploy

**Using clasp (recommended):**
```bash
cd project
clasp push
```

**Without clasp:** In the [Apps Script](https://script.google.com/home) editor, create a file for each `.js` file
in `project/` and paste in the contents. Also paste the contents of
`appsscript.json` into the manifest (enable in app script editor via **View → Show manifest file**).

Then: **Deploy → New deployment → Google Workspace Add-on**. Note the **Deployment ID**.

### 5. Publish to internal Marketplace

1. In GCP: **APIs & Services → Google Workspace Marketplace SDK → App Configuration**
2. Set visibility to **Private**
3. Enter the **Deployment ID** from step 4
4. Add the OAuth scopes from `appsscript.json`
5. Save, then complete the **Store Listing** tab and publish

The app will then appear in the internal Marketplace and can be installed via the Google Admin console or directly by users from Gmail's add-on store.

### Updating

1. Make changes and `clasp push`
2. **Deploy → Manage deployments → edit → New version → Deploy**

Users receive updates automatically — no reinstall needed.
