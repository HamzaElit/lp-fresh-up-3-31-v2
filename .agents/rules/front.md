---
description: Front-end coding standards and conventions for the Elithair landing page project
---

# Elithair Landing Page - Coding Rules

These rules guide the coding style for the Google Antigravity AI when working on the Elithair Landing Page project.

## 1. SCSS Architecture & BEM Methodology
- **BEM Naming Convention**: Always use strict BEM (Block Element Modifier) structural conventions (e.g., `.lp-hero`, `.lp-hero__bg`, `.lp-prices-tables__row--header`).
- **SCSS Nesting**: Utilize the `&` selector carefully within SCSS to define elements (`&__element`) and modifiers (`&--modifier`). Prevent deep DOM-based nesting (e.g., avoid `.lp-header .lp-header__main ul li a`), stick to flat BEM selectors.
- **CSS Variables**: Use native CSS custom properties for colors, typography, and spacing (e.g., `color: var(--White);`, `font-family: var(--font-titles);`, `background-color: var(--Deep-Blue);`).
- **Units**: Use `rem` exclusively for dimensions, padding, margins, and typography instead of `px`.
- **Modularity**: Place distinct section components in separate files inside `scss/modules/` (e.g., `_lp-hero.scss`, `_lp-prices-tables.scss`) and import them into `_modules.scss`.

## 2. Responsiveness & Media Queries
- **Mobile-First Approach**: Always author base CSS for mobile views first. Override styles progressively for larger screens.
- **Media Query Mixins**: ALWAYS utilize the predefined breakpoint mixins from `_mixins-master.scss` instead of writing raw media queries.
  - `@include xs-up { ... }` (min-width: 391px)
  - `@include sm-up { ... }` (min-width: 430px)
  - `@include md-up { ... }` (min-width: 768px)
  - `@include lg-up { ... }` (min-width: 1024px)
  - `@include xl-up { ... }` (min-width: 1288px)
  - `@include xxl-up { ... }` (min-width: 1700px)
- **Utility Classes**: Create or utilize responsive utility classes (e.g., `.mobile-only`, `.sm-only`) by hiding elements at larger breakpoints via mixins.

## 3. HTML Structure & Assets
- **Responsive Images**: Make use of the `<picture>` HTML element to serve context-appropriate images based on breakpoints (e.g., using `<source srcset="..." media="(min-width: 768px)">` and `<img src="..." />` for fallback).
- **Semantics**: Use appropriate HTML5 semantic tags (`<header>`, `<main>`, `<section>`, `<nav>`).
- **Icons & SVGs**: SVGs are typically used inline or loaded directly into CSS using optimized `data:image/svg+xml` backgrounds (e.g., in `_helpers.scss` custom lists).
- **Carousels/Sliders**: Implement carousels using **Embla Carousel**. The required structure is:
  ```html
  <div class="embla" data-slides-mobile="1" data-slides-desk="3">
    <div class="embla__viewport">
      <div class="embla__container">
        <div class="embla__slide">...</div>
      </div>
    </div>
  </div>
  ```
  Pass settings directly onto the root element through `data-*` attributes (`data-embla-loop`, `data-vertical`, etc.).

## 4. JavaScript Logic & Interactions
- **Vanilla JS**: Always write modern, modular Vanilla JS (ES6+). Do not use jQuery.
- **DOM Ready**: Place execution blocks inside `document.addEventListener("DOMContentLoaded", () => { ... })` or `window.addEventListener("load", ...)`.
- **Carousel Data API**: `custom.js` handles all Embla initialization globally by iterating over `.embla`. Ensure all new sliders rely on this global logic rather than initializing them separately, controlling behavior using corresponding `data-*` attributes.
- **Classes for State**: Control JavaScript visual state changes by toggling classes like `.is-active`, `.is-open`, `.active`, or `.is-disabled`. Ensure CSS handles the visual transition.
