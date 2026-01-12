# How to Build Your Own Consulting Website (Free)

This is a simple, professional website template you can customize and deploy for free using GitHub Pages. No coding experience required - just follow these steps.

## What You'll Get

- A professional single-page website
- Free hosting (via GitHub Pages)
- Custom domain support (optional, domain costs ~$10-15/year)
- Mobile-friendly responsive design
- No ongoing maintenance or costs

## Prerequisites

1. A GitHub account (free) - [Sign up here](https://github.com/signup)
2. A text editor - [VS Code](https://code.visualstudio.com/) is free and great
3. Git installed - [Download here](https://git-scm.com/downloads)

## Step 1: Get the Code

### Option A: Download directly
1. Click the green "Code" button on this repo
2. Click "Download ZIP"
3. Unzip the folder somewhere on your computer

### Option B: Clone with Git
```bash
git clone https://github.com/REPO_URL_HERE.git
cd jaldata-website
```

## Step 2: Customize the Content

Open the project folder in VS Code (or any text editor).

### Edit `index.html`

This is your entire website. Search and replace these items:

| Find | Replace With |
|------|--------------|
| `JAL Data` | Your company name |
| `JALData` | Your company name (no space) |
| `consulting@jaldata.com` | Your email address |

Then customize these sections:
- **Hero section** (~line 34) - Your main headline and tagline
- **Credentials** (~line 56) - Your stats (years experience, etc.)
- **Services** (~line 83) - What you offer
- **Technical Expertise** (~line 191) - Your skills/tools
- **Industries** (~line 248) - Industries you've worked in
- **Results** (~line 306) - Your quantified achievements

### Edit `styles.css` (Optional)

To change colors, edit the variables at the top of `styles.css`:

```css
:root {
    --primary: #2563eb;        /* Main blue - buttons, links */
    --secondary: #0f172a;      /* Dark navy - dark sections */
    --accent: #06b6d4;         /* Cyan - secondary accent */
}
```

### Edit `CNAME`

Replace `jaldata.com` with your domain, or delete this file if you're not using a custom domain.

## Step 3: Preview Locally

Just double-click `index.html` to open it in your browser. Refresh after making changes.

## Step 4: Create a GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it something like `my-consulting-site` (or `yourusername.github.io` for a cleaner URL)
3. Keep it **Public** (required for free GitHub Pages)
4. Don't initialize with README (you already have one)
5. Click **Create repository**

## Step 5: Push Your Code to GitHub

Open Terminal (Mac) or Command Prompt (Windows), navigate to your project folder, and run:

```bash
# Initialize git in your project folder
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit"

# Connect to your GitHub repo (replace with YOUR repo URL)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push
git branch -M main
git push -u origin main
```

## Step 6: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (gear icon in the top menu)
3. Click **Pages** in the left sidebar
4. Under "Source", select **Deploy from a branch**
5. Select **main** branch and **/ (root)** folder
6. Click **Save**

Wait 1-2 minutes, then your site will be live at:
```
https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/
```

## Step 7: Custom Domain (Optional)

Want `yourname.com` instead of `github.io`?

### Buy a Domain

Get one from any registrar (~$10-15/year):
- [Namecheap](https://namecheap.com)
- [Cloudflare](https://www.cloudflare.com/products/registrar/)
- [Google Domains](https://domains.google)
- [GoDaddy](https://godaddy.com)

### Configure DNS

Log into your domain registrar and add these DNS records:

**A Records** (point your domain to GitHub):
| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**CNAME Record** (for www):
| Type | Host | Value |
|------|------|-------|
| CNAME | www | YOUR_USERNAME.github.io |

### Update GitHub Settings

1. Edit the `CNAME` file in your repo to contain just your domain (e.g., `mysite.com`)
2. Push the change: `git add . && git commit -m "Update domain" && git push`
3. In GitHub repo **Settings > Pages**, enter your custom domain
4. Check **Enforce HTTPS** (may take a few minutes to appear)

DNS changes can take 15 minutes to 48 hours to propagate globally.

## Updating Your Site

After making changes to any files:

```bash
git add .
git commit -m "Description of what you changed"
git push
```

GitHub Pages automatically rebuilds your site within 1-2 minutes.

## File Structure

```
your-website/
├── index.html      # Your entire website (edit this!)
├── styles.css      # All the styling (colors, layout)
├── CNAME           # Your custom domain (optional)
├── DEPLOYMENT.md   # More detailed deployment notes
└── README.md       # This guide
```

## Troubleshooting

**Site not loading?**
- Make sure GitHub Pages is enabled (Settings > Pages)
- Check that you pushed to the `main` branch
- Wait a few minutes for GitHub to build

**Custom domain not working?**
- DNS takes time to propagate (up to 48 hours)
- Check your DNS records are correct at [whatsmydns.net](https://whatsmydns.net)
- Make sure your CNAME file has the correct domain

**Changes not showing?**
- Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
- Or open in an incognito window

## Questions?

The whole thing is just HTML and CSS - Google anything you want to change and you'll find answers. That's the beauty of keeping it simple.
