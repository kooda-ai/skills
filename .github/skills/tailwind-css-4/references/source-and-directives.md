# Source Detection And Directives

Sources used: Tailwind CSS docs for detecting classes in source files and functions and directives.

## How Classes Are Detected
- Tailwind scans source files as plain text and does not parse files as code.
- It looks for tokens that could be classes based on characters Tailwind expects in class names.
- Tailwind then generates CSS for tokens that map to known utility classes and discards tokens that do not.

## Dynamic Class Names
- Tailwind cannot understand string concatenation or interpolation.
- Class names must exist in full in source files.
- For component props, map values to complete static class names instead of building strings dynamically.

```jsx
function Button({ color, children }) {
  const colorVariants = {
    blue: "bg-blue-600 hover:bg-blue-500 text-white",
    red: "bg-red-500 hover:bg-red-400 text-white",
    yellow: "bg-yellow-300 hover:bg-yellow-400 text-black",
  };

  return <button className={`${colorVariants[color]} ...`}>{children}</button>;
}
```

## Files Scanned By Default
Tailwind scans every file in the project except:
- Files in `.gitignore`.
- Files in `node_modules`.
- Binary files like images, videos, or zip files.
- CSS files.
- Common package manager lock files.

## Explicit Sources
Use `@source` to register source paths relative to the stylesheet.

```css
@import "tailwindcss";
@source "../node_modules/@acmecorp/ui-lib";
```

Use `source()` on the Tailwind import to set the base path for source detection.

```css
@import "tailwindcss" source("../src");
```

Use `@source not` to ignore paths relative to the stylesheet.

```css
@import "tailwindcss";
@source not "../src/components/legacy";
```

Use `source(none)` to disable automatic source detection and register all sources explicitly.

```css
@import "tailwindcss" source(none);
@source "../admin";
@source "../shared";
```

## Safelisting And Excluding Utilities
Use `@source inline()` to force generation of utilities that do not appear in content files.

```css
@import "tailwindcss";
@source inline("underline");
```

Use brace expansion to safelist variants and ranges.

```css
@import "tailwindcss";
@source inline("{hover:,focus:,}underline");
@source inline("{hover:,}bg-red-{50,{100..900..100},950}");
```

Use `@source not inline()` to prevent specific classes from being generated even if detected.

```css
@import "tailwindcss";
@source not inline("{hover:,focus:,}bg-red-{50,{100..900..100},950}");
```

## Directives
Tailwind exposes custom at-rules for CSS projects.

### `@import`
Use `@import` to inline import CSS files, including Tailwind itself.

```css
@import "tailwindcss";
```

### `@theme`
Use `@theme` to define custom design tokens such as fonts, colors, and breakpoints.

```css
@theme {
  --font-display: "Satoshi", "sans-serif";
  --breakpoint-3xl: 120rem;
  --color-avocado-100: oklch(0.99 0 0);
  --ease-fluid: cubic-bezier(0.3, 0, 0, 1);
}
```

### `@source`
Use `@source` for source files not picked up by automatic content detection.

```css
@source "../node_modules/@my-company/ui-lib";
```

### `@utility`
Use `@utility` to add custom utilities that work with variants like `hover`, `focus`, and `lg`.

```css
@utility tab-4 {
  tab-size: 4;
}
```

### `@variant`
Use `@variant` to apply a Tailwind variant inside custom CSS.

```css
.my-element {
  background: white;
  @variant dark {
    background: black;
  }
}
```

### `@custom-variant`
Use `@custom-variant` to add a custom variant.

```css
@custom-variant theme-midnight (&:where([data-theme="midnight"] *));
```

This enables utilities like `theme-midnight:bg-black` and `theme-midnight:text-white`.

### `@apply`
Use `@apply` to inline existing utility classes into custom CSS.

```css
.select2-dropdown {
  @apply rounded-b-lg shadow-md;
}
.select2-search {
  @apply rounded border border-gray-300;
}
.select2-results__group {
  @apply text-lg font-bold text-gray-900;
}
```

The docs describe this as useful for custom CSS such as third-party library overrides while still using Tailwind design tokens and syntax.

### `@reference`
Use `@reference` in Vue or Svelte component `<style>` blocks, CSS modules, or other separately bundled stylesheets when `@apply` or `@variant` needs access to theme variables, custom utilities, and custom variants from another file.

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

If only the default theme is used with no customizations such as `@theme`, `@custom-variant`, or `@plugin`, the docs show importing `tailwindcss` directly.

```vue
<template>
  <h1>Hello world!</h1>
</template>
<style>
  @reference "tailwindcss";
  h1 {
    @apply text-2xl font-bold text-red-500;
  }
</style>
```

### Subpath Imports
When using the CLI, Vite, or PostCSS, `@import`, `@reference`, `@plugin`, and `@config` support Node.js subpath imports.

```json
{
  "imports": {
    "#app.css": "./src/css/app.css"
  }
}
```

```vue
<template>
  <h1>Hello world!</h1>
</template>
<style>
  @reference "#app.css";
  h1 {
    @apply text-2xl font-bold text-red-500;
  }
</style>
```

## Build-Time Functions
Tailwind provides build-time functions for colors and spacing.

### `--alpha()`
Use `--alpha()` to adjust color opacity.

```css
.my-element {
  color: --alpha(var(--color-lime-300) / 50%);
}
```

Compiles to `color-mix(in oklab, var(--color-lime-300) 50%, transparent)`.

### `--spacing()`
Use `--spacing()` to generate a spacing value based on the theme.

```css
.my-element {
  margin: --spacing(4);
}
```

Compiles to `calc(var(--spacing) * 4)`.

The docs also show `--spacing()` in arbitrary values.

```html
<div class="py-[calc(--spacing(4)-1px)]"></div>
```

## Compatibility Directives And Function
The following exist for compatibility with Tailwind CSS v3.x.

### `@config`
Use `@config` to load a legacy JavaScript configuration file.

```css
@config "../../tailwind.config.js";
```

The `corePlugins`, `safelist`, and `separator` options from JavaScript config are not supported in v4.0. To safelist utilities in v4, use `@source inline()`.

### `@plugin`
Use `@plugin` to load a legacy JavaScript-based plugin.

```css
@plugin "@tailwindcss/typography";
```

The docs state `@plugin` accepts a package name or local path.

### `theme()`
Use `theme()` to access theme values with dot notation, but the function is deprecated and the docs recommend CSS theme variables instead.

```css
.my-element {
  margin: theme(spacing.12);
}
```

`@config`, `@plugin`, and `theme()` exist solely for v3.x compatibility. The docs state `@config` and `@plugin` can be used with CSS-driven features, and CSS-defined values are merged where possible and otherwise take precedence over configs, presets, and plugins.