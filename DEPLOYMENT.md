# JAL Data Consulting - Deployment Guide

## GitHub Pages Deployment

### Step 1: Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon in the top right, then **New repository**
3. Name it `jaldata.github.io` (for user site) OR any name like `jaldata-website` (for project site)
4. Set visibility to **Public** (required for free GitHub Pages)
5. Click **Create repository**

### Step 2: Push Your Website to GitHub

Open your terminal and run:

```bash
cd /Users/josephlucibello/Documents/jaldata_website

# Initialize git repository
git init

# Add all files
git add .

# Commit
git commit -m "Initial website commit"

# Add your GitHub repository as remote (replace with your actual repo URL)
git remote add origin https://github.com/YOUR_USERNAME/jaldata.github.io.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (gear icon)
3. In the left sidebar, click **Pages**
4. Under "Source", select **Deploy from a branch**
5. Select **main** branch and **/ (root)** folder
6. Click **Save**

Your site will be live at: `https://YOUR_USERNAME.github.io/` (user site) or `https://YOUR_USERNAME.github.io/repo-name/` (project site)

---

## Custom Domain Setup (e.g., jaldata.com)

### Step 1: Purchase a Domain

Purchase your domain from a registrar like:
- [Namecheap](https://namecheap.com)
- [Google Domains](https://domains.google)
- [GoDaddy](https://godaddy.com)
- [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/)

### Step 2: Create CNAME File

Create a file named `CNAME` (no extension) in your repository root with your domain:

```
jaldata.com
```

This file is already included if you want to use jaldata.com. Update it with your actual domain.

### Step 3: Configure DNS Records

Log into your domain registrar's DNS management panel and add these records:

#### Option A: Apex Domain (jaldata.com)

Add **A records** pointing to GitHub's IP addresses:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 3600 |
| A | @ | 185.199.109.153 | 3600 |
| A | @ | 185.199.110.153 | 3600 |
| A | @ | 185.199.111.153 | 3600 |

#### Option B: Subdomain (www.jaldata.com)

Add a **CNAME record**:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME | www | YOUR_USERNAME.github.io | 3600 |

#### Recommended: Both Apex + WWW

For best results, configure both:

1. Add all 4 **A records** above (for apex domain)
2. Add a **CNAME record** for www:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME | www | YOUR_USERNAME.github.io | 3600 |

### Step 4: Configure Custom Domain in GitHub

1. Go to your repository **Settings** > **Pages**
2. Under "Custom domain", enter your domain (e.g., `jaldata.com`)
3. Click **Save**
4. Check **Enforce HTTPS** (may take a few minutes to become available)

### Step 5: Wait for DNS Propagation

DNS changes can take **15 minutes to 48 hours** to propagate globally. You can check propagation at:
- [whatsmydns.net](https://www.whatsmydns.net/)
- [dnschecker.org](https://dnschecker.org/)

---

## DNS Configuration Examples by Registrar

### Namecheap

1. Log into Namecheap > **Domain List** > **Manage**
2. Go to **Advanced DNS** tab
3. Add records under "Host Records":

```
Type: A Record      Host: @    Value: 185.199.108.153    TTL: Automatic
Type: A Record      Host: @    Value: 185.199.109.153    TTL: Automatic
Type: A Record      Host: @    Value: 185.199.110.153    TTL: Automatic
Type: A Record      Host: @    Value: 185.199.111.153    TTL: Automatic
Type: CNAME Record  Host: www  Value: YOUR_USERNAME.github.io.  TTL: Automatic
```

### Cloudflare

1. Log into Cloudflare > Select your domain
2. Go to **DNS** > **Records**
3. Click **Add record** for each:

```
Type: A      Name: @    IPv4: 185.199.108.153    Proxy: DNS only
Type: A      Name: @    IPv4: 185.199.109.153    Proxy: DNS only
Type: A      Name: @    IPv4: 185.199.110.153    Proxy: DNS only
Type: A      Name: @    IPv4: 185.199.111.153    Proxy: DNS only
Type: CNAME  Name: www  Target: YOUR_USERNAME.github.io    Proxy: DNS only
```

**Note:** Set proxy status to "DNS only" (gray cloud) for GitHub Pages to work properly with HTTPS.

### GoDaddy

1. Log into GoDaddy > **My Products** > **DNS**
2. Under "Records", click **Add**:

```
Type: A      Name: @    Value: 185.199.108.153    TTL: 1 Hour
Type: A      Name: @    Value: 185.199.109.153    TTL: 1 Hour
Type: A      Name: @    Value: 185.199.110.153    TTL: 1 Hour
Type: A      Name: @    Value: 185.199.111.153    TTL: 1 Hour
Type: CNAME  Name: www  Value: YOUR_USERNAME.github.io    TTL: 1 Hour
```

---

## Troubleshooting

### Site Not Loading

1. **Check DNS propagation** - Use whatsmydns.net to verify your records are live
2. **Verify CNAME file** - Must contain only your domain, no extra spaces or lines
3. **Check GitHub Pages settings** - Ensure custom domain is saved and matches CNAME file

### HTTPS Not Working

1. **Wait for certificate** - GitHub automatically provisions SSL, can take up to 24 hours
2. **Check DNS** - HTTPS won't work until DNS is properly configured
3. **Remove and re-add** - Try removing the custom domain, saving, then adding it back

### "Domain already taken" Error

Another GitHub repository may have this domain configured. Remove the CNAME file from any other repos.

### Changes Not Showing

1. **Hard refresh** - Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
2. **Clear cache** - Or open in incognito/private window
3. **Check build status** - Go to Actions tab in your repo to see if deployment succeeded

---

## Updating Your Website

After making changes to your files:

```bash
git add .
git commit -m "Description of changes"
git push
```

GitHub Pages will automatically rebuild and deploy your site within 1-2 minutes.

---

## Contact Form Setup

The website includes a contact form. To make it functional:

### Option 1: Formspree (Recommended - Free)

1. Go to [formspree.io](https://formspree.io)
2. Create a free account
3. Create a new form and get your form ID
4. Update the form action in `index.html`:

```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```

### Option 2: Netlify Forms

If you decide to use Netlify instead of GitHub Pages:

1. Add `netlify` attribute to your form:
```html
<form name="contact" netlify>
```

### Option 3: Email Link Only

Remove the form and keep just the email link for simplicity.

---

## File Structure

```
jaldata_website/
├── index.html      # Main website
├── styles.css      # Stylesheet
├── CNAME           # Custom domain (create this)
└── DEPLOYMENT.md   # This guide
```
