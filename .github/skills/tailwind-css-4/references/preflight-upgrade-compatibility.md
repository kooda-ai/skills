# Preflight, Upgrade, And Compatibility

Sources used: Tailwind CSS docs for Preflight, upgrade guide, and compatibility.

## Preflight Overview
- Preflight is built on top of `modern-normalize`.
- It is a set of base styles for Tailwind projects, designed to smooth cross-browser inconsistencies and make it easier to work within design-system constraints.
- When importing `tailwindcss`, Preflight is automatically injected into the `base` layer.

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/preflight.css" layer(base);
@import "tailwindcss/utilities.css" layer(utilities);
```

## Documented Preflight Behaviors
- Margins and padding are removed from all elements, including headings, blockquotes, and paragraphs.
- All elements use `box-sizing: border-box` and `border: 0 solid`, so adding `border` adds a solid `1px` border using `currentColor`.
- Headings are unstyled by default and inherit font size and weight.
- Ordered and unordered lists are unstyled by default with `list-style: none`.
- The docs note that unstyled lists are not announced as lists by VoiceOver, and show adding `role="list"` when content is truly a list.
- Images and replaced elements such as `svg`, `video`, `canvas`, `audio`, `iframe`, `embed`, and `object` are `display: block` and `vertical-align: middle` by default.
- Images and videos use `max-width: 100%` and `height: auto` by default.
- Elements with a `hidden` attribute stay hidden unless using `hidden="until-found"`.

## Extending Preflight
Add base styles on top of Preflight with `@layer base`.

```css
@layer base {
  h1 {
    font-size: var(--text-2xl);
  }
  h2 {
    font-size: var(--text-xl);
  }
  h3 {
    font-size: var(--text-lg);
  }
  a {
    color: var(--color-blue-600);
    text-decoration-line: underline;
  }
}
```

## Disabling Preflight
Disable Preflight by importing only the Tailwind parts needed and omitting `preflight.css`.

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/utilities.css" layer(utilities);
```

