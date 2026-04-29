# Core Web, Static Assets, And Builders

Use this file for `lucide`, `lucide-static`, or `@lucide/icons` questions.

## Core Web: `lucide`
- The documented HTML pattern is elements such as `<i data-lucide="menu"></i>`.
- The documented JavaScript pattern is importing `createIcons` and the needed icons, then calling `createIcons({ icons: { ... } })`.
- The docs show a CDN pattern with `https://unpkg.com/lucide@latest` and `lucide.createIcons()`.
- Documented `createIcons()` options include:
  - `attrs`
  - `nameAttr`
  - `root`
  - `inTemplates`
- `root` is shown for replacement inside a shadow root.
- `inTemplates: true` is shown for replacing icons inside `<template>` tags.

## Core Web Styling And Attributes
- The docs show setting icon color with the `color` attribute on the HTML element.
- The docs show setting size with `width` and `height` attributes on the HTML element.
- The docs show global styling by targeting `.lucide` in CSS.
- The docs also show applying default attributes globally through `createIcons({ attrs: ... })`.
- Multiple docs show `currentColor` inheritance for icons inside parent elements with a text color.

## Lucide Lab With Core Web
- The docs show importing custom icons from `@lucide/lab` and registering them through `createIcons({ icons: { ... } })`.
- The docs also show rendering a Lucide Lab icon in HTML with `data-lucide="avocado"` after registration.

## Static Assets: `lucide-static`
- The docs show importing SVG strings from `lucide-static` in both ESM and CommonJS.
- The docs show writing imported SVG strings directly into `innerHTML`.
- The docs show Node.js server-side rendering with imported SVG strings.
- The docs show linking individual SVG files with `<img>` tags.
- The docs show CSS `background-image` usage with SVG files.
- The docs show icon font usage by importing `lucide-static/font/lucide.css`.
- The docs show sprite usage and explicitly note that the sprite path is not optimized for production.

## Raw Icon Data And Builders: `@lucide/icons`
- The docs explicitly say imports from `@lucide/icons` are icon data, not rendered components.
- Importing icons individually is documented as tree-shakable.
- Documented builder helpers include:
  - `buildLucideSvg`
  - `buildLucideIconNode`
  - `buildLucideIconElement`
  - `buildLucideDataUri`
- Documented build parameters include:
  - `color`
  - `size`
  - `width`
  - `height`
  - `strokeWidth`
  - `absoluteStrokeWidth`
  - `className`
  - `attributes`
- The docs say generated SVGs include default Lucide attributes such as `xmlns`, `viewBox`, `fill="none"`, `stroke="currentColor"`, `stroke-width="2"`, `stroke-linecap="round"`, `stroke-linejoin="round"`, plus a class string of the form `lucide lucide-{iconName}`.

## Use This Boundary Carefully
- If the user needs rendered framework components, do not answer from `@lucide/icons`.
- If the user needs raw SVG output, data URIs, or DOM/SVG builders, stay with `@lucide/icons` instead of component-package guidance.
