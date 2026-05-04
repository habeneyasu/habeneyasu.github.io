# Requirements Document

## Introduction

This document defines requirements for a complete redesign of habeneyasu.github.io — a static portfolio site for Haben Eyasu Akelom, Senior Software & AI Engineer. The redesign targets CSS consolidation, improved section flow, dark mode, accessibility, and several UX improvements — all within the existing vanilla HTML/CSS/JS stack with no build tools or frameworks.

All text content (names, titles, descriptions, metrics, links) must remain unchanged. All existing sections must be preserved except Focus Areas (explicitly redundant with About expertise cards). All existing functionality must continue to work.

## Glossary

- **Site**: The static portfolio at habeneyasu.github.io (index.html + style.css)
- **CSS_System**: The custom property and rule set defined in style.css
- **Dark_Mode_Toggle**: The button added to the navbar that switches between light and dark color schemes
- **Theme**: The active color scheme — either light or dark
- **IntersectionObserver**: The browser API used to trigger entrance animations when sections scroll into view
- **Scroll_To_Top**: The floating button that appears after the user scrolls 400px and returns the page to the top
- **Skip_Link**: The visually-hidden anchor at the top of the page that allows keyboard users to jump past the navbar to main content
- **Focus_Visible**: The `:focus-visible` CSS pseudo-class used to show keyboard focus indicators without affecting mouse users
- **Print_Styles**: CSS rules inside `@media print` that optimize the page for printing
- **Section_Order**: The sequence of sections as rendered in the DOM and reflected in the navbar
- **Architecture_Card**: The card components in the Architecture section that display system diagrams
- **Hero_CTA**: The call-to-action buttons in the hero section

## Requirements

---

### Requirement 1: CSS Custom Property Consolidation

**User Story:** As a developer maintaining the site, I want all design tokens defined as CSS custom properties, so that I can make consistent changes in one place without hunting for hardcoded values.

#### Acceptance Criteria

1. THE CSS_System SHALL define `--radius-sm`, `--radius-md`, `--radius-lg`, and `--radius-xl` custom properties for all border-radius values used across the site.
2. THE CSS_System SHALL define `--transition-fast`, `--transition-base`, and `--transition-slow` custom properties for all transition durations used across the site.
3. THE CSS_System SHALL replace all hardcoded `border-radius` values (6px, 8px, 10px, 12px, 16px) with the appropriate radius custom property.
4. THE CSS_System SHALL replace all hardcoded transition durations (0.2s, 0.25s, 0.3s) with the appropriate transition custom property.
5. THE CSS_System SHALL remove all duplicate color variable declarations, retaining a single canonical definition for each color token in the `:root` block.
6. THE CSS_System SHALL remove all CSS rules that are not referenced by any element in index.html (dead code).

---

### Requirement 2: Section Reordering

**User Story:** As a visitor, I want the portfolio sections to follow a logical narrative flow, so that I can understand Haben's background progressively without disorientation.

#### Acceptance Criteria

1. THE Site SHALL render sections in this order: Hero → About → Experience → Skills → Projects (AI/ML + Software + Additional) → Architecture → GitHub → Insights → Contact → Footer.
2. THE Site SHALL move the Case Study content to appear as a subsection within the About section or the Projects section, not as a standalone top-level section before About.
3. THE Site SHALL remove the Focus Areas section from the rendered page.
4. THE Site SHALL update the navbar links to reflect the new section order and remove the Focus Areas link.
5. WHEN a user clicks any navbar link, THE Site SHALL scroll to the correct target section after reordering.

---

### Requirement 3: Dark Mode

**User Story:** As a visitor, I want to switch between light and dark color schemes, so that I can read the portfolio comfortably in low-light environments.

#### Acceptance Criteria

1. THE CSS_System SHALL define a complete set of dark-mode color overrides using a `[data-theme="dark"]` attribute selector on the `<html>` element.
2. THE Dark_Mode_Toggle SHALL be rendered as a button inside the navbar, visible on all screen sizes.
3. WHEN the user clicks the Dark_Mode_Toggle, THE Site SHALL toggle the `data-theme` attribute on the `<html>` element between `"light"` and `"dark"`.
4. WHEN the user's OS preference is dark (`prefers-color-scheme: dark`) and no manual preference has been saved, THE Site SHALL apply the dark Theme on initial load.
5. WHEN the user manually selects a Theme, THE Site SHALL persist that preference to `localStorage` and restore it on subsequent page loads.
6. WHILE the dark Theme is active, THE Site SHALL ensure all text meets WCAG AA contrast ratio (minimum 4.5:1 for normal text, 3:1 for large text) against dark backgrounds.
7. WHILE the dark Theme is active, THE Mermaid diagrams SHALL use the `dark` Mermaid theme.

---

### Requirement 4: Accessibility Improvements

**User Story:** As a keyboard or assistive-technology user, I want the site to be navigable without a mouse, so that I can access all content and functionality.

#### Acceptance Criteria

