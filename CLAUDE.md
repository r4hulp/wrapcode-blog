# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

wrapcode is a personal developer blog built with the MultiTerm Astro theme. It features multiple color schemes (59 Shiki themes) and terminal-inspired aesthetics for showcasing programming content with beautiful syntax highlighting.

## Common Commands

### Development
- `npm run dev` - Start development server
- `npm run build` - Build the site for production
- `npm run postbuild` - Runs after build to generate search index with pagefind
- `npm run preview` - Preview the built site locally
- `npm run format` - Format code with Prettier

### Testing the build
To test a complete build: `npm run build && npx serve dist`

## Architecture

### Core Configuration
- **`src/site.config.ts`** - Central configuration file for the entire site including themes, navigation, social links, and Giscus comments
- **`astro.config.mjs`** - Astro configuration with markdown plugins, integrations, and build settings

### Content Management
- **Content Collections** (defined in `src/content.config.ts`):
  - `posts` - Blog posts with frontmatter schema for title, date, tags, cover images
  - `home` - Homepage content with optional avatar and GitHub calendar
  - `addendum` - Additional content pages
- **Content Directory** (`src/content/`):
  - `posts/` - Markdown/MDX blog posts
  - `home.md` - Homepage content
  - `addendum.md` - Footer addendum content

### Theming System
- Supports three modes: single theme, light/dark auto-switching, or user-selectable themes
- Themes are Shiki syntax highlighting themes that color the entire site
- Theme data processing handled in `src/settings-utils.ts`
- CSS variables dynamically updated based on selected theme

### Key Components
- **Layouts**: `src/layouts/Layout.astro` - Base layout wrapper
- **Page Components**: 
  - `src/pages/index.astro` - Homepage
  - `src/pages/posts/[slug].astro` - Individual blog posts
  - `src/pages/posts/[...page].astro` - Paginated post listings
- **UI Components**: Header, Footer, Search, Pagination, Table of Contents, Theme Selectors
- **React Integration**: GitHub calendar component (`src/components/ReactGithubCalendar.tsx`)

### Markdown Processing
Rich markdown pipeline with plugins:
- **Remark plugins**: Reading time, descriptions, admonitions, math, emoji shortcodes
- **Rehype plugins**: Slug generation, autolink headings, external links, image unwrapping, KaTeX math rendering
- Custom plugins in `src/plugins/` for admonitions, emoji, and pixelated images

### Features
- **SEO**: Automatic social card generation using Satori
- **Search**: Client-side search powered by Pagefind
- **Comments**: GitHub Discussions integration via Giscus
- **RSS/Sitemap**: Built-in feed and sitemap generation
- **Responsive**: Mobile-first design with Tailwind CSS v4

### File Structure Notes
- Static assets in `public/`
- TypeScript types in `src/types.ts`
- Utilities in `src/utils.ts`
- Global styles in `src/styles/global.css`
- Icons as SVG files in `src/icons/`

## Development Notes

### Adding New Posts
Create `.md` or `.mdx` files in `src/content/posts/` with required frontmatter (title, published date). Optional: description, tags, cover image, draft status.

### Customizing Themes
Modify the `themes.include` array in `src/site.config.ts` to change available color schemes. The `themes.mode` setting controls how themes are presented to users.

### Deployment
The site builds to static files in `dist/` directory. The `postbuild` script generates search indexes automatically.