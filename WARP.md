# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

**NOESIS Intelligence Value** is a Mozambican company website showcasing their data center infrastructure services. The site is a one-page application (SPA) built with vanilla HTML/CSS/JavaScript, Bootstrap 5, jQuery, and AOS (Animate On Scroll) animations. The website is bilingual (Portuguese/English) and presents NOESIS as a pioneer in digital transformation for Mozambique.

## Development Commands

### Viewing the Website
Since this is a static HTML/CSS/JS website with no build process:

```bash
# Open directly in browser (Windows)
start index.html

# Or use a local server (if Python is installed)
python -m http.server 8000

# Or use VS Code Live Server extension
# Right-click index.html → "Open with Live Server"
```

### Version Control
```bash
# View recent changes
git --no-pager log --oneline -10

# Check current status
git status

# View uncommitted changes
git --no-pager diff

# Stage and commit changes
git add .
git commit -m "Description of changes"
```

## Architecture and Structure

### File Organization

```
Noesis/
├── index.html              # Main entry point - single-page application
├── CSS/
│   ├── final-design.css   # Primary custom styles (SCSS-like syntax)
│   ├── navbar.css         # Navigation-specific styles
│   └── style-2.css        # Additional custom styles
├── JS/
│   ├── main.js            # Primary JavaScript (jQuery-based navbar/mobile menu)
│   ├── navbar.js          # Additional navbar functionality
│   └── language.js        # Translation functionality (inline in index.html)
├── Assets/
│   ├── images/            # All visual assets (logos, backgrounds, team photos)
│   └── videos/            # Video assets if any
└── HTML/
    └── old-version.html   # Previous version for reference
```

### Key Technical Details

**Frontend Stack:**
- Pure HTML5, CSS3, JavaScript (ES5+)
- Bootstrap 5.3.2 (from CDN)
- jQuery 3.3.1 (legacy dependency for plugins)
- AOS 2.3.1 (scroll animations)
- Font Awesome 6.5.0 (icons)
- Ubuntu font family from Google Fonts

**No Build System:** This project does not use npm, webpack, or any bundler. All dependencies are loaded via CDN.

### Page Structure (SPA Sections)

The `index.html` file contains these main sections (all on one page, linked via anchor navigation):

1. **#inicio** - Hero section with company tagline
2. **#sobre** - About section (company overview, vision, mission)
3. **#servicos** - Services/Areas of operation
4. **#diferenciais** - Strategic objectives (carousel component)
5. **#porque** - "Why NOESIS?" competitive advantages
6. **#parcerias** - Partnerships (energy needs & benefits modals)
7. **#sustentabilidade** - Sustainability commitment
8. **#implementacao** - Implementation timeline
9. **#lideranca** - Leadership team
10. **#contacto** - Contact form and information

### Internationalization (i18n)

**Translation System:**
- Bilingual support: Portuguese (default) and English
- Implemented via inline JavaScript object (`translations`) at the end of `index.html`
- Elements use `data-key` attributes that map to translation keys
- Language switcher buttons toggle between `pt` and `en`

**To add/modify translations:**
1. Locate the `translations` object in `index.html` (around line 1198)
2. Add or modify keys in both `pt` and `en` objects
3. Add `data-key="your.key"` attribute to HTML elements

### Styling Architecture

**CSS Structure:**
- `final-design.css` uses SCSS-like nested syntax (but is actually CSS)
- Heavy use of Bootstrap 5 utility classes
- Custom color palette:
  - Primary green: `#8ED138` / `#92CA63`
  - Corporate blue: `#1E3A8A` / `#2A3B65`
  - Dark gray: `#262626` / `#696969`
  - Background: `#F5F5F5`

**Responsive Design:**
- Mobile-first approach
- Breakpoints follow Bootstrap 5 standards (sm, md, lg, xl)
- Custom mobile menu implementation in `main.js`

### JavaScript Patterns

**jQuery Dependencies:**
- Menu cloning for mobile navigation
- Sticky header functionality (`jquery.sticky.js`)
- Off-canvas mobile menu toggle

**Vanilla JS:**
- Bootstrap carousel controls (strategic objectives section)
- Language switcher functionality
- AOS scroll animations initialization

**Important Note:** The codebase mixes jQuery and vanilla JavaScript. When adding features:
- Use vanilla JS for new features when possible
- Maintain jQuery syntax only for existing menu/navigation code

## Common Development Tasks

### Modifying Content

**Text Changes:**
1. For bilingual content: Update the `translations` object in `index.html`
2. For static content: Directly edit HTML elements

**Images:**
- Place new images in `Assets/images/`
- Reference using relative paths: `Assets/images/filename.png`
- Key images: logos (`noesis_logo_white.png`, `noesis_logo_black.png`), team photos, backgrounds

### Adding New Sections

When adding a new section to the one-page layout:

1. Add navigation link in navbar (`<ul class="site-menu"...>`)
2. Create section with appropriate `id` attribute
3. Add translations for the section in both `pt` and `en`
4. Apply consistent styling using existing section patterns
5. Add AOS animations for scroll effects

### Working with Forms

The contact form (`#contacto`) is currently **client-side only** (no backend submission). To implement:

1. Add form action handler in JavaScript
2. Consider using services like Formspree, EmailJS, or build a backend endpoint
3. Add validation feedback using Bootstrap 5 validation classes

### Animation Guidelines

- AOS is initialized globally: `AOS.init()`
- Add animations via data attributes:
  - `data-aos="fade-up"` - animation type
  - `data-aos-delay="800"` - delay in milliseconds
  - `data-aos-offset="0"` - offset from trigger point
  - `data-aos-easing="linear"` - easing function

## Project-Specific Guidelines

### Company Branding
- Primary brand color is green (`#8ED138`), not blue
- Maintain professional, corporate tone
- All content should support NOESIS positioning as Mozambique's tech infrastructure pioneer

### Content Language
- Default language: Portuguese (pt)
- Keep translations synchronized when updating content
- Technical terms often remain in English even in Portuguese text

### Browser Support
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Bootstrap 5 does not support IE11
- Mobile responsiveness is critical (large mobile user base in target market)

### Asset Management
- Keep images optimized for web (compress before adding)
- Use WebP format where possible for better performance
- Maintain aspect ratios for team photos and background images

### Performance Considerations
- All external dependencies are CDN-hosted
- Consider adding loading="lazy" to images below fold
- AOS animations should be tested on slower devices/connections

## Development Workflow

1. **Before Making Changes:** Check `git status` and review recent commits
2. **Test Locally:** Open `index.html` in browser or use local server
3. **Cross-browser Testing:** Verify in Chrome, Firefox, and Safari
4. **Mobile Testing:** Use browser DevTools responsive mode
5. **Translation Check:** Switch between PT/EN to verify both languages
6. **Commit:** Use descriptive commit messages following existing pattern

## Important Files Reference

- `index.html` - Complete single-page application, contains all structure and embedded scripts
- `CSS/final-design.css` - Main styling, section-specific rules
- `CSS/navbar.css` - Navigation and header styles
- `JS/main.js` - Mobile menu, sticky header, menu cloning logic
- `README.md` - Project brief and requirements (Portuguese)
