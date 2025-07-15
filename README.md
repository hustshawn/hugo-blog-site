# My Hugo Blog

A simple blog built with Hugo and the PaperMod theme, ready for GitHub Pages deployment.

## Quick Start

### Local Development

1. Install Hugo (if not already installed):

   ```bash
   brew install hugo  # macOS
   ```

2. Clone this repository:

   ```bash
   git clone <your-repo-url>
   cd blog-site
   git submodule update --init --recursive
   ```

3. Start the development server:

   ```bash
   hugo server -D
   ```

4. Open your browser to `http://localhost:1313`

### Creating New Posts

Create a new blog post:

```bash
hugo new posts/my-new-post.md
```

Edit the markdown file in `content/posts/` and set `draft = false` when ready to publish.

### Deployment to GitHub Pages

This blog is configured to automatically deploy to GitHub Pages using GitHub Actions.

#### Setup Instructions

1. **Create a GitHub repository** for your blog
2. **Push this code** to your repository
3. **Enable GitHub Pages**:
   - Go to your repository settings
   - Navigate to "Pages" section
   - Under "Source", select "GitHub Actions"
4. **Update configuration**:
   - Edit `hugo.toml` and update the `baseURL` to match your GitHub Pages URL
   - Update social links and personal information

#### Manual Deployment

If you prefer manual deployment:

```bash
hugo --gc --minify
# Then upload the contents of the 'public' folder to your web server
```

## Customization

### Site Configuration

Edit `hugo.toml` to customize:

- Site title and description
- Author information
- Social media links
- Menu items
- Theme parameters

### Adding Content

- **Blog posts**: Add markdown files to `content/posts/`
- **Pages**: Add markdown files to `content/`
- **Static files**: Add to `static/` folder

### Theme Customization

This blog uses the [PaperMod theme](https://github.com/adityatelange/hugo-PaperMod).
Check their documentation for advanced customization options.

## File Structure

```
blog-site/
├── .github/workflows/    # GitHub Actions for deployment
├── archetypes/          # Content templates
├── content/             # Your blog content
│   ├── posts/          # Blog posts
│   └── about.md        # About page
├── static/             # Static files (images, etc.)
├── themes/PaperMod/    # Theme files (git submodule)
├── hugo.toml           # Site configuration
└── README.md           # This file
```

## Writing Posts

Blog posts should be written in Markdown format with front matter:

```markdown
+++
title = 'My Post Title'
date = '2025-01-14T10:00:00+00:00'
draft = false
tags = ['tag1', 'tag2']
categories = ['category1']
+++

# Your content here

Write your blog post content in Markdown format.
```

## Support

- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Theme Documentation](https://github.com/adityatelange/hugo-PaperMod)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)