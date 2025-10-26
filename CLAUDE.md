# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file, self-contained personal website with no external dependencies, no build tools, and no framework required. The entire site exists in `index.html` with inline CSS and vanilla JavaScript.

## Architecture

**Single-File Structure**: All HTML, CSS, and JavaScript are contained in `index.html`. This design choice prioritizes simplicity and portability.

**Section-Based Navigation**: The site uses a hash-based routing system where:
- Each content section has a unique `id` (home, blog, cv, projects)
- Navigation uses anchor links (`#home`, `#blog`, etc.)
- JavaScript toggles `.active` class to show/hide sections
- CSS `:target` provides fallback for no-JS environments

**Fixed Header and Footer**: The site has:
- Fixed header at top with navigation links (home, blog, projects, cv)
- Fixed footer at bottom with copyright and social links (LinkedIn, Email, Strava)
- Navigation uses underline to indicate active state

**Blog System**: The blog section has two views:
- List view (default): Shows article titles with dates, clickable to open articles
- Article view: Shows full article with view counter stored in localStorage
- Navigation pattern: `#blog` for list, `#blog/article-id` for specific articles

**Projects System**: The projects section displays:
- 3x3 grid of project images with hover effects (scale + overlay text)
- Complex hover animation: images scale up, show title/year on the side
- Non-hovered images fade to 20% opacity when any project is hovered
- Support for detail views via `#projects/project-id` routing pattern

## File Structure

```
/
├── index.html              # Complete website (HTML, CSS, JS)
├── vercel.json             # Vercel deployment configuration
├── package.json            # Minimal package file (no dependencies)
└── public/
    ├── Federico_Comel_CV.pdf
    ├── icon web.png        # Site favicon
    ├── sofa.webp          # Blog article image
    └── projects/           # Project thumbnail images
```

## Development

**No Build Process**: Open `index.html` directly in a browser. No compilation, bundling, or dependencies needed.

**Testing Locally**: Use any local server or simply open the file:
```bash
open index.html
# or
python3 -m http.server 8000
```

## Deployment

**Vercel Deployment**: The site is configured for Vercel with:
- All routes rewrite to `/index.html` (except `/public/*`)
- This enables hash-based routing to work correctly
- Cache-Control headers set for proper CDN behavior

## Content Editing Guidelines

Content is edited directly in `index.html`:

1. **Adding Content**: Edit within `<section>` tags in the `<main>` element
2. **Section IDs**: Keep section `id` attributes unchanged to preserve navigation
3. **Adding Blog Articles**:
   - Add clickable title in `.blog-list-view` with `onclick="showArticle('article-id')"`
   - Create new `<div id="article-id" class="blog-article-view">` with article content
   - View counter will automatically be tracked in localStorage
4. **Adding Projects**:
   - Add new `.project-item` div in the `.project-grid`
   - Include image, link, and overlay with title/year
5. **Adding New Sections**:
   - Add link in `<nav>` element (line ~517-522)
   - Create new `<section>` with matching `id`
6. **Formatting**: Use semantic HTML only (p, ul, ol, h2, h3, em, strong, a)

## Styling Philosophy

- Minimalist design with Helvetica Neue for all text
- Black text on light gray background (#EDECEB)
- No external CSS frameworks or libraries
- Responsive via media queries for mobile (breakpoint: 600px)
- Animations: fade transitions between sections (0.07s), project hover effects (0.3s scale)

## JavaScript Behavior

The inline JavaScript (lines ~706-880) handles:
- Hash-based routing with support for nested routes (`blog/article-id`, `projects/project-id`)
- Section visibility toggling with cross-fade animations
- Blog list/article view switching
- Project grid/detail view switching
- Article view counter using localStorage
- CV link opens PDF in new tab
- Graceful degradation (works without JavaScript via CSS `:target`)

## Key Implementation Details

**Routing Pattern**: Uses hash fragments for client-side routing:
- Simple sections: `#home`, `#blog`, `#projects`
- Nested routes: `#blog/article-moving-abroad`, `#projects/solvo`
- The `showSection()` function parses these paths and manages view state accordingly

**View State Management**:
- Sections use `.active` class for visibility
- Blog uses `.hidden` class on list view and `.active` on article views
- Projects use `.hidden` class on grid view and `.active` on detail views
- All transitions handled via CSS for smooth animations
