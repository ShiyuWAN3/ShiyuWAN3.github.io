# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic personal website for Shiyu Wan (Ph.D. Student in Biostatistics at University of Washington) built with Jekyll and hosted on GitHub Pages. Based on the Academic Pages template, a fork of Minimal Mistakes Jekyll Theme.

**Live site**: https://ShiyuWAN3.github.io

## Development Commands

```bash
# Install dependencies
bundle install        # Ruby gems
npm install           # Node.js packages (for JS minification)

# Local development server (with live reload)
jekyll serve -l -H localhost
# Visit http://localhost:4000

# JavaScript minification
npm run uglify        # Minify JS to assets/js/main.min.js
npm run watch:js      # Watch and auto-rebuild JS
```

### Docker Alternative
```bash
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

## Architecture

**Tech Stack**: Jekyll (Ruby) + Liquid templates + kramdown Markdown + SCSS

**Content Collections**: Publications, Talks, Teaching, Portfolio, Blog Posts - each defined in `_config.yml` with YAML frontmatter for metadata.

### Key Directories
- `_config.yml` - Main site configuration, author info, collection definitions
- `_pages/` - Static pages (about.md, cv.md, publications.md, etc.)
- `_publications/`, `_talks/`, `_teaching/` - Academic content collections
- `_posts/` - Blog posts (format: `YYYY-MM-DD-title.md`)
- `_layouts/` - Page layout templates (default, single, archive, talk)
- `_includes/` - Reusable HTML/Liquid components
- `_sass/` - SCSS stylesheets
- `_data/navigation.yml` - Top navigation menu structure
- `markdown_generator/` - Python scripts to generate content from TSV files
- `images/` - Image assets including profile photo
- `files/` - Downloadable PDFs and documents

## Content Workflow

### Bulk Content Generation
For publications/talks, edit the TSV files then run the Python scripts:
```bash
cd markdown_generator
python publications.py   # Generates _publications/*.md from publications.tsv
python talks.py          # Generates _talks/*.md from talks.tsv
```

### Manual Content
Create `.md` files directly in the appropriate collection directory with YAML frontmatter:
```yaml
---
title: "Paper Title"
collection: publications
permalink: /publication/2024-paper-name
date: 2024-01-15
venue: 'Journal Name'
---
Content here...
```

## Deployment

Automatic via GitHub Pages - push to `master` branch triggers Jekyll build and deployment. No manual build step required.
