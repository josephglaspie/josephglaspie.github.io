# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a professional resume website for Joseph Glaspie, Senior Cloud Engineer. The site is a static website (HTML/CSS/JavaScript) designed to be deployed on GitHub Pages. It features a modern, responsive design that is also optimized for printing to PDF.

## Multi-Agent Architecture

This project uses coordinating agents defined in the `agents/` directory. Each agent has specific responsibilities for building and maintaining the resume site.

### Agent Roles

1. **project-setup** (agents/project-setup.md)
   - Model: Sonnet (cost-effective for planning)
   - Coordinates overall project architecture
   - Manages deployment workflows
   - Makes final architectural decisions

2. **ui-designer** (agents/ui-designer.md)
   - Model: Inherit (flexible based on task)
   - Designs professional, modern layouts
   - Creates visual hierarchy and color schemes
   - Ensures responsive and print-friendly design

3. **frontend-developer** (agents/frontend-developer.md)
   - Model: Inherit (flexible based on task)
   - Implements HTML/CSS/JavaScript
   - Ensures accessibility and performance
   - Optimizes for all browsers and devices

4. **code-reviewer** (agents/code-reviewer.md)
   - Model: Opus (thorough analysis)
   - Reviews code quality and accessibility
   - Validates HTML/CSS standards
   - Ensures production readiness

### Agent Coordination Workflow

```
project-setup → ui-designer → frontend-developer → code-reviewer → [feedback loop]
```

When making changes:
1. ui-designer creates design specifications
2. frontend-developer implements the design
3. code-reviewer validates quality and accessibility
4. project-setup coordinates iterations

See `agents/README.md` for detailed coordination protocols.

## Development

### Project Structure

```
docs/
├── index.html          # Main resume page (single page application)
├── css/
│   ├── style.css      # Main styles with CSS variables
│   └── print.css      # Print-optimized styles
└── js/
    └── script.js       # Progressive enhancement JavaScript
```

### Technology Stack

- **HTML5**: Semantic markup, accessibility-first
- **CSS3**: Modern features (Grid, Flexbox, Custom Properties)
- **Vanilla JavaScript**: No frameworks or dependencies
- **GitHub Pages**: Static site hosting
- **GitHub Actions**: Automated deployment

### Local Development

```bash
# Serve locally (any static server works)
python3 -m http.server 8000 --directory docs

# Open in browser
open http://localhost:8000

# Or simply open the file
open docs/index.html
```

### File Editing

**To update resume content:**
- Edit `docs/index.html`
- All content is in semantic HTML sections
- Contact info is in the `<header>` element

**To modify styling:**
- Edit `docs/css/style.css`
- Uses CSS custom properties in `:root` for easy theming
- Mobile-first responsive design with breakpoints at 480px and 768px

**To adjust print output:**
- Edit `docs/css/print.css`
- Optimized for black & white printing
- Includes proper page break handling

**To add interactivity:**
- Edit `docs/js/script.js`
- Progressive enhancement approach
- Respects prefers-reduced-motion

## Design System

### CSS Custom Properties

All design tokens are defined in `:root` in `docs/css/style.css`:

```css
:root {
    /* Colors */
    --primary-color: #2563eb;
    --text-primary: #1f2937;

    /* Spacing */
    --spacing-sm: 0.75rem;
    --spacing-md: 1rem;
    --spacing-lg: 1.5rem;

    /* Typography */
    --font-primary: system font stack
}
```

To change the color scheme, modify these variables.

### Responsive Breakpoints

- **Mobile**: < 480px
- **Tablet**: 480px - 768px
- **Desktop**: > 768px

Mobile-first approach: base styles are for mobile, media queries add complexity for larger screens.

### Typography Scale

- **h1**: 3rem (48px) on desktop, 1.875rem (30px) on mobile
- **h2**: 1.875rem (30px), section titles
- **h3**: 1.5rem (24px), job titles
- **body**: 16px base, 15px on small mobile

## Key Features

### 1. Responsive Design

The site uses CSS Grid and Flexbox for responsive layouts:
- Header uses flexbox for contact information
- Skills section uses CSS Grid with auto-fit
- Mobile navigation stacks vertically

### 2. Accessibility

- Semantic HTML5 elements (`<header>`, `<main>`, `<section>`, `<article>`)
- ARIA labels on interactive elements
- Sufficient color contrast (WCAG AA)
- Keyboard navigation support
- Screen reader optimized

### 3. Print Optimization

Dedicated print stylesheet (`print.css`):
- Removes colors and backgrounds
- Adjusts typography for print
- Manages page breaks
- Hides print button
- Converts to grayscale

Print using browser's print dialog or the "Print Resume" button.

### 4. Performance

- Zero external dependencies
- Minimal file sizes (<50KB total)
- No render-blocking resources
- Inline SVG icons
- Lazy loading animations (respects prefers-reduced-motion)

## Making Content Changes

### Add New Job Experience

1. Open `docs/index.html`
2. Find the `<section id="experience">` element
3. Add new `<article class="job">` block:

