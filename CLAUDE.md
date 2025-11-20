# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based iOS app landing page template designed for GitHub Pages. It automatically fetches app metadata from the App Store and generates a responsive landing page with device mockups, features, and contact forms.

## Technology Stack

- **Static Site Generator**: Jekyll 3.10
- **Styling**: SCSS (Sass)
- **Deployment**: GitHub Pages
- **Dependencies**:
  - `github-pages` gem
  - Bootstrap 4.4.1 (for form controls)
  - Font Awesome 6.4.0 (via CDN)

## Development Commands

### Local Development
```bash
# Install dependencies
bundle install

# Build the site locally
bundle exec jekyll build

# Serve the site locally with auto-rebuild
bundle exec jekyll serve

# Serve with drafts and future posts
bundle exec jekyll serve --drafts --future
```

The local site will be available at `http://localhost:4000/` (or the port shown in the output).

### Production Build
GitHub Pages automatically builds and deploys when changes are pushed to the repository.

## Site Architecture

### Configuration-Driven Design
The site is entirely configured through `_config.yml` with minimal need to touch HTML/CSS:

- **App Metadata**: iOS App ID automatically populates app name, icon, price, and App Store link
- **Visual Customization**: Colors, transparency values, device mockup colors
- **Content**: Features list, social links, contact information
- **SEO**: Open Graph and Twitter Card metadata

### Directory Structure

- `_config.yml` - Central configuration file for all site content and styling
- `_layouts/` - Page templates
  - `default.html` - Main landing page layout with device preview
  - `page.html` - Simple page layout for markdown pages
- `_includes/` - Reusable components
  - `head.html` - Meta tags, Open Graph, Twitter Cards, Font Awesome
  - `header.html` - Top navigation bar with app icon
  - `features.html` - Feature list grid
  - `footer.html` - Social links and contact form
  - `screencontent.html` - Device mockup content area
  - `appstoreimages.html` - App store badge images
- `_pages/` - Content pages
  - `changelog.md` - App changelog
  - `privacypolicy.md` - Privacy policy
  - `contact.md` - Contact form page
- `_sass/` - Styling
  - `base.scss` - Base styles and variables
  - `layout.scss` - Main layout and component styles
  - `github-markdown.scss` - Markdown rendering styles
- `assets/` - Static files
  - Device mockup images (`black.png`, `blue.png`, `coral.png`, `white.png`, `yellow.png`)
  - `screenshot/` - App screenshots
  - `videos/` - App preview videos
  - `headerimage.png` - Hero cover image
  - `og_image.jpg` - Default Open Graph image

### Key Architecture Patterns

**Jekyll Collections**: The `_pages` collection allows markdown files to be rendered with custom permalinks and included in navigation via `include_in_header: true`.

**Automatic App Store Integration**: The `ios_app_id` in `_config.yml` triggers automatic fetching of app metadata from the App Store API.

**Device Mockup System**: SVG clip paths are used to display screenshots/videos within iPhone device frames. Device color is configurable via `device_color` setting.

**Media Display Logic**: The site automatically detects and displays either:
- Static screenshots from `assets/screenshot/`
- Videos from `assets/videos/` (supports .webm/.ogg for Chrome/Firefox, .mp4/.mov for Safari)

**SEO Optimization**: Head includes Open Graph and Twitter Card meta tags that pull from `_config.yml` or page-specific frontmatter overrides.

## Content Management

### Adding/Editing Features
Edit the `features` array in `_config.yml`. Each feature requires:
- `title` - Feature name
- `description` - Feature description
- `fontawesome_icon_name` - Icon name from fontawesome.com/icons

### Adding New Pages
Create markdown files in `_pages/` with frontmatter:
```yaml
---
layout: page
title: Page Title
include_in_header: true  # Show in navigation
permalink: /page-url/
---
```

### Customizing Colors/Styling
All color values are centralized in `_config.yml` under "Theme Settings". No need to edit SCSS files for basic color changes.

### Media Requirements
Screenshots and videos must use iPhone resolutions:
- 828x1792
- 1125x2436
- 1242x2688

## Contact Form Integration

The site uses Formspree for contact form handling. Set `formspree_form_id` in `_config.yml` to enable the contact form in the footer.

## Important Configuration Notes

- The `ios_app_id` drives automatic metadata population - this is the core identifier
- `ios_app_country` defaults to "us" but can be changed for international apps
- Smart app banner (`enable_smart_app_banner`) shows iOS banner on mobile devices
- Social links are conditionally displayed - only configured platforms appear in footer
