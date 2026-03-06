---
description: 'File structure, coding best practices, and color/styling rules for HTML, CSS, and JS to ensure accessible, professional, and maintainable designs.'
applyTo: '**/*.html, **/*.css, **/*.js'
---

# HTML, CSS & JS — Style, Color & Best Practices Guide

Follow these guidelines when creating or updating HTML, CSS, and JavaScript files for browser rendering.
Color names represent the full spectrum of their respective hue ranges (e.g., "blue" includes navy, sky blue, etc.).

## File Separation & Project Structure

Always follow the **separation of concerns** principle. HTML, CSS, and JavaScript **must** be kept in separate files.

### Rules

- **Never** write inline `<style>` or `<script>` blocks inside HTML files.
- **Never** use inline styles (`style="..."`) on HTML elements.
- **Never** use inline event handlers (`onclick="..."`, `onchange="..."`, etc.) on HTML elements.
- Structure files following accepted market conventions:
  - `index.html` — semantic markup and content only.
  - `styles.css` (or a `/css` folder) — all visual presentation and layout.
  - `script.js` (or a `/js` folder) — all behavior and interactivity.
- Link external stylesheets with `<link rel="stylesheet" href="styles.css">` in the `<head>`.
- Link external scripts with `<script src="script.js"></script>` at the end of the `<body>` (or use the `defer` attribute).

### Recommended Folder Structure

```
project/
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── script.js
└── assets/
    └── images/
```

### Industry Best Practices

- **Semantic HTML**: Use semantic tags (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<nav>`, etc.) instead of generic `<div>` elements.
- **Accessibility (a11y)**: Include `alt` attributes on images, `aria-label` on interactive elements, proper heading hierarchy (`h1`→`h6`), and ensure keyboard navigability.
- **CSS Variables**: Define a design-token system with CSS custom properties (`:root { --color-primary: … }`) for consistency and easy theming.
- **BEM or consistent naming**: Adopt a CSS naming convention (e.g., BEM — Block, Element, Modifier) to keep selectors predictable and maintainable.
- **Progressive Enhancement**: Build core functionality with HTML first, enhance with CSS, then layer JavaScript behavior on top.
- **Responsive Design**: Use relative units (`rem`, `em`, `%`, `vw/vh`), media queries, and mobile-first approach.
- **Performance**: Minimize render-blocking resources, prefer `defer` or `async` for scripts, and optimize asset sizes.

## Color Definitions

- **Hot Colors**: Oranges, reds, and yellows
- **Cool Colors**: Blues, greens, and purples
- **Neutral Colors**: Grays and grayscale variations
- **Binary Colors**: Black and white
- **60-30-10 Rule**
  - **Primary Color**: Use 60% of the time (*cool or light color*)
  - **Secondary Color**: Use 30% of the time (*cool or light color*)
  - **Accent**: Use 10% of the time (*complementary hot color*)

## Color Usage Guidelines

Balance the colors used by applying the **60-30-10 rule** to graphic design elements like backgrounds,
buttons, cards, etc...

### Background Colors

**Never Use:**

- Purple or magenta
- Red, orange, or yellow
- Pink
- Any hot color

**Recommended:**

- White or off-white
- Light cool colors (e.g., light blues, light greens)
- Subtle neutral tones
- Light gradients with minimal color shift

### Text Colors

**Never Use:**

- Yellow (poor contrast and readability)
- Pink
- Pure white or light text on light backgrounds
- Pure black or dark text on dark backgrounds

**Recommended:**

- Dark neutral colors (e.g., #1f2328, #24292f)
- Near-black variations (#000000 to #333333)
  - Ensure background is a light color
- Dark grays (#4d4d4d, #6c757d)
- High-contrast combinations for accessibility
- Near-white variations (#ffffff to #f0f2f3)
  - Ensure background is a dark color

### Colors to Avoid

Unless explicitly required by design specifications or user request, avoid:

- Bright purples and magentas
- Bright pinks and neon colors
- Highly saturated hot colors
- Colors with low contrast ratios (fails WCAG accessibility standards)

### Colors to Use Sparingly

**Hot Colors** (red, orange, yellow):

- Reserve for critical alerts, warnings, or error messages
- Use only when conveying urgency or importance
- Limit to small accent areas rather than large sections
- Consider alternatives like icons or bold text before using hot colors

## Gradients

Apply gradients with subtle color transitions to maintain professional aesthetics.

### Best Practices

- Keep color shifts minimal (e.g., #E6F2FF to #F5F7FA)
- Use gradients within the same color family
- Avoid combining hot and cool colors in a single gradient
- Prefer linear gradients over radial for backgrounds

### Appropriate Use Cases

- Background containers and sections
- Button hover states and interactive elements
- Drop shadows and depth effects
- Header and navigation bars
- Card components and panels

## Additional Resources

- [Color Tool](https://civicactions.github.io/uswds-color-tool/)
- [Government or Professional Color Standards](https://designsystem.digital.gov/design-tokens/color/overview/)
- [UI Color Palette Best Practices](https://www.interaction-design.org/literature/article/ui-color-palette)
- [Color Combination Resource](https://www.figma.com/resource-library/color-combinations/)
- [HTML Best Practices](https://www.w3schools.com/html/html5_syntax.asp)
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [MDN — Separation of Concerns](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Webpage_structure)