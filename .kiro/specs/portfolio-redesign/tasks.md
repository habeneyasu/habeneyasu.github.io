# Implementation Tasks

## Task List

- [x] 1. CSS System Consolidation
  - [x] 1.1 Add `--radius-sm`, `--radius-md`, `--radius-lg`, `--radius-xl`, `--radius-pill` custom properties to `:root` in style.css
  - [x] 1.2 Add `--transition-fast`, `--transition-base`, `--transition-slow` custom properties to `:root` in style.css
  - [x] 1.3 Replace all hardcoded `border-radius` pixel values with the appropriate `--radius-*` variable throughout style.css
  - [x] 1.4 Replace all hardcoded transition durations (0.2s, 0.25s, 0.3s) with the appropriate `--transition-*` variable throughout style.css
  - [x] 1.5 Remove the duplicate `--text-light` variable from `:root` and replace all `var(--text-light)` usages with `var(--text-secondary)`
  - [x] 1.6 Remove dead CSS rules for `.focus-areas-grid`, `.focus-area-card`, `.focus-area-icon`, `.focus-area-title`, `.focus-area-description`

- [x] 2. Section Reordering
  - [x] 2.1 Move the Case Study `<section>` content into the About section as a `<div class="case-study-subsection" id="case-study">` after the expertise cards grid
  - [x] 2.2 Remove the Focus Areas `<section id="focus-areas">` from index.html
  - [x] 2.3 Reorder the remaining top-level sections in index.html to: Hero → About (with Case Study) → Experience → Skills → Projects (AI/ML, Software, Additional) → Architecture → GitHub → Insights → Contact → Footer
  - [x] 2.4 Update the navbar `<ul>` to reflect the new order: About, Experience, Skills, Projects, Architecture, GitHub, Insights, Contact — removing Case Study and Focus Areas links

- [ ] 3. Dark Mode
  - [x] 3.1 Add `[data-theme="dark"]` CSS block to style.css with overrides for all background, text, border, and shadow custom properties
  - [x] 3.2 Add component-specific dark mode overrides for navbar, cards, timeline content, hero section, footer, and code/tag elements
  - [x] 3.3 Add the dark mode toggle button HTML inside `.navbar .container` with `id="theme-toggle"` and appropriate `aria-label`
  - [x] 3.4 Add CSS for `.theme-toggle` button (size, position, icon display, hover state, dark mode variant)
  - [ ] 3.5 Add JS logic to read `localStorage` and `prefers-color-scheme` on page load and set `data-theme` on `<html>`
  - [ ] 3.6 Add JS click handler for the toggle button that updates `data-theme`, saves to `localStorage`, updates `aria-label`, and re-initializes Mermaid with the appropriate theme

- [ ] 4. Accessibility
  - [ ] 4.1 Add the skip link `<a href="#main-content" class="skip-link">Skip to main content</a>` as the first child of `<body>`
  - [ ] 4.2 Add `id="main-content"` to the `<main>` element
  - [ ] 4.3 Add `.skip-link` CSS rules (visually hidden by default, visible on `:focus`)
  - [ ] 4.4 Add global `:focus-visible` CSS rules with a visible outline using `var(--primary-color)`
  - [ ] 4.5 Add `:focus:not(:focus-visible) { outline: none; }` to remove outlines for mouse users without breaking keyboard navigation
  - [ ] 4.6 Remove any existing `outline: none` declarations on interactive elements that lack a `:focus-visible` replacement

- [ ] 5. Hero Simplification
  - [ ] 5.1 Remove the `<a class="btn btn-resume">` Download Resume button from the `.hero-buttons` div in index.html
  - [ ] 5.2 Verify the Resume download button already exists in the Contact section (`.btn-resume-contact`); add it if missing

- [ ] 6. Architecture Cards Fix
  - [ ] 6.1 Locate and remove the `max-width: 600px` constraint from Architecture section card CSS rules in style.css

- [ ] 7. Section Title Rename
  - [ ] 7.1 Change the software projects section heading text from "Featured Software Projects (Top 2)" to "Software Engineering Projects" in index.html

- [ ] 8. Inline Style Removal
  - [ ] 8.1 Add `.github-graph-img` CSS class to style.css with `width: 100%` and `border-radius: var(--radius-sm)`
  - [ ] 8.2 Replace the inline `style` attribute on the GitHub graph `<img>` element with `class="github-graph-img"`

- [ ] 9. Scroll-To-Top Button
  - [ ] 9.1 Add `<button id="scroll-to-top" class="scroll-to-top" aria-label="Scroll to top">↑</button>` before the closing `</body>` tag
  - [ ] 9.2 Add `.scroll-to-top` CSS rules (fixed position, bottom-right, hidden by default, `.visible` state, hover lift, dark mode variant)
  - [ ] 9.3 Add JS scroll event listener that adds/removes `.visible` class at 400px threshold
  - [ ] 9.4 Add JS click handler that calls `window.scrollTo({ top: 0, behavior: 'smooth' })`

- [ ] 10. Section Entrance Animations
  - [ ] 10.1 Add `.animate-on-scroll` and `.animate-on-scroll.animated` CSS rules for the fade-in-up animation
  - [ ] 10.2 Add `@media (prefers-reduced-motion: reduce)` override that makes `.animate-on-scroll` immediately visible with no transition
  - [ ] 10.3 Add JS IntersectionObserver that adds `.animate-on-scroll` to target elements and applies `.animated` when they enter the viewport, then unobserves them

- [ ] 11. Print Styles
  - [ ] 11.1 Add `@media print` block to style.css that hides navbar, scroll-to-top, theme-toggle, hero buttons, hero social links, and footer social links
  - [ ] 11.2 Add print rules for single-column layout, black-on-white colors, no box shadows, no background gradients
  - [ ] 11.3 Add print rule to show all `.skill-tag-hidden` elements and hide `.skill-more-btn`

- [ ] 12. Component Standardization
  - [ ] 12.1 Audit all card hover `translateY` values and standardize to `translateY(-3px)` for standard cards and `translateY(-4px)` for featured/primary cards, documented in a CSS comment
  - [ ] 12.2 Verify all card components use `--radius-md`, all tags use `--radius-sm`, and all section-level boxes use `--radius-lg` after the radius variable replacement in task 1.3

- [ ] 13. Full Width Layout
  - [ ] 13.1 Verify `.container` max-width is 1200px in style.css; update if it differs
  - [ ] 13.2 Add CSS grid rule for `.skills-grid`: 3 columns above 1024px, 2 columns at 768px–1023px, 1 column below 768px
  - [ ] 13.3 Add CSS grid rule for `.projects-grid`: 2 columns above 768px, 1 column below 768px
  - [ ] 13.4 Verify the Experience timeline renders as a vertical left-rail layout on all sizes; add `@media (max-width: 480px)` rule to hide the rail line and adjust marker positioning
  - [ ] 13.5 Add CSS for `.about-content` 2-column layout above 768px (text left, supplementary right), collapsing to 1 column below 768px
  - [ ] 13.6 Add CSS for `.contact-content` or `.contact-methods-grid` 2-column layout above 768px, collapsing to 1 column below 768px

- [ ] 14. Hero Two-Column Layout
  - [ ] 14.1 Restructure the `.hero-content` HTML in index.html to a two-column flex/grid container: `.hero-left` (name, title, tagline, CTAs, social links) and `.hero-right` (avatar + metric cards)
  - [ ] 14.2 Add the circular avatar placeholder HTML inside `.hero-right`: a `<div class="hero-avatar">` containing `<span>HEA</span>`, styled as a circle with the primary gradient and white initials text
  - [ ] 14.3 Add the 2×2 metric cards grid HTML inside `.hero-right`: a `<div class="hero-metrics">` containing 4 `<div class="hero-metric-card">` elements, each with the stat number and label from the existing hero stats bar
  - [ ] 14.4 Add CSS for `.hero-left` and `.hero-right` columns: flex layout, column widths (roughly 55%/45%), gap, vertical alignment
  - [ ] 14.5 Add CSS for `.hero-avatar`: circular shape (border-radius 50%), minimum 160px diameter on desktop, primary gradient background, centered white initials text
  - [ ] 14.6 Add CSS for `.hero-metrics` 2×2 grid and `.hero-metric-card` styling (semi-transparent background, border, padding, number/label typography)
  - [ ] 14.7 Add CSS to hide `.hero-stats-bar` when the two-column layout is active (above 768px) and show it when collapsed to single column (below 768px)
  - [ ] 14.8 Add `@media (max-width: 767px)` rule to collapse `.hero-content` to single column with `.hero-right` stacked below `.hero-left`

- [ ] 15. Mermaid Diagram Rendering
  - [ ] 15.1 Verify Mermaid.js CDN script is present in `<head>` with `startOnLoad: true` and `theme: 'neutral'`; add or correct if missing
  - [ ] 15.2 Audit all flowchart code blocks in the Architecture section of index.html; wrap any that are in `<pre>` or bare text in `<div class="mermaid">` containers
  - [ ] 15.3 Update the dark mode JS toggle handler (task 3.6) to call `mermaid.initialize({ theme: 'dark' })` and re-render diagrams when switching to dark mode, and `theme: 'neutral'` when switching to light mode

- [ ] 16. Content Fixes
  - [ ] 16.1 Search index.html for all occurrences of "+251 942 707 424" and remove the containing element (phone link or text node) from each location
  - [ ] 16.2 Update the static copyright year fallback in the footer `<span id="copyright-year">` from any non-2026 value to `2026`
  - [ ] 16.3 Add a `<span class="coming-soon-badge">Coming Soon</span>` element inside each of the 3 Insights article `<h3>` or adjacent to the title in index.html
  - [ ] 16.4 Add `.coming-soon-badge` CSS to style.css: small font size, muted background (`var(--bg-tertiary)`), subtle border (`var(--border-color)`), `border-radius: var(--radius-pill)`, inline-block, padding 2px 8px
  - [ ] 16.5 Locate and remove the `<div class="stats-bar">` (or equivalent element) that displays the 4 metrics inside the About section in index.html, leaving the metrics only in the Hero section
