# My Portfolio Website

A personal portfolio and blog website built with Hugo and hosted on GitHub Pages.

## 🌟 Features

- **Projects Section**: Showcase your major projects with detailed descriptions
- **Resume Page**: Display and provide downloadable PDF resume
- **Blog**: Write and publish blog posts
- **Responsive Design**: Clean, modern theme (PaperMod) that works on all devices
- **Automatic Deployment**: GitHub Actions workflow for seamless deployment

## 🚀 Quick Start

### Prerequisites

- Conda environment with Hugo installed (already set up as `website`)

### Running Locally

1. Activate the conda environment:
   ```bash
   conda activate website
   ```

2. Navigate to the website directory:
   ```bash
   cd /Users/ambujegupta/Desktop/personal_work/website
   ```

3. Start the Hugo development server:
   ```bash
   hugo server -D
   ```

4. Open your browser and visit: `http://localhost:1313`

## 📝 Adding Content

### Adding a New Project

1. Create a new file in `content/projects/`:
   ```bash
   hugo new content/projects/my-new-project.md
   ```

2. Edit the file and add your project details:
   ```markdown
   ---
   title: "Project Name"
   date: 2024-01-15
   draft: false
   description: "Brief description"
   tags: ["python", "web"]
   ---
   
   ## Overview
   Your project description...
   ```

3. Set `draft: false` when ready to publish

### Adding a New Blog Post

1. Create a new blog post:
   ```bash
   hugo new content/blog/my-blog-post.md
   ```

2. Edit the file with your content:
   ```markdown
   ---
   title: "My Blog Post Title"
   date: 2024-01-20
   draft: false
   description: "Post description"
   tags: ["technology", "tutorial"]
   ---
   
   Your blog content here...
   ```

### Updating Your Resume

1. Save your resume as `resume.pdf`
2. Place it in the `static/` folder
3. The download link on the Resume page will automatically work

### Customizing the Site

Edit `hugo.toml` to update:
- Site title and description
- Your name and bio
- Social media links (GitHub, LinkedIn, etc.)
- Menu items
- Theme settings

## 🌐 Deploying to GitHub Pages

### Initial Setup

1. Create a new repository on GitHub (e.g., `yourusername.github.io`)

2. Update the `baseURL` in `hugo.toml`:
   ```toml
   baseURL = 'https://yourusername.github.io/'
   ```

3. Initialize git and push to GitHub:
   ```bash
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/yourusername/yourusername.github.io.git
   git push -u origin main
   ```

4. Enable GitHub Pages:
   - Go to your repository on GitHub
   - Navigate to Settings → Pages
   - Under "Source", select "GitHub Actions"

5. The site will automatically deploy when you push to the main branch!

### Updating the Site

After making changes:
```bash
git add .
git commit -m "Description of changes"
git push
```

The GitHub Actions workflow will automatically build and deploy your site.

## 📁 Project Structure

```
website/
├── .github/
│   └── workflows/
│       └── hugo.yml          # GitHub Actions deployment workflow
├── content/
│   ├── _index.md            # Home page
│   ├── resume.md            # Resume page
│   ├── blog/
│   │   ├── _index.md        # Blog section page
│   │   └── *.md             # Individual blog posts
│   └── projects/
│       ├── _index.md        # Projects section page
│       └── *.md             # Individual project pages
├── static/
│   └── resume.pdf           # Your resume PDF (add this)
├── themes/
│   └── PaperMod/            # Hugo theme (git submodule)
└── hugo.toml                # Site configuration
```

## 🎨 Customization Tips

### Theme Colors and Appearance

The PaperMod theme supports light/dark mode automatically. You can customize it further by adding custom CSS in `assets/css/extended/` (create this folder if needed).

### Adding Images

1. Place images in the `static/images/` folder
2. Reference them in your markdown:
   ```markdown
   ![Description](/images/your-image.jpg)
   ```

### Social Icons

Update the `[[params.socialIcons]]` section in `hugo.toml` to add/modify social links.

## 🛠️ Useful Hugo Commands

```bash
# Create new content
hugo new content/blog/post-name.md
hugo new content/projects/project-name.md

# Start development server
hugo server -D

# Build the site (generates public/ folder)
hugo

# Check Hugo version
hugo version
```

## 📚 Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Theme Documentation](https://github.com/adityatelange/hugo-PaperMod/wiki)
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)

## 📧 Support

If you encounter any issues, check:
1. Hugo server is running (visit http://localhost:1313)
2. Files are saved with correct frontmatter
3. `draft: false` is set for published content
4. GitHub Actions workflow completed successfully

## 📄 License

This project is open source and available for personal use.

---

**Next Steps:**
1. Customize `hugo.toml` with your personal information
2. Update `content/_index.md` with your bio
3. Add your projects to `content/projects/`
4. Add your resume PDF to `static/`
5. Start writing blog posts in `content/blog/`
6. Deploy to GitHub Pages!
