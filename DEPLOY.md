# Deploy to GitHub Pages

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Create a new repository named: `ambuje.github.io`
3. Make it **Public**
4. Don't initialize with README (we already have files)

## Step 2: Push Your Code

Run these commands in your terminal:

```bash
cd /Users/ambujegupta/Desktop/personal_work/website

# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit your changes
git commit -m "Initial commit - Portfolio website"

# Add your GitHub repository as remote
git remote add origin https://github.com/ambuje/ambuje.github.io.git

# Rename branch to main
git branch -M main

# Push to GitHub
git push -u origin main
```

## Step 3: Enable GitHub Pages

1. Go to your repository: https://github.com/ambuje/ambuje.github.io
2. Click **Settings** (top right)
3. Click **Pages** (left sidebar)
4. Under **Source**, select **GitHub Actions**
5. The workflow will automatically deploy your site!

## Step 4: Wait for Deployment

1. Go to **Actions** tab in your repository
2. You'll see the workflow running
3. Wait 2-3 minutes for it to complete
4. Your site will be live at: **https://ambuje.github.io/**

## Updating Your Site

After making changes:

```bash
cd /Users/ambujegupta/Desktop/personal_work/website

git add .
git commit -m "Update content"
git push
```

The site will automatically rebuild and deploy!

## Troubleshooting

**If you get authentication errors:**
- You may need to use a Personal Access Token instead of password
- Go to GitHub → Settings → Developer settings → Personal access tokens
- Create a token with `repo` permissions
- Use the token as your password when pushing

**Alternative: Use GitHub Desktop**
- Download GitHub Desktop: https://desktop.github.com/
- Open the app and sign in
- Add your local repository
- Publish to GitHub

---

Your website will be live at: **https://ambuje.github.io/** 🚀
