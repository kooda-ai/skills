# Theme And Custom Styles

Sources used: Tailwind CSS docs for theme variables, adding custom styles, and functions and directives.

## Theme Variables
- Theme variables are special CSS variables defined with `@theme`.
- Theme variables influence which utility classes exist in the project.
- Tailwind also generates regular CSS variables for theme variables so design tokens can be referenced in arbitrary values or inline styles.
- Theme variables are required to be defined top-level and not nested under selectors or media queries.
- Use `@theme` when a design token should map directly to a utility class.
- Use `:root` for regular CSS variables that should not create corresponding utility classes.

```css
@import "tailwindcss";

@theme {
  --color-mint-500: oklch(0.72 0.11 178);
}
```

```html
<div class="bg-mint-500"></div>
<div style="background-color: var(--color-mint-500)"></div>
```

## Relationship To Utilities And Variants
- Some utilities like `flex` and `object-cover` are static.
- Many utilities are driven by theme variables.
- Theme variables in the `--font-*` namespace determine font-family utilities.
- Theme variables in the `--breakpoint-*` namespace determine responsive breakpoint variants.

```css
@import "tailwindcss";

@theme {
  --font-poppins: Poppins, sans-serif;
  --breakpoint-3xl: 120rem;
}
```

```html
<h1 class="font-poppins">This headline will use Poppins.</h1>
<div class="3xl:grid-cols-6 grid grid-cols-2 md:grid-cols-4"></div>
```

## Theme Variable Namespaces
The docs list these namespaces and their corresponding APIs:

| Namespace | API |
| --- | --- |
| `--color-*` | Color utilities like `bg-red-500`, `text-sky-300`, and many more |
| `--font-*` | Font family utilities like `font-sans` |
| `--text-*` | Font size utilities like `text-xl` |
| `--font-weight-*` | Font weight utilities like `font-bold` |
| `--tracking-*` | Letter spacing utilities like `tracking-wide` |
| `--leading-*` | Line height utilities like `leading-tight` |
| `--breakpoint-*` | Responsive breakpoint variants like `sm:*` |
| `--container-*` | Container query variants like `@sm:*` and size utilities like `max-w-md` |
| `--spacing-*` | Spacing and sizing utilities like `px-4`, `max-h-16`, and many more |
| `--radius-*` | Border radius utilities like `rounded-sm` |
| `--shadow-*` | Box shadow utilities like `shadow-md` |
| `--inset-shadow-*` | Inset box shadow utilities like `inset-shadow-xs` |
| `--drop-shadow-*` | Drop shadow filter utilities like `drop-shadow-md` |
| `--blur-*` | Blur filter utilities like `blur-md` |
| `--perspective-*` | Perspective utilities like `perspective-near` |
| `--aspect-*` | Aspect ratio utilities like `aspect-video` |
| `--ease-*` | Transition timing function utilities like `ease-out` |
| `--animate-*` | Animation utilities like `animate-spin` |

## Default Theme Import
Importing `tailwindcss` includes default theme variables.

```css
@layer theme, base, components, utilities;
@import "./theme.css" layer(theme);
@import "./preflight.css" layer(base);
@import "./utilities.css" layer(utilities);
```

The docs state `theme.css` includes the default color palette, type scale, shadows, fonts, and more. Utilities like `bg-red-200`, `font-serif`, and `shadow-sm` exist because they are driven by default theme variables.

## Extending, Overriding, And Replacing Theme Values
Use `@theme` to add new theme variables.

```css
@import "tailwindcss";

@theme {
  --font-script: Great Vibes, cursive;
}
```

Override a default theme variable by redefining it.

```css
@import "tailwindcss";

@theme {
  --breakpoint-sm: 30rem;
}
```

Set a namespace to `initial` to remove default utilities in that namespace.

