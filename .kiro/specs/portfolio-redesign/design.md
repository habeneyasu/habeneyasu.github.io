# Design Document

## Overview

This document describes the technical design for the portfolio-redesign feature. The implementation targets `index.html` and `style.css` only — no build tools, no frameworks, no new dependencies. All changes are backward-compatible and the site must continue to work as a standalone static file.

The design is organized into the same areas as the requirements: CSS system, section reordering, dark mode, accessibility, hero simplification, architecture cards, section rename, inline style removal, scroll-to-top, entrance animations, print styles, and component standardization.

---

## Architecture

The site is a single-page static document. There is no server, no bundler, and no module system. All JavaScript runs inline at the bottom of `<body>`. All styles live in `style.css` with a small critical-CSS `<style>` block in `<head>` for above-the-fold rendering.

The redesign adds no new files and no new CDN dependencies. The only structural additions are:

- A `data-theme` attribute on `<html>` (managed by JS)
- A `#skip-to-content` anchor before `<nav>`
- A `#scroll-to-top` button before `</body>`
- A dark mode toggle button inside `.navbar .container`

Mermaid.js is already loaded from CDN. Dark mode will re-initialize Mermaid with `theme: 'dark'` when the dark theme is active.

---

## CSS System Design

### New Custom Properties

Added to `:root` alongside existing tokens:

```css
/* Border radius scale */
--radius-sm: 6px;
--radius-md: 12px;
--radius-lg: 16px;
--radius-xl: 24px;

/* Transition timing */
--transition-fast: 0.15s ease;
--transition-base: 0.25s ease;
--transition-slow: 0.35s ease;
```

### Duplicate Removal

The current `:root` block has `--text-light: #4b5563` which duplicates `--text-secondary: #4b5563`. `--text-light` will be removed and all usages replaced with `--text-secondary`.

All hardcoded `border-radius` values will be replaced:
- `6px` → `--radius-sm`
- `8px` → `--radius-sm` (contextually — buttons, small elements)
- `10px` → `--radius-md` (contextually — medium containers)
- `12px` → `--radius-md`
- `16px` → `--radius-lg`
- `20px` (pill tags) → kept as `20px` or extracted to `--radius-pill: 20px`

All hardcoded transition durations will be replaced:
- `0.2s` → `--transition-fast`
- `0.25s` → `--transition-base`
- `0.3s` → `--transition-slow`

### Dead Code Removal

The `.focus-areas-grid`, `.focus-area-card`, `.focus-area-icon`, `.focus-area-title`, `.focus-area-description` rules will be removed since the Focus Areas section is being removed from the HTML.

---

## Dark Mode Design

### Color Token Strategy

Dark mode overrides are applied via `[data-theme="dark"]` on `<html>`. This avoids `prefers-color-scheme` media query conflicts with the manual toggle and allows JS to control the active theme.

```css
[data-theme="dark"] {
  --bg-primary: #0f172a;
  --bg-secondary: #1e293b;
  --bg-tertiary: #334155;
  --text-primary: #f1f5f9;
  --text-secondary: #94a3b8;
  --border-color: #334155;
  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.3);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.4);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.4);
  --shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.4);
}
```

Component-specific dark overrides (navbar background, card backgrounds, timeline content, etc.) are added as `[data-theme="dark"] .component` rules grouped at the end of style.css.

### Navbar Dark Mode Toggle Button

The toggle button is placed after `.nav-brand` and before `.nav-toggle` in the DOM:

```html
<button class="theme-toggle" id="theme-toggle" aria-label="Switch to dark mode">
  <span class="theme-toggle-icon">🌙</span>
</button>
```

The icon swaps to ☀️ when dark mode is active. The `aria-label` updates via JS.

### JS Theme Logic

```javascript
// On load: check localStorage, then OS preference
const savedTheme = localStorage.getItem('theme');
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
const initialTheme = savedTheme || (prefersDark ? 'dark' : 'light');
document.documentElement.setAttribute('data-theme', initialTheme);

// Toggle handler
document.getElementById('theme-toggle').addEventListener('click', () => {
  const current = document.documentElement.getAttribute('data-theme');
  const next = current === 'dark' ? 'light' : 'dark';
  document.documentElement.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
  updateToggleButton(next);
  // Re-initialize Mermaid with appropriate theme
  mermaid.initialize({ startOnLoad: false, theme: next === 'dark' ? 'dark' : 'neutral' });
  document.querySelectorAll('.mermaid[data-processed]').forEach(el => {
    el.removeAttribute('data-processed');
  });
  mermaid.init(undefined, '.mermaid');
});
```