When importing Tailwind files individually:
- `source(...)` affects generated utilities and should go on the `utilities.css` import.
- `important` affects utilities and should go on the `utilities.css` import.
- `theme(static)` and `theme(inline)` affect generated theme variables and should go on the `theme.css` import.
- `prefix(tw)` affects utilities and variables and should go on both `theme.css` and `utilities.css` imports.

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/utilities.css" layer(utilities) source(none);
```

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/utilities.css" layer(utilities) important;
```

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme) theme(static);
@import "tailwindcss/utilities.css" layer(utilities);
```

```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme) prefix(tw);
@import "tailwindcss/utilities.css" layer(utilities) prefix(tw);
```

## Upgrade Tool
Use the upgrade tool to migrate from v3 to v4.

```bash
npx @tailwindcss/upgrade
```

The docs state the upgrade tool automates most migration work, including updating dependencies, migrating configuration to CSS, and handling template changes. It requires Node.js 20 or higher. The docs recommend running it in a new branch, reviewing the diff, testing in the browser, and reading the breaking changes.

## Manual Upgrade Setup Changes
### PostCSS
In v4, the PostCSS plugin lives in `@tailwindcss/postcss`. Imports and vendor prefixing are handled automatically, so the docs say `postcss-import` and `autoprefixer` can be removed if present.

```js
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};
```

### Vite
For Vite, the docs recommend migrating from the PostCSS plugin to the dedicated Vite plugin.

```ts
import { defineConfig } from "vite";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
});
```

### Tailwind CLI
In v4, Tailwind CLI lives in `@tailwindcss/cli`.

```bash
npx @tailwindcss/cli -i input.css -o output.css
```

## Browser Requirements
Tailwind CSS v4.0 is designed for Safari 16.4+, Chrome 111+, and Firefox 128+. The docs state it depends on modern CSS features like `@property` and `color-mix()` and will not work in older browsers. Projects that need older browsers should stay on v3.4 according to the docs.

The compatibility page lists core browser support as:
- Chrome 111, released March 2023.
- Safari 16.4, released March 2023.
- Firefox 128, released July 2024.

The docs also state Tailwind includes utilities for modern platform features such as `field-sizing: content`, `@starting-style`, and `text-wrap: balance`; using those features depends on the target browsers.

## Removed `@tailwind` Directives
Use regular CSS `@import` in v4.

```css
@import "tailwindcss";
```

The old v3 directives were:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Removed Deprecated Utilities
The upgrade guide lists these removed utilities and alternatives:

| Removed | Use instead |
| --- | --- |
| `bg-opacity-*` | opacity modifiers like `bg-black/50` |
| `text-opacity-*` | opacity modifiers like `text-black/50` |
| `border-opacity-*` | opacity modifiers like `border-black/50` |
| `divide-opacity-*` | opacity modifiers like `divide-black/50` |
| `ring-opacity-*` | opacity modifiers like `ring-black/50` |
| `placeholder-opacity-*` | opacity modifiers like `placeholder-black/50` |
| `flex-shrink-*` | `shrink-*` |
| `flex-grow-*` | `grow-*` |
| `overflow-ellipsis` | `text-ellipsis` |
| `decoration-slice` | `box-decoration-slice` |
| `decoration-clone` | `box-decoration-clone` |

## Renamed Utilities
The upgrade guide lists these renamed utilities:

| v3 | v4 |
| --- | --- |
| `shadow-sm` | `shadow-xs` |
| `shadow` | `shadow-sm` |
| `drop-shadow-sm` | `drop-shadow-xs` |
| `drop-shadow` | `drop-shadow-sm` |
| `blur-sm` | `blur-xs` |
| `blur` | `blur-sm` |
| `backdrop-blur-sm` | `backdrop-blur-xs` |
| `backdrop-blur` | `backdrop-blur-sm` |
| `rounded-sm` | `rounded-xs` |
| `rounded` | `rounded-sm` |
| `outline-none` | `outline-hidden` |
| `ring` | `ring-3` |

Additional upgrade notes:
- `outline` now sets `outline-width: 1px` by default.
- `outline-<number>` utilities default `outline-style` to `solid`.
- `outline-none` now sets `outline-style: none`; use `outline-hidden` for the old accessible invisible outline behavior.
- The `ring` utility changed from 3px to 1px.

## Selector And Default Changes
- `space-x-*` and `space-y-*` selectors changed from sibling-based margins to `:not(:last-child)` rules. The docs recommend flex or grid with `gap` if this causes issues.
- `divide-x-*` and `divide-y-*` selectors changed similarly to use `:not(:last-child)`.
- Gradient values are preserved across variants in v4; use `via-none` when a three-stop gradient should become two-stop in a specific state.
- The v3 `container` utility configuration options like `center` and `padding` no longer exist; customize `container` with `@utility`.

```css
@utility container {
  margin-inline: auto;
  padding-inline: 2rem;
}
```

- `border-*` and `divide-*` default color changed from configured `gray-200` to `currentColor`.
- `ring` default width changed from 3px to 1px and default color changed from `blue-500` to `currentColor`.
- Compatibility variables `--default-ring-width` and `--default-ring-color` can preserve v3 ring behavior, but the docs say these variables are supported only for compatibility and are not idiomatic Tailwind CSS v4.0 usage.

## Preflight Changes In v4
- Placeholder text now uses current text color at 50% opacity instead of configured `gray-400`.
- Buttons use `cursor: default` instead of `cursor: pointer` to match browser defaults.
- Preflight resets margins on `<dialog>` elements.
- Display classes like `block` or `flex` no longer take priority over the `hidden` attribute. Remove the `hidden` attribute to make the element visible. This does not apply to `hidden="until-found"`.

## Prefixes And Important During Upgrade
Prefixes now look like variants and are always at the beginning of the class name.

```html
<div class="tw:flex tw:bg-red-500 tw:hover:bg-red-600"></div>
```

When using `prefix(tw)`, configure theme variables without the prefix; generated CSS variables include the prefix.

The important modifier should be placed at the end of the class name in v4.

```html
<div class="flex! bg-red-500! hover:bg-red-600/50!"></div>
```

The old leading `!` syntax is still supported for compatibility but is deprecated.

## Custom Utilities And Variant Order
In v4, use `@utility` instead of defining true utilities in `@layer utilities` or `@layer components`.

```css
@utility tab-4 {
  tab-size: 4;
}
```

The upgrade guide states custom utilities are sorted based on the amount of properties they define, so component utilities such as `.btn` can be overwritten by other Tailwind utilities.

Stacked variants now apply left to right in v4. Reverse order-sensitive stacked variants from v3 when needed.

```html
<ul class="py-4 *:first:pt-0 *:last:pb-0"></ul>
```

## Arbitrary Value Upgrade Changes
Use parentheses for CSS variable shorthand in arbitrary values.

```html
<div class="bg-(--brand-color)"></div>
```

For `grid-cols-*`, `grid-rows-*`, and `object-*` arbitrary values, use underscores to represent spaces.

```html
<div class="grid-cols-[max-content_auto]"></div>
```

## Hover, Transitions, And Transforms
- In v4, the `hover` variant only applies when the primary input device supports hover.
- The docs show overriding the hover variant with `@custom-variant hover (&:hover);` if old behavior is needed.
- The docs recommend treating hover as an enhancement and not depending on hover for touch-device functionality.
- `transition` and `transition-colors` now include `outline-color`.
- `rotate-*`, `scale-*`, and `translate-*` are based on individual CSS properties.
- Reset transforms with individual reset utilities such as `scale-none`, not `transform-none`.
- If customized transition property lists include `transform`, include individual properties such as `scale` instead.

## JavaScript Config And Theme Values
- The `corePlugins` option is no longer supported in v4.
- JavaScript config files are still supported for backward compatibility but are no longer detected automatically.
- Use `@config` to load a JavaScript config file.
- `corePlugins`, `safelist`, and `separator` options from JavaScript config are not supported in v4.0.
- Use `@source inline()` to safelist utilities in v4.
- The `resolveConfig` function was removed in v4.
- The docs recommend using generated CSS variables directly in JavaScript or `getComputedStyle` for resolved values.

```css
@config "../../tailwind.config.js";
```

```css
.my-class {
  background-color: var(--color-red-500);
}
```

```css
@media (width >= theme(--breakpoint-xl)) {
  /* ... */
}
```

## `@apply` In Scoped Or Separate CSS
In v4, stylesheets bundled separately from the main CSS file, such as CSS modules and `<style>` blocks in Vue, Svelte, or Astro, do not have access to theme variables, custom utilities, or custom variants defined in other files.

Use `@reference` to import definitions without duplicating CSS.

```vue
<template>
  <h1>Hello world!</h1>
