# Package Selection And Installation

Use this file when the task starts with "which Lucide package should I use?" or needs install commands.

## Package Surfaces Confirmed In The Docs
- `lucide`: core web package for general web applications and `createIcons()` usage.
- `lucide-static`: static assets such as SVG files, sprites, icon font, and server-side SVG string usage.
- `@lucide/icons`: raw icon data plus builder helpers.
- `lucide-react`: React components.
- `lucide-preact`: Preact components.
- `lucide-solid`: Solid components.
- `lucide-react-native`: React Native components. The docs say `react-native-svg` must be installed and compatible.
- `@lucide/vue`: Vue components.
- `@lucide/svelte`: Svelte components.
- `@lucide/astro`: Astro components.
- `@lucide/angular`: Angular components and providers.

## Installation Notes To Preserve Exactly
- The top-level installation guide shows `@next` commands for several surfaces such as `lucide@next`, `lucide-react@next`, `lucide-preact@next`, `lucide-solid@next`, `@lucide/astro@next`, `lucide-static@next`, and `@lucide/svelte@next`.
- Several package-specific pages show stable-looking package commands without `@next`, for example `lucide-react`, `lucide-preact`, `lucide-solid`, `lucide-static`, `@lucide/vue`, `@lucide/astro`, `@lucide/svelte`, `@lucide/angular`, and `@lucide/icons`.
- Do not reconcile those differences from memory. Re-query the exact page the user cares about and follow that page.

## Package-Specific Confirmed Notes
- The installation guide says Svelte 5 applications use `@lucide/svelte@next` and says to use `lucide-svelte` for Svelte 4.
- The package docs also contain `@lucide/svelte` package pages and examples.
- React migration docs show swapping from `react-feather` with:

```sh
npm install lucide-react
npm uninstall react-feather
```

## Selection Shortcut
- Need HTML replacement with `data-lucide` and `createIcons()`: use `lucide`.
- Need SVG files, sprite, font, image links, or server-rendered SVG strings: use `lucide-static`.
- Need raw icon data or to build SVG output yourself: use `@lucide/icons`.
- Need framework components: use the framework package for React, Preact, Solid, Vue, Svelte, Astro, React Native, or Angular.
