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

**Fixed Header Pattern**: The header remains fixed at the top with:
- Site title in the left
- Navigation links displayed inline
- Active link indicated with bottom border

## File Structure

```
/
├── index.html          # Complete website (HTML, CSS, JS)
└── public/
    └── Federico_Comel_CV.pdf  # CV document opened in new tab
```

## Development

**No Build Process**: Open `index.html` directly in a browser. No compilation, bundling, or dependencies needed.

**Testing Locally**: Use any local server or simply open the file:
```bash
open index.html
# or
python3 -m http.server 8000
```

## Content Editing Guidelines

Content is edited directly in `index.html`:

1. **Adding Content**: Edit within `<section>` tags in the `<main>` element
2. **Section IDs**: Keep section `id` attributes unchanged to preserve navigation
3. **Adding New Sections**:
   - Add link in `<nav>` element (line ~204-210)
   - Create new `<section>` with matching `id`
4. **Formatting**: Use semantic HTML only (p, ul, ol, h2, h3, em, strong, a)

## Styling Philosophy

- Minimalist design with Times New Roman for body, Arial for navigation
- Black text on white background
- No external CSS frameworks or libraries
- Responsive via media queries for mobile (breakpoint: 600px)
- Animations limited to simple fade-in on section display

## JavaScript Behavior

The inline JavaScript (lines 331-398) handles:
- Hash-based routing and section visibility
- Active state management for navigation links
- CV link opens PDF in new tab instead of navigating
- Graceful degradation (works without JavaScript via CSS `:target`)