---

## Section Reordering Design

### New DOM Order

```
<nav>
<main id="main-content">
  #hero
  #about          (includes Case Study as subsection)
  #experience
  #skills
  #projects-ai-ml (AI/ML projects)
  #projects-software
  #projects-additional
  #architecture
  #github
  #insights
  #contact
</main>
<footer>
<button id="scroll-to-top">
```

### Case Study Integration

The Case Study section (`#case-study`) is moved inside `#about`, rendered after the expertise cards grid, as a visually distinct subsection with a `<h3>` heading. The `section` element becomes a `<div class="case-study-subsection">` to avoid nested landmark conflicts. The `id="case-study"` is preserved on the wrapper div so existing anchor links continue to work.

### Navbar Links Update

```html
<ul class="nav-menu" id="nav-menu">
  <li><a href="#about">About</a></li>
  <li><a href="#experience">Experience</a></li>
  <li><a href="#skills">Skills</a></li>
  <li><a href="#projects-ai-ml">Projects</a></li>
  <li><a href="#architecture">Architecture</a></li>
  <li><a href="#github">GitHub</a></li>
  <li><a href="#insights">Insights</a></li>
  <li><a href="#contact">Contact</a></li>
</ul>
```

The "Case Study" link is removed from the navbar (it's now a subsection of About). The "Focus Areas" link is removed.

---

## Accessibility Design

### Skip Link

Inserted as the very first child of `<body>`, before `<nav>`:

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 16px;
  padding: 8px 16px;
  background: var(--primary-color);
  color: white;
  border-radius: var(--radius-sm);
  font-weight: 600;
  text-decoration: none;
  z-index: 9999;
  transition: top var(--transition-fast);
}

.skip-link:focus {
  top: 16px;
}
```

### Focus Visible Styles

Added globally after the reset block:

```css
:focus-visible {
  outline: 2px solid var(--primary-color);
  outline-offset: 3px;
  border-radius: var(--radius-sm);
}

/* Remove outline for mouse users */
:focus:not(:focus-visible) {
  outline: none;
}
```

All existing `outline: none` rules on interactive elements are removed.

---

## Hero Simplification Design

The third button (`btn-resume`) is removed from `.hero-buttons`. The Resume download button is added to the Contact section alongside the existing contact methods:

```html
<!-- In #contact section -->
<div class="contact-resume">
  <a href="Haben_Eyasu_Akelom_Resume.pdf" class="btn-resume-contact" download="Haben_Eyasu_Akelom_Resume.pdf">
    📄 Download Resume
  </a>
</div>
```

The `.btn-resume` CSS class is kept (it's used by `.btn-resume-contact` which shares the same styles). No visual change to the contact section layout — the resume button already exists there.

---

## Architecture Cards Fix

The `max-width: 600px` rule is removed from `.architecture-card` (or whichever selector applies it). The cards use the existing grid/flex layout and will naturally fill their column.

A quick audit of style.css confirms the constraint appears on `.architecture-card` or a parent wrapper. The fix is a single property removal.

---

## Scroll-To-Top Design

### HTML

```html
<button id="scroll-to-top" class="scroll-to-top" aria-label="Scroll to top">
  ↑
</button>
```

### CSS

```css
.scroll-to-top {
  position: fixed;
  bottom: 32px;
  right: 32px;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--primary-color);
  color: white;
  border: none;
  font-size: 1.25rem;
  cursor: pointer;
  opacity: 0;
  visibility: hidden;
  transition: opacity var(--transition-base), visibility var(--transition-base), transform var(--transition-base);
  z-index: 900;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-md);
}

.scroll-to-top.visible {
  opacity: 1;
  visibility: visible;
}

.scroll-to-top:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}
```

### JS

```javascript
const scrollToTopBtn = document.getElementById('scroll-to-top');

window.addEventListener('scroll', () => {
  if (window.scrollY >= 400) {
    scrollToTopBtn.classList.add('visible');
  } else {
    scrollToTopBtn.classList.remove('visible');
  }
}, { passive: true });

scrollToTopBtn.addEventListener('click', () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
});
```

---

## Entrance Animations Design

### CSS

```css
.animate-on-scroll {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 500ms ease, transform 500ms ease;
}

.animate-on-scroll.animated {
  opacity: 1;
  transform: translateY(0);
}

@media (prefers-reduced-motion: reduce) {
  .animate-on-scroll {
    opacity: 1;
    transform: none;
    transition: none;
  }
}
```

### JS

```javascript
const animatedElements = document.querySelectorAll(
  '.section, .project-card, .timeline-item, .skill-category, .education-card'
);

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('animated');
      observer.unobserve(entry.target); // animate once only
    }
  });
}, { threshold: 0.1 });

animatedElements.forEach(el => {
  el.classList.add('animate-on-scroll');
  observer.observe(el);
});
```

The `prefers-reduced-motion` check is handled entirely in CSS — no JS branching needed.

---

## Print Styles Design

```css
@media print {
  .navbar,
  .scroll-to-top,
  .theme-toggle,
  .hero-buttons,
  .hero-social,
  .footer-social,
  .skip-link {
    display: none !important;
  }

  body {
    color: #000 !important;
    background: #fff !important;
  }

  .section,
  .about-content,
  .projects-grid,
  .skills-grid {
    display: block !important;
  }

  .project-card,
  .skill-category,
  .timeline-content,
  .education-card {
    box-shadow: none !important;
    background: #fff !important;
    border: 1px solid #ccc !important;
    break-inside: avoid;
  }

  .skill-tag-hidden {
    display: inline-block !important;
  }

  .skill-more-btn {
    display: none !important;
  }

  * {
    background-image: none !important;
  }
}
```

---

## Inline Style Removal

The GitHub graph `<img>` currently has inline styles like `style="width:100%; border-radius:8px"`. These move to a CSS class:

```css
.github-graph-img {
  width: 100%;
  border-radius: var(--radius-sm);
}
```

```html
<!-- Before -->
<img src="..." style="width:100%; border-radius:8px" ...>

<!-- After -->
<img src="..." class="github-graph-img" ...>
```

---

## Correctness Properties

### CSS Custom Property Coverage

- Property: For every `border-radius` value in style.css, the value MUST be one of the defined `--radius-*` variables or `50%` (circles) or `--radius-pill` (pill shapes). No raw pixel values for border-radius should remain after the refactor.
- Property: For every `transition` duration in style.css, the value MUST reference one of `--transition-fast`, `--transition-base`, or `--transition-slow`. No raw `0.Xs` duration values should remain.

### Dark Mode Round-Trip

- Property: Toggling dark mode twice (dark → light → dark) MUST result in the same visual state as toggling once (dark). The `data-theme` attribute and `localStorage` value must be consistent after any number of toggles.
- Property: On page reload after setting dark mode, the page MUST load in dark mode (localStorage persistence).

### Section Order Invariant

- Property: The order of `<section id="...">` elements in the DOM MUST match the order of `<a href="#...">` links in the navbar. Any reordering of sections must be reflected in the navbar.

### Scroll-To-Top Visibility Invariant

- Property: The scroll-to-top button MUST be hidden (opacity 0, visibility hidden) when `window.scrollY < 400` and visible when `window.scrollY >= 400`. This is an invariant that holds regardless of scroll direction.

### Entrance Animation Idempotence

- Property: Calling the IntersectionObserver callback on an already-animated element MUST NOT re-animate it. Once `.animated` is added and `observer.unobserve()` is called, the element's state is final.

### Accessibility Focus Invariant

- Property: For every interactive element (a, button) in the DOM, a `:focus-visible` style MUST be defined that produces a visible outline. No interactive element should have `outline: none` without a `:focus-visible` replacement.

### Print Style Completeness

- Property: After applying print styles, the navbar, scroll-to-top button, and hero buttons MUST have `display: none`. All `.skill-tag-hidden` elements MUST be visible.
