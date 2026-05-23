# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal website and blog at [gloor.fyi](https://www.gloor.fyi), built with [Quarto](https://quarto.org). Content is written in `.qmd` files (Quarto Markdown). The custom domain (`www.gloor.fyi`) lives in `CNAME`, which is listed under `resources:` in `_quarto.yml` so it gets copied into the rendered `_site/`.

## Commands

```bash
# Preview the site with live reload
quarto preview

# Build the site (output goes to _site/)
quarto render
```

Blog posts containing R code chunks use `freeze: true` (set in `posts/_metadata.yml`), so R does not need to be installed to build the site, frozen outputs in `_freeze/` are used instead. To re-execute a post's code, run `quarto render posts/<post-dir>/index.qmd --no-freeze`.

## Structure

- `_quarto.yml`: site-wide config: title, navbar, theme, fonts
- `theme.scss`: all visual styling (Solarized-inspired palette, typography, syntax highlighting overrides)
- `styles.css`: additional CSS (currently empty, for ad-hoc overrides)
- `index.qmd`: homepage; renders as a Quarto listing of `posts/`
- `posts/<slug>/index.qmd`: individual blog posts; each post is its own directory
- `posts/_metadata.yml`: defaults applied to every post (author, freeze, fig-format, title-block-banner)
- `projects.qmd`: projects page
- `about.qmd`: bio page
- `_site/`: built output (gitignored, but `CNAME` inside is copied as a resource)
- `_freeze/`: frozen computational outputs for R code chunks

## Adding a new blog post

Create `posts/<slug>/index.qmd` with frontmatter like:

```yaml
---
title: "Post Title"
date: "YYYY-MM-DD"
categories: [tag1, tag2]
toc: true
---
```

Set `draft: true` to keep it out of the listing while writing. Defaults inherited from `posts/_metadata.yml`: `author: Joshua Gloor`, `date-modified: last-modified`, `fig-format: svg`, `freeze: true`, and `title-block-banner: true` (which is why posts have the banner-style header but top-level pages like `about.qmd` don't).

## Theming

All colors are defined as SCSS variables at the top of `theme.scss`. The palette is Solarized Light (`$sol-*` variables) with a neutral warm-white body. Syntax highlighting is manually overridden in `theme.scss` using `span.*` selectors because Quarto's built-in `solarized` highlight style doesn't match the Solarized spec precisely.
