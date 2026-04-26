# Utilities, Variants, Responsive Design, And Dark Mode

Sources used: Tailwind CSS docs for styling with utility classes, hover/focus and other states, responsive design, and dark mode.

## Utility-Class Workflow
- Tailwind styles elements by combining single-purpose presentational utility classes directly in markup.
- The docs describe advantages over inline styles: constrained design tokens, variants for states like hover and focus, and responsive variants for media queries.
- Tailwind generates CSS based on classes it detects in project files.
- Many utilities are driven by theme variables, while arbitrary values can generate CSS for values outside the theme.

```html
<div class="mx-auto flex max-w-sm items-center gap-x-4 rounded-xl bg-white p-6 shadow-lg outline outline-black/5 dark:bg-slate-800 dark:shadow-none dark:-outline-offset-1 dark:outline-white/10">
  <img class="size-12 shrink-0" src="/img/logo.svg" alt="ChitChat Logo" />
  <div>
    <div class="text-xl font-medium text-black dark:text-white">ChitChat</div>
    <p class="text-gray-500 dark:text-gray-400">You have a new message!</p>
  </div>
</div>
```

## Variants
- Every utility class can be conditionally applied by prefixing a variant.
- Variants cover pseudo-classes, pseudo-elements, media and feature queries, attribute selectors, and child selectors.
- Variants can be stacked, such as `dark:md:hover:bg-fuchsia-600`.
- In v4, order-sensitive stacked variants apply left to right according to the upgrade guide.

```html
<button class="bg-sky-500 hover:bg-sky-700">Save changes</button>
<button class="dark:md:hover:bg-fuchsia-600">Save changes</button>
```

## Utility Composition
The docs show utilities composing through CSS variables for effects such as filters, and state that Tailwind uses the same approach for gradients, shadow colors, transforms, and more.

```html
<div class="blur-sm grayscale"></div>
```

## Managing Duplication
The docs describe these documented approaches:
- Use loops when repeated rendered elements are authored once.
- Use multi-cursor editing when duplication is localized to a group of elements in a single file.
- Use components in React, Svelte, Vue, or template partials in Blade, ERB, Twig, or Nunjucks when styles need reuse across multiple files.
- Use custom CSS when a template partial feels heavy for small cases, and use theme variables for consistency.

## Style Conflicts, Important, And Prefixes
When two classes target the same CSS property, the class later in the stylesheet wins, not the class later in the HTML `class` attribute. The docs advise not adding two conflicting classes to the same element.

Use `!` at the end of a class to make its declarations `!important`.

```html
<div class="bg-teal-500 bg-red-500!"></div>
```

Use the `important` flag on the Tailwind import to mark all utilities as `!important`.

```css
@import "tailwindcss" important;
```

Use `prefix()` on the Tailwind import to prefix generated classes and CSS variables.

```css
@import "tailwindcss" prefix(tw);
```

The docs show generated classes like `.tw\:text-red-500` and prefixed variables like `--tw-color-red-500`.

## Responsive Design
Add the viewport meta tag before relying on responsive utilities.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Prefix utilities with breakpoint names to apply them at that breakpoint and above.

```html
<img class="w-16 md:w-32 lg:w-48" src="..." />
```

Default viewport breakpoints:

| Variant | Width | Media query |
| --- | --- | --- |
| `sm` | 40rem (640px) | `@media (width >= 40rem) { ... }` |
| `md` | 48rem (768px) | `@media (width >= 48rem) { ... }` |
| `lg` | 64rem (1024px) | `@media (width >= 64rem) { ... }` |
| `xl` | 80rem (1280px) | `@media (width >= 80rem) { ... }` |
| `2xl` | 96rem (1536px) | `@media (width >= 96rem) { ... }` |

Tailwind uses a mobile-first breakpoint system:
- Unprefixed utilities apply on all screen sizes.
- Prefixed utilities like `md:uppercase` apply at that breakpoint and above.
- Use unprefixed utilities for mobile and override them at larger breakpoints.

```html
<div class="text-center sm:text-left"></div>
```

Use `max-*` variants to target ranges.

```html
<div class="md:max-xl:flex"></div>
<div class="md:max-lg:flex"></div>
```

Documented max variants are `max-sm`, `max-md`, `max-lg`, `max-xl`, and `max-2xl`.

Customize breakpoints with `--breakpoint-*` theme variables.

```css
@import "tailwindcss";

@theme {
  --breakpoint-xs: 30rem;
  --breakpoint-2xl: 100rem;
  --breakpoint-3xl: 120rem;
}
```

The docs say to use the same unit for breakpoint definitions because mixed units can sort unexpectedly; Tailwind defaults use `rem`.

Remove a default breakpoint by setting it to `initial`, or reset all defaults with `--breakpoint-*: initial`.

```css
@import "tailwindcss";

@theme {
  --breakpoint-2xl: initial;
}
```

```css
@import "tailwindcss";

@theme {
  --breakpoint-*: initial;
  --breakpoint-tablet: 40rem;
  --breakpoint-laptop: 64rem;
  --breakpoint-desktop: 80rem;
}
```

Use `min-[...]` and `max-[...]` for one-off breakpoints.

```html
<div class="max-[600px]:bg-sky-300 min-[320px]:text-center"></div>
```

## Container Queries
Use `@container` to mark an element as a container, then use variants like `@sm` and `@md` on children.

```html
<div class="@container">
  <div class="flex flex-col @md:flex-row"></div>
</div>
```

Container queries are mobile-first and apply at the target container size and up.

Use `@max-*` for styles below a container size.

```html
<div class="@container">
  <div class="flex flex-row @max-md:flex-col"></div>
</div>
```

Stack regular and max container variants for ranges.

```html
<div class="@container">
  <div class="flex flex-row @sm:@max-md:flex-col"></div>
</div>
```

Name containers with `@container/{name}` and target them with variants like `@sm/{name}`.

```html
<div class="@container/main">
  <div class="flex flex-row @sm/main:flex-col"></div>
</div>
```

Customize container sizes with `--container-*`.

```css
@import "tailwindcss";

@theme {
  --container-8xl: 96rem;
}
```

Use arbitrary container sizes with `@min-[...]` and `@max-[...]`, and use container query units like `cqw` in arbitrary values.

```html
<div class="@container">
  <div class="flex flex-col @min-[475px]:flex-row"></div>
  <div class="w-[50cqw]"></div>
</div>
```

Default container size variants:

| Variant | Width |
| --- | --- |
| `@3xs` | 16rem (256px) |
| `@2xs` | 18rem (288px) |
| `@xs` | 20rem (320px) |
| `@sm` | 24rem (384px) |
| `@md` | 28rem (448px) |
| `@lg` | 32rem (512px) |
| `@xl` | 36rem (576px) |
| `@2xl` | 42rem (672px) |
| `@3xl` | 48rem (768px) |
| `@4xl` | 56rem (896px) |
| `@5xl` | 64rem (1024px) |
| `@6xl` | 72rem (1152px) |
| `@7xl` | 80rem (1280px) |

## Dark Mode
The default `dark` variant uses the `prefers-color-scheme` media feature.

```html
<div class="bg-white dark:bg-gray-800">
  <h3 class="text-gray-900 dark:text-white">Writes upside-down</h3>
  <p class="text-gray-500 dark:text-gray-400"></p>
</div>
```

Override `dark` with a selector to manually toggle dark mode.

```css
@import "tailwindcss";
@custom-variant dark (&:where(.dark, .dark *));
```

```html
<html class="dark">
  <body>
    <div class="bg-white dark:bg-black"></div>
  </body>
</html>
```

Override `dark` with a data attribute.

```css
@import "tailwindcss";
@custom-variant dark (&:where([data-theme=dark], [data-theme=dark] *));
```

```html
<html data-theme="dark">
  <body>
    <div class="bg-white dark:bg-black"></div>
  </body>
</html>
```

The docs show a three-way theme toggle using a custom dark selector, `window.matchMedia()`, `localStorage.theme = "light"`, `localStorage.theme = "dark"`, and `localStorage.removeItem("theme")`.

## Pseudo-Class Variants
Documented pseudo-class variants include `hover`, `focus`, `focus-within`, `focus-visible`, `active`, `visited`, `target`, `first`, `last`, `only`, `odd`, `even`, `first-of-type`, `last-of-type`, `only-of-type`, `nth-*`, `nth-last-*`, `nth-of-type-*`, `nth-last-of-type-*`, `empty`, `disabled`, `enabled`, `checked`, `indeterminate`, `default`, `optional`, `required`, `valid`, `invalid`, `user-valid`, `user-invalid`, `in-range`, `out-of-range`, `placeholder-shown`, `details-content`, `autofill`, and `read-only`.

Use `has-*` to style an element based on descendants.

```html
<label class="has-checked:bg-indigo-50 has-checked:text-indigo-900"></label>
```

Use `not-*` when a condition is not true.

```html
<button class="bg-indigo-600 hover:not-focus:bg-indigo-700"></button>
```

## Parent, Ancestor, And Sibling State
Use `group` and `group-*` variants for parent state.

```html
<a class="group">
  <span class="group-hover:underline">Read more...</span>
</a>
```

Groups can be named with `group/{name}` and targeted with variants such as `group-hover/{name}`. Arbitrary group variants use `group-[...]`; the `&` character marks where `.group` ends up in the final selector. The `in-*` variant responds to state changes in any parent without adding `group`, while `group` is used for finer control.

Use `peer` and `peer-*` variants for previous sibling state.

```html
<form>
  <input type="email" class="peer" />
  <p class="invisible peer-invalid:visible">Please provide a valid email address.</p>
</form>
```

The docs note that the `peer` marker can only be used on previous siblings because of the subsequent-sibling combinator. Peers can be named with `peer/{name}` and targeted with variants like `peer-checked/{name}`. Arbitrary peer variants use `peer-[...]`.

## Pseudo-Element Variants
Documented pseudo-element variants include `before`, `after`, `placeholder`, `file`, `marker`, `selection`, `first-line`, `first-letter`, and `backdrop`.

- `before` and `after` automatically add `content: ''` by default unless a different value is specified.
- The docs say real HTML elements are usually simpler than `before` and `after`; save them for cases where pseudo-element content should not be in the DOM or selectable.
- `marker` and `selection` are inheritable, so they can be applied on a parent.
- `backdrop` styles the backdrop of native `<dialog>` elements.

## Media And Feature Query Variants
Documented media and feature query variants include:
- Responsive variants: `sm`, `md`, `lg`, `xl`, `2xl`, `min-[...]`, `max-*`, `max-[...]`.
- Container variants: `@3xs` through `@7xl`, `@min-[...]`, `@max-*`, `@max-[...]`.
- `dark` for `prefers-color-scheme: dark` by default.
- `motion-safe` and `motion-reduce` for `prefers-reduced-motion`.
- `contrast-more` and `contrast-less` for `prefers-contrast`.
- `forced-colors` and `not-forced-colors` for forced colors mode.
- `inverted-colors` for inverted color schemes.
- `pointer-fine`, `pointer-coarse`, `pointer-none`, `any-pointer-fine`, `any-pointer-coarse`, and `any-pointer-none`.
- `portrait` and `landscape`.
- `noscript`.
- `print`.
- `supports-[...]` and `not-supports-[...]`.
- `starting` for `@starting-style`.

The docs show creating `supports-*` shortcuts with `@custom-variant`.

```css
@custom-variant supports-grid {
  @supports (display: grid) {
    @slot;
  }
}
```

## Attribute Variants
Documented ARIA boolean variants include `aria-busy`, `aria-checked`, `aria-disabled`, `aria-expanded`, `aria-hidden`, `aria-pressed`, `aria-readonly`, `aria-required`, and `aria-selected`.

```html
<div aria-checked="true" class="bg-gray-600 aria-checked:bg-sky-700"></div>
```

Use arbitrary ARIA variants for specific values.

```html
<th aria-sort="ascending" class="aria-[sort=ascending]:bg-[url('/img/down-arrow.svg')]"></th>
```

ARIA variants can target parent and sibling elements with `group-aria-*` and `peer-aria-*`.

Use `data-*` to style based on data attributes.

```html
<div data-active class="border border-gray-300 data-active:border-purple-500"></div>
<div data-size="large" class="data-[size=large]:p-8"></div>
```

Configure data-attribute shortcuts with `@custom-variant` in the `data-*` namespace.

```css
@import "tailwindcss";
@custom-variant data-checked (&[data-ui~="checked"]);
```

Use `rtl` and `ltr` for right-to-left and left-to-right modes. Use `open` for `<details>`, `<dialog>`, and popovers in open states. Use `inert` for elements marked with the `inert` attribute.

## Child Variants
Use `*` for direct children and `**` for all descendants.

```html
<ul class="*:rounded-full *:border *:border-sky-100 *:bg-sky-50 *:px-2 *:py-0.5"></ul>
<ul class="**:data-avatar:size-12 **:data-avatar:rounded-full"></ul>
```

The docs note that overriding a style with a utility directly on the child will not work when a parent child-variant rule targets it, because children rules are generated after regular ones and have the same specificity.

## Arbitrary Variants
Arbitrary variants are selector format strings wrapped in square brackets.

```html
<li class="[&.is-dragging]:cursor-grabbing"></li>
<li class="[&.is-dragging]:active:cursor-grabbing"></li>
<div class="[&_p]:mt-4"></div>
<div class="flex [@supports(display:grid)]:grid"></div>
```

Use `_` for spaces inside arbitrary variant selectors. With at-rule arbitrary variants like `@media` or `@supports`, the `&` placeholder is not necessary.

If the same arbitrary variant is used repeatedly, the docs suggest registering a custom variant with `@custom-variant`.