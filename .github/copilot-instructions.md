# Copilot instructions (Thinking with Comics website)

## Repo snapshot
- Static one-page site (no build step): `index.html` + `css/style.css` + `js/main.js`.
- External deps are CDN-loaded in `index.html` (`Chart.js`, `chartjs-plugin-annotation`, Google Fonts, Font Awesome).
- Images live under `images/` (notably `images/benchmark.png`, `images/appendix/`, `images/examples/<task>/`).

## Local preview (avoid file://)
- `python -m http.server 8080`
- or `npx http-server -p 8080`

## HTML ↔ JS “wiring” conventions (see `js/main.js`)
- **Mobile nav**: `.nav-toggle` toggles `.nav-menu.open` + `.nav-overlay.open` and updates `aria-expanded`.
- **Smooth scroll**: `.nav-menu a[href^="#"]` scrolls to target with offset `navbar.height + 20`.
- **Scroll reveal**: `IntersectionObserver` watches elements with class `.section`, adds `.visible` when in view.
- **Tabs (two systems, both toggle `.hidden`)**:
  - TL;DR: `.tldr-tab-btn[data-tab="tldr-math"]` → `#tldr-math.tldr-examples-grid`.
  - Gallery: `.tab-btn[data-tab="math"]` → `#gallery-math.gallery-grid` (note the `gallery-` prefix).

## Images & lightbox modal
- Shared modal markup is in `index.html` (`.image-modal`); JS auto-binds clicks for `.comic-frame-wrapper img`.
- For one-off clickable images, inline `onclick="openImageModal(this.src)"` works (global `openImageModal`).
- Keep paths relative and under `images/` so GitHub Pages resolves them.

## Academic charts
- Canvases live in `index.html` (e.g. `#scalingChart`, `#distributionChart`).
- All chart construction is inline at the bottom of `index.html` in the “Academic Charts Initialization” script.
  - To add a chart: add `<canvas id="...">` + a matching `new Chart(...)` block there.

## Styling conventions
- Reuse CSS variables in `:root` (colors, fonts, spacing) and existing components (`.btn*`, `.container`, `.hidden`).
- Avoid adding frameworks/bundlers unless explicitly requested; keep changes lightweight and CDN-friendly.