```css
@import "tailwindcss";

@theme {
  --color-*: initial;
  --color-white: #fff;
  --color-purple: #3f3cbb;
  --color-midnight: #121063;
  --color-tahiti: #3ab7bf;
  --color-bermuda: #78dcca;
}
```

Set the global namespace to `initial` to disable the default theme and use only custom values.

```css
@import "tailwindcss";

@theme {
  --*: initial;
  --spacing: 4px;
  --font-body: Inter, sans-serif;
  --color-lagoon: oklch(0.72 0.11 221.19);
  --color-coral: oklch(0.74 0.17 40.24);
  --color-driftwood: oklch(0.79 0.06 74.59);
  --color-tide: oklch(0.49 0.08 205.88);
  --color-dusk: oklch(0.82 0.15 72.09);
}
```

## Theme Options
Define `@keyframes` rules for `--animate-*` inside `@theme` to include them in generated CSS.

```css
@import "tailwindcss";

@theme {
  --animate-fade-in-scale: fade-in-scale 0.3s ease-out;

  @keyframes fade-in-scale {
    0% {
      opacity: 0;
      transform: scale(0.95);
    }
    100% {
      opacity: 1;
      transform: scale(1);
    }
  }
}
```

Define custom `@keyframes` outside `@theme` if they should always be included even without an `--animate-*` theme variable.

Use `inline` when defining theme variables that reference other variables and the utility should use the theme variable value instead of referencing the variable.

```css
@import "tailwindcss";

@theme inline {
  --font-sans: var(--font-inter);
}
```

Use `static` to always generate all CSS variables.

```css
@import "tailwindcss";

@theme static {
  --color-primary: var(--color-red-500);
  --color-secondary: var(--color-blue-500);
}
```

## Sharing Theme Variables
Theme variables are CSS, so they can be shared in a CSS file and imported.

```css
/* ./packages/brand/theme.css */
@theme {
  --*: initial;
  --spacing: 4px;
  --font-body: Inter, sans-serif;
  --color-lagoon: oklch(0.72 0.11 221.19);
}
```

```css
/* ./packages/admin/app.css */
@import "tailwindcss";
@import "../brand/theme.css";
```

The docs state shared theme variables can live in their own package in monorepos or be published to NPM and imported like other third-party CSS files.

## Using Theme Variables
- Use `var(--*)` values in custom CSS.
- Use theme variables in arbitrary values, especially with `calc()`.
- Reference CSS variables directly in JavaScript when possible.
- Use `getComputedStyle(document.documentElement).getPropertyValue("--shadow-xl")` when a resolved variable value is needed in JavaScript.

```css
@import "tailwindcss";

@layer components {
  .typography {
    p {
      font-size: var(--text-base);
      color: var(--color-gray-700);
    }
  }
}
```

```html
<div class="absolute inset-px rounded-[calc(var(--radius-xl)-1px)]"></div>
```

```js
let styles = getComputedStyle(document.documentElement);
let shadow = styles.getPropertyValue("--shadow-xl");
```

## Arbitrary Values And Properties
Use square bracket notation for one-off values outside the theme.

```html
<div class="top-[117px] lg:top-[344px]"></div>
<div class="bg-[#bada55] text-[22px] before:content-['Festivus']"></div>
```

Use custom property shorthand when referencing CSS variables as arbitrary values.

```html
<div class="fill-(--my-brand-color)"></div>
```

This is shorthand for `fill-[var(--my-brand-color)]`.

Use arbitrary properties for CSS properties not included out of the box.

```html
<div class="[mask-type:luminance] hover:[mask-type:alpha]"></div>
<div class="[--scroll-offset:56px] lg:[--scroll-offset:44px]"></div>
```

When an arbitrary value needs a space, use `_`; Tailwind converts it to a space at build time.

```html
<div class="grid grid-cols-[1fr_500px_2fr]"></div>
```

Tailwind preserves underscores where spaces are invalid, such as URLs. Escape an ambiguous underscore with a backslash. In JSX, use `String.raw()` if the backslash would otherwise be stripped.

Use a CSS data type hint when an arbitrary value is ambiguous.

```html
<div class="text-(length:--my-var)"></div>
<div class="text-(color:--my-var)"></div>
```

## Custom CSS Layers
Use `@layer base` for default base styles.

```css
@layer base {
  h1 {
    font-size: var(--text-2xl);
  }
  h2 {
    font-size: var(--text-xl);
  }
}
```

Use the `components` layer for more complicated classes that should still be overridable by utility classes.

```css
@layer components {
  .card {
    background-color: var(--color-white);
    border-radius: var(--radius-lg);
    padding: --spacing(6);
    box-shadow: var(--shadow-xl);
  }
}
```

```html
<div class="card rounded-none"></div>
```

The docs also describe the `components` layer as a place for custom styles for third-party components.

## Custom Utilities
Use `@utility` to add custom utilities. Custom utilities work with variants and are inserted into the `utilities` layer.

```css
@utility content-auto {
  content-visibility: auto;
}
```

```html
<div class="content-auto hover:content-auto"></div>
```

Use nesting for complex utilities.

```css
@utility scrollbar-hidden {
  &::-webkit-scrollbar {
    display: none;
  }
}
```

## Functional Utilities
Use `@utility name-*` with `--value()` for functional utilities.

```css
@theme {
  --tab-size-2: 2;
  --tab-size-4: 4;
  --tab-size-github: 8;
}

@utility tab-* {
  tab-size: --value(--tab-size-*);
}
```

`--value()` documented forms:
- Theme values: `--value(--theme-key-*)`.
- Bare values: `--value(integer)`, with `number`, `integer`, `ratio`, and `percentage` documented.
- Literal values: `--value("inherit", "initial", "unset")`.
- Arbitrary values: `--value([integer])`.

Available arbitrary value data types documented for `--value()` are `absolute-size`, `angle`, `bg-size`, `color`, `family-name`, `generic-name`, `image`, `integer`, `length`, `line-width`, `number`, `percentage`, `position`, `ratio`, `relative-size`, `url`, `vector`, and `*`.

Multiple `--value()` declarations can be used; declarations that fail to resolve are omitted.

```css
@theme {
  --tab-size-github: 8;
}

@utility tab-* {
  tab-size: --value([integer]);
  tab-size: --value(integer);
  tab-size: --value(--tab-size-*);
}
```

Use separate utilities for negative values.

```css
@utility inset-* {
  inset: --spacing(--value(integer));
  inset: --value([percentage], [length]);
}

@utility -inset-* {
  inset: --spacing(--value(integer) * -1);
  inset: calc(--value([percentage], [length]) * -1);
}
```

Use `--modifier()` for modifiers; it works like `--value()` but operates on a modifier if present. Declarations depending on a missing modifier are omitted.

```css
@utility text-* {
  font-size: --value(--text-*, [length]);
  line-height: --modifier(--leading-*, [length], [*]);
}
```

Use the CSS `ratio` data type for fractions.

```css
@utility aspect-* {
  aspect-ratio: --value(--aspect-ratio-*, ratio, [ratio]);
}
```

This matches utilities like `aspect-square`, `aspect-3/4`, and `aspect-[7/9]`.

## Custom Variants
Use `@custom-variant` to add custom variants.

```css
@custom-variant theme-midnight {
  &:where([data-theme="midnight"] *) {
    @slot;
  }
}
```

```html
<html data-theme="midnight">
  <button class="theme-midnight:bg-black"></button>
</html>
```

Use shorthand syntax when nesting is not required.

```css
@custom-variant theme-midnight (&:where([data-theme="midnight"] *));
```

When a custom variant has multiple rules, they can be nested.

```css
@custom-variant any-hover {
  @media (any-hover: hover) {
    &:hover {
      @slot;
    }
  }
}
```