</template>
<style>
  @reference "../../app.css";
  h1 {
    @apply text-2xl font-bold text-red-500;
  }
</style>
```

The docs also show using CSS variables directly instead of `@apply`, which avoids Tailwind processing those styles.

```vue
<template>
  <h1>Hello world!</h1>
</template>
<style>
  h1 {
    color: var(--text-red-500);
  }
</style>
```

## Sass, Less, And Stylus
Tailwind CSS v4.0 is not designed to be used with CSS preprocessors like Sass, Less, or Stylus. The docs say to think of Tailwind CSS itself as the preprocessor, and state it is not possible to use Sass, Less, or Stylus for stylesheets or `<style>` blocks in Vue, Svelte, Astro, etc.

Compatibility details from the docs:
- Tailwind automatically bundles CSS files included with `@import` without another preprocessing tool.
- Tailwind relies heavily on native CSS variables.
- Tailwind uses Lightning CSS to process nested CSS.
- Tailwind generates classes like `col-span-1` and `col-span-2` on demand when used, instead of requiring loops.
- The docs point to predefined color palettes and modern `color-mix()` for color adjustment, and native math functions like `min()`, `max()`, and `round()`.

## CSS Modules
- Tailwind can co-exist with CSS modules when introducing Tailwind into a project that already uses them.
- The docs do not recommend using CSS modules and Tailwind together when avoidable.
- CSS modules are processed separately by build tools, so Tailwind must run separately for each module, which the docs describe as slower.
- CSS modules have no `@theme` unless one is imported.
- Import global styles with `@reference` when features like `@apply` need theme context.
- Use CSS variables instead of `@apply` to let Tailwind skip processing those files and improve build performance.

```css
@reference "../app.css";

button {
  @apply bg-blue-500;
}
```

```css
button {
  background: var(--color-blue-500);
}
```

## Vue, Svelte, And Astro
- Vue, Svelte, and Astro support `<style>` blocks that behave much like CSS modules and are processed separately.
- The docs recommend avoiding component `<style>` blocks and styling directly with utility classes in markup when using Tailwind with these tools.
- If `<style>` blocks are used, import global styles with `@reference` for `@apply`.
- CSS variables can be used directly instead of features like `@apply`.

```vue
<template>
  <button><slot /></button>
</template>
<style scoped>
  @reference "../app.css";
  button {
    @apply bg-blue-500;
  }
</style>
```

```vue
<template>
  <button><slot /></button>
</template>
<style scoped>
  button {
    background-color: var(--color-blue-500);
  }
</style>
```