1. THE Site SHALL include a Skip_Link as the first focusable element in the DOM, linking to `#main-content`, that becomes visible on keyboard focus.
2. THE CSS_System SHALL define `:focus-visible` styles for all interactive elements (links, buttons, inputs) using a visible outline that meets WCAG AA contrast requirements.
3. THE CSS_System SHALL NOT suppress the default focus outline on `:focus` without providing an equivalent `:focus-visible` replacement.
4. THE Dark_Mode_Toggle SHALL have an `aria-label` attribute that reflects the current Theme (e.g., "Switch to dark mode" / "Switch to light mode").
5. THE Scroll_To_Top button SHALL have an `aria-label` of "Scroll to top".
6. IF an interactive element receives keyboard focus, THEN THE Site SHALL display a visible focus indicator on that element.

---

### Requirement 5: Hero Section Simplification

**User Story:** As a visitor landing on the page, I want a clear and focused hero section, so that I can immediately understand who Haben is and take one of two primary actions.

#### Acceptance Criteria

1. THE Hero_CTA area SHALL contain exactly two buttons: "Get In Touch" (linking to `#contact`) and "View Projects" (linking to `#projects-ai-ml`).
2. THE Site SHALL move the "Download Resume" button from the hero to the Contact section.
3. THE Site SHALL preserve the hero social links (Email, LinkedIn, GitHub) in their current position below the CTA buttons.
4. THE Site SHALL preserve all hero content that is not a CTA button: title, subtitle, value statement, description, and stats bar.

---

### Requirement 6: Architecture Cards Layout Fix

**User Story:** As a visitor viewing the Architecture section, I want the architecture cards to fill the available grid width, so that the section doesn't look cramped on wide screens.

#### Acceptance Criteria

1. THE CSS_System SHALL remove the `max-width: 600px` constraint from Architecture section card elements.
2. THE Architecture_Card elements SHALL expand to fill their grid column width on all viewport sizes.
3. WHILE the viewport is 768px or wider, THE Architecture_Card elements SHALL be displayed in a multi-column grid layout.

---

### Requirement 7: Section Title Rename

**User Story:** As a visitor reading the projects section, I want section titles to be clear and professional, so that I understand what each section contains.

#### Acceptance Criteria

1. THE Site SHALL display the software projects section title as "Software Engineering Projects" instead of "Featured Software Projects (Top 2)".
2. THE Site SHALL preserve all other section titles unchanged.

---

### Requirement 8: Inline Style Removal

**User Story:** As a developer maintaining the site, I want all styles defined in style.css rather than inline on elements, so that the codebase is consistent and maintainable.

#### Acceptance Criteria

1. THE Site SHALL move all inline `style` attributes from the GitHub contribution graph `<img>` element into named CSS classes in style.css.
2. THE Site SHALL have no remaining inline `style` attributes on any element except the critical CSS fallback `<style>` block in `<head>`.

---

### Requirement 9: Scroll-To-Top Button

**User Story:** As a visitor who has scrolled deep into the page, I want a scroll-to-top button, so that I can return to the top without manually scrolling.

#### Acceptance Criteria

1. THE Site SHALL render a Scroll_To_Top button that is hidden when the page scroll position is less than 400px from the top.
2. WHEN the page scroll position reaches or exceeds 400px, THE Scroll_To_Top button SHALL become visible with a smooth CSS transition.
3. WHEN the user clicks the Scroll_To_Top button, THE Site SHALL scroll the page to the top using smooth scrolling behavior.
4. THE Scroll_To_Top button SHALL be positioned fixed in the bottom-right corner of the viewport.
5. WHILE the dark Theme is active, THE Scroll_To_Top button SHALL use dark-mode-appropriate colors.

---

### Requirement 10: Section Entrance Animations

**User Story:** As a visitor scrolling through the portfolio, I want subtle entrance animations on sections, so that the page feels polished and guides my attention.

#### Acceptance Criteria

1. THE Site SHALL use an IntersectionObserver to detect when section elements enter the viewport.
2. WHEN a section element enters the viewport for the first time, THE Site SHALL apply a fade-in-up animation (opacity 0→1, translateY 20px→0) over 500ms.
3. THE Site SHALL apply entrance animations to section containers, project cards, timeline items, and skill category cards.
4. IF a user has `prefers-reduced-motion: reduce` set, THEN THE Site SHALL skip all entrance animations and display elements in their final visible state immediately.
5. THE Site SHALL only animate each element once — elements that have already entered the viewport SHALL NOT re-animate on scroll.

---

### Requirement 11: Print Styles

**User Story:** As a recruiter or visitor who wants to print the portfolio, I want a clean printed version, so that the output is readable and professional without navigation chrome.

#### Acceptance Criteria

1. THE CSS_System SHALL include a `@media print` block that hides the navbar, Scroll_To_Top button, Dark_Mode_Toggle, hero buttons, and footer social links.
2. WHILE printing, THE Site SHALL render all section content in a single-column layout.
3. WHILE printing, THE Site SHALL use black text on white background regardless of the active Theme.
4. WHILE printing, THE Site SHALL expand all collapsed skill tag groups to show all tags.
5. WHILE printing, THE Site SHALL remove all box shadows and background gradients from cards.

---

### Requirement 12: Component Standardization

**User Story:** As a developer maintaining the site, I want all interactive components to use consistent border-radius, transition timing, and hover effects, so that the design feels cohesive.

#### Acceptance Criteria

1. THE CSS_System SHALL apply `--radius-md` to all card components (project cards, skill categories, timeline content, education cards, contact method cards).
2. THE CSS_System SHALL apply `--transition-base` to all hover state transitions on interactive cards and buttons.
3. THE CSS_System SHALL apply consistent `translateY(-3px)` or `translateY(-4px)` lift on hover for all card components (no mixing of -2px, -3px, -4

---

### Requirement 13: Full Width Layout

**User Story:** As a visitor on any screen size, I want the portfolio to use the full available width with a consistent grid system, so that content is well-organized and readable at every breakpoint.

#### Acceptance Criteria

1. THE CSS_System SHALL set the global `.container` to a maximum width of 1200px, centered with auto horizontal margins.
2. THE Skills section SHALL render as a 3-column grid when the viewport is 1024px or wider, collapsing to 2 columns at 768px–1023px and 1 column below 768px.
3. THE Projects grid SHALL render as a 2-column card grid when the viewport is 768px or wider, collapsing to 1 column below 768px.
4. THE Experience section SHALL render as a vertical timeline with a left rail on all viewport sizes, with the rail hidden below 480px.
5. THE About section SHALL render as a 2-column layout (text left, supplementary content right) when the viewport is 768px or wider, collapsing to a single column below 768px.
6. THE Contact section SHALL render as a 2-column layout (contact methods left, resume/availability right) when the viewport is 768px or wider, collapsing to a single column below 768px.

---

### Requirement 14: Hero Two-Column Layout

**User Story:** As a visitor landing on the page, I want the hero section to use a two-column layout with a visual identity element, so that the page feels professional and immediately communicates who Haben is.

#### Acceptance Criteria

1. WHEN the viewport is 768px or wider, THE Hero section SHALL render as a two-column layout: left column containing the name, title, tagline, CTA buttons, and social links; right column containing an avatar and metric cards.
2. THE right column SHALL contain a circular avatar placeholder displaying the initials "HEA" styled with the primary gradient background.
3. THE right column SHALL contain 4 metric cards arranged in a 2×2 grid, each displaying one of the existing hero stats (8+ Years, 35+ Banks, 8M+ Txns/Month, 99.8% Uptime).
4. THE hero stats bar (the existing horizontal stats row) SHALL be hidden when the two-column layout is active, as the metrics are displayed in the right column cards instead.
5. WHEN the viewport is below 768px, THE Hero section SHALL collapse to a single column with the avatar and metric cards stacked below the text content.
6. THE avatar placeholder SHALL be at least 160px in diameter on desktop and 120px on mobile.

---

### Requirement 15: Mermaid Diagram Rendering

**User Story:** As a visitor viewing the Architecture section, I want the Mermaid flowchart diagrams to render as actual visual diagrams rather than raw code blocks, so that I can understand the system architectures at a glance.

#### Acceptance Criteria

1. THE Site SHALL load Mermaid.js from CDN in the `<head>` with `startOnLoad: true` and `theme: 'neutral'` as the default configuration.
2. ALL flowchart code blocks in the Architecture section SHALL be wrapped in `<div class="mermaid">` containers so Mermaid renders them as diagrams.
3. WHEN the dark Theme is active, THE Site SHALL re-initialize Mermaid with `theme: 'dark'` so diagrams match the active color scheme.
4. THE Mermaid CDN script SHALL be loaded before the closing `</head>` tag to ensure diagrams render on page load without a flash of raw code.
5. IF Mermaid fails to load (offline or CDN unavailable), THE Site SHALL display the raw flowchart text in a styled `<pre>` block as a fallback.

---

### Requirement 16: Content Fixes

**User Story:** As a visitor and site owner, I want the portfolio content to be accurate, clean, and free of outdated or sensitive information, so that the site presents a professional and current profile.

#### Acceptance Criteria

1. THE Site SHALL remove the phone number "+251 942 707 424" from all locations where it appears, including the contact section, hero social links, and any footer content.
2. THE Site SHALL display the copyright year as 2026 in the footer (both the static fallback value and the dynamically updated value).
3. ALL three Insights articles SHALL display a "Coming Soon" badge rendered as a small, muted, rounded pill element adjacent to the article title.
4. THE About section SHALL NOT display the 4 key metrics (8+ Years, 35+ Banks, 8M+ Txns/Month, 99.8% Uptime) — these metrics SHALL appear only in the Hero section.
5. THE "Coming Soon" badge SHALL use a muted background color and subtle border that does not distract from the article title.