```html
<article class="job">
    <div class="job-header">
        <div>
            <h3 class="job-title">Job Title</h3>
            <p class="company">Company Name</p>
        </div>
        <div class="job-period">2020 - Present</div>
    </div>
    <ul class="job-achievements">
        <li>Achievement 1</li>
        <li>Achievement 2</li>
    </ul>
</article>
```

### Update Skills

1. Open `docs/index.html`
2. Find `<section id="skills">`
3. Edit skill categories and items within the grid

### Change Colors

1. Open `docs/css/style.css`
2. Modify CSS variables in `:root`:
   - `--primary-color`: Main theme color
   - `--primary-dark`: Darker variant for hover states
   - `--text-primary`: Main text color

## Deployment

### GitHub Pages Setup

The site automatically deploys when you push to the main branch:

1. Ensure GitHub Pages is enabled in repository settings
2. Set source to "Deploy from a branch"
3. Select `main` branch, `/(root)` folder
4. GitHub Actions workflow (`.github/workflows/deploy.yml`) handles deployment

### Manual Deployment

To deploy to other hosting:
1. Copy entire `docs/` directory
2. Upload to any static hosting service
3. No build process required - just static files

## Common Tasks

### Preview Changes Locally

```bash
# Simple HTTP server
python3 -m http.server 8000 --directory docs

# Or use any other static server
npx http-server docs
```

### Generate PDF

1. Open site in browser
2. Click "Print Resume" button
3. Select "Save as PDF" in print dialog
4. Adjust margins if needed (use "None" for best results)

### Validate HTML/CSS

```bash
# HTML validation (requires validator.nu)
curl -H "Content-Type: text/html; charset=utf-8" \
  --data-binary @docs/index.html \
  https://validator.w3.org/nu/?out=text

# CSS validation
curl -H "Content-Type: text/css; charset=utf-8" \
  --data-binary @docs/css/style.css \
  "https://jigsaw.w3.org/css-validator/validator"
```

## Browser Support

Tested and working in:
- Chrome/Edge 120+
- Firefox 120+
- Safari 17+
- iOS Safari 17+
- Chrome Android 120+

Uses modern CSS features:
- CSS Grid
- CSS Custom Properties
- Flexbox
- CSS Animations

## Troubleshooting

### Styles Not Loading

Check file paths in `index.html`:
- CSS: `<link rel="stylesheet" href="css/style.css">`
- JS: `<script src="js/script.js"></script>`

Paths are relative to `docs/index.html`.

### Print Styles Not Working

- Ensure `<link rel="stylesheet" href="css/print.css" media="print">` is in `<head>`
- Test with browser's print preview (Cmd/Ctrl + P)

### Icons Not Showing

Icons are inline SVG in the HTML. If missing:
- Check for proper SVG markup in `index.html`
- Ensure the `<svg>` elements have proper `viewBox` attributes

## Future Enhancements

Consider these when extending the project:

1. **Dark Mode**: Add toggle and dark theme colors
2. **Animations**: Enhance with Intersection Observer animations
3. **Multi-language**: Add language switcher for international opportunities
4. **Portfolio Section**: Add project showcase with images
5. **Contact Form**: Integrate with form service (Formspree, etc.)
6. **Analytics**: Add Google Analytics or privacy-friendly alternative
7. **SEO**: Add OpenGraph and Twitter Card meta tags
8. **PWA**: Add service worker for offline capability

## Code Style Guidelines

### HTML

- Use semantic elements
- One `<h1>` per page
- Proper heading hierarchy (h1 → h2 → h3)
- ARIA labels where needed
- Descriptive alt text for images

### CSS

- Mobile-first approach
- BEM-like naming (block__element--modifier)
- CSS custom properties for values used multiple times
- Comments for major sections
- Group related properties together

### JavaScript

- Progressive enhancement (works without JS)
- ES6+ syntax (const/let, arrow functions)
- Respect `prefers-reduced-motion`
- No dependencies - vanilla JS only
- Comment complex logic

## Performance Targets

- **First Contentful Paint**: < 1.0s
- **Largest Contentful Paint**: < 2.5s
- **Total Blocking Time**: < 200ms
- **Cumulative Layout Shift**: < 0.1
- **Time to Interactive**: < 3.0s

Current metrics should be validated with Lighthouse.

## Accessibility Checklist

- ✅ Semantic HTML structure
- ✅ Proper heading hierarchy
- ✅ Color contrast WCAG AA (4.5:1 for text)
- ✅ Keyboard navigation
- ✅ Screen reader tested
- ✅ Focus indicators visible
- ✅ No flashing/strobing content
- ✅ Respects prefers-reduced-motion
- ✅ Form labels properly associated
- ✅ Links have descriptive text

## Security Notes

This is a static site with no backend, so security concerns are minimal:

- No user input processing
- No cookies or local storage
- No external scripts or dependencies
- All resources served from same origin
- Contact information is public (as intended for resume)

## License

© 2025 Joseph Glaspie. All rights reserved.
