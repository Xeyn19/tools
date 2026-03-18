---
name: responsive-page-design
description: Create or retrofit responsive pages that work on all device sizes, including text, images, layouts, and interactive elements. Use when building or reviewing HTML/CSS/JS (or React) to ensure mobile, tablet, and desktop responsiveness, fluid typography, and adaptive media.
---

# Responsive Page Design

## Quick Start
- Use fluid layouts (flex/grid) and avoid fixed widths unless constrained by a max-width.
- Set global media defaults so images and video do not overflow.
- Use `clamp()` for fluid typography and spacing.
- Test widths: 320, 360, 375, 414, 768, 1024, 1280, 1440.

## Baseline CSS
```css
*, *::before, *::after { box-sizing: border-box; }
img, video, canvas, svg { max-width: 100%; height: auto; }
body { margin: 0; }
```

## Workflow
1. Wrap content in a responsive container (`max-width` + `padding-inline` + center).
2. Build layout with flex/grid and `gap`, not manual margins.
3. Make typography and spacing fluid using `clamp()`.
4. Ensure media scales and preserves aspect ratio.
5. Add breakpoints only when the layout breaks, not by device names.
6. Test touch targets and scroll behavior.

## Layout And Typography Patterns
- Container: `max-width: 72rem; margin: 0 auto; padding-inline: clamp(1rem, 4vw, 2.5rem);`
- Typography: `font-size: clamp(1rem, 0.9rem + 0.5vw, 1.125rem);` and `line-height` >= 1.4.
- Cards: `display: grid; grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr)); gap: 1.5rem;`.
- Use `min()` and `max()` for widths: `width: min(100%, 48rem);`.
- Keep line length readable: `max-width: 65ch` for long text blocks.

## Media Handling
- Fixed aspect blocks: set `aspect-ratio` on the container.
- Cropped images: use `object-fit: cover;`.
- Background images: `background-size: cover; background-position: center;`.

## Breakpoint Guidance
- Use `@media (min-width: 640px)`, `768px`, `1024px`, `1280px` when needed.
- Prefer container and layout changes over font size jumps.
- Avoid width-based hacks that create horizontal scroll.

## Accessibility And UX
- Touch targets: minimum 44x44px.
- Avoid text smaller than 14px on mobile.
- Ensure readable contrast and prevent horizontal scroll.
- Respect user zoom; avoid `user-scalable=no`.
- Use `@media (hover: hover)` to limit hover-only affordances.

## Review Checklist
- No horizontal scroll at 320px.
- Images and media scale without overflow.
- Typography remains readable across breakpoints.
- Components stack logically on small screens.
- Spacing remains consistent with `clamp()` and `gap`.
- Inputs and buttons are touch-friendly.