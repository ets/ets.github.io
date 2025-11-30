# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is Eric Simmerman's personal blog (ericsimmerman.com) built with Hugo using the LoveIt theme. The site is deployed via GitHub Actions to GitHub Pages.

## Author Context

Eric is cofounder of [Qualytics](https://www.qualytics.ai), a data quality management SaaS company founded in early 2022. The platform uses machine learning to automatically infer and apply data quality checks, identifying anomalies as new data arrives. Key themes:

- **Data quality automation** - Moving beyond manual rule creation to ML-driven anomaly detection
- **Known unknowns vs unknown unknowns** - Monitoring expected issues while discovering unexpected ones
- **Separation of transformation and assertion** - Philosophical approach to data pipeline architecture
- **Startup building** - Lessons from founding and scaling a B2B SaaS company

## Commands

**Local development:**
```bash
hugo serve
```

**Build for production:**
```bash
hugo --minify
```

## Deployment

Push to the `main` branch triggers GitHub Actions which builds and deploys to GitHub Pages (publishes to `master` branch). No manual deployment needed.

## Content Structure

- `content/blog/` - Blog posts (markdown files with frontmatter)
- `content/about/` - About page
- `static/images/` - Static images referenced in posts
- `config.toml` - Site configuration

## Writing Blog Posts

Blog posts use this frontmatter structure:
```yaml
---
title: Post Title
date: YYYY-MM-DD
type: posts
tags:
- tag1
- tag2
---
```

Posts are stored as `content/blog/YYYY-MM-DD-slug.md`. The permalink format is `/blog/:year/:month/:day/:title/`.

## Writing Style Guidelines

Eric's writing style based on existing posts:

- **Direct and conversational** - Writes like talking to a peer, not lecturing
- **Story-driven** - Opens with personal experience or real-world problem before diving into concepts
- **Technical but accessible** - Includes code snippets and specifics when relevant, but explains the "why"
- **Concise paragraphs** - Gets to the point, avoids fluff
- **Uses bullet points** - For takeaways and lists, often with bold lead-ins
- **Links contextually** - Weaves in relevant links naturally (Qualytics, past employers, references)
- **Ends with punch** - Short memorable closers ("Onward & Upward!", "Set math logic was restored and the universe once again in balance")
- **Authentic voice** - Uses phrases like "Guh.", "c'est la vie", "down the rabbit hole"
- **No excessive selling** - Mentions Qualytics where relevant but leads with value/insight

## Theme

Uses LoveIt theme (in `themes/LoveIt/`). Theme customizations should be made by overriding files in the project root rather than modifying theme files directly.
