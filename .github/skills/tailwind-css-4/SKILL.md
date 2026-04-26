---
name: tailwind-css-4
description: 'Use when: working with Tailwind CSS 4, Tailwind v4, CSS-first configuration, @import "tailwindcss", @theme, theme variables, @source, source(), automatic class detection, @utility, @variant, @custom-variant, @apply, @reference, @config, @plugin, Vite, PostCSS, Tailwind CLI, Preflight, responsive design, container queries, dark mode, prefixes, important utilities, v3 upgrades, compatibility, Sass/Less/Stylus, CSS modules, Vue/Svelte/Astro style blocks, VS Code IntelliSense, and Prettier class sorting. Requires Context7 /websites/tailwindcss docs before adding details.'
argument-hint: 'Tailwind CSS 4 setup, CSS-first config, utility/variant, theme, upgrade, compatibility, or code review task'
---

# Tailwind CSS 4

## Purpose
Use this skill to create, review, or explain Tailwind CSS 4 usage using only details confirmed in the current Tailwind CSS documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/tailwindcss` with the exact Tailwind CSS 4 topic.
2. Do not add installation steps, package names, commands, directives, functions, utility names, variant names, browser requirements, upgrade advice, compatibility claims, editor setup, or configuration behavior unless they appear in the retrieved documentation or in the reference files below.
3. If a requested detail is not confirmed by the current documentation context, run a narrower Context7 lookup or explicitly say that the current Tailwind CSS documentation context did not confirm it.
4. Keep examples close to documented snippets and preserve documented package names, CSS directives, functions, file names, import modifiers, class syntax, variant syntax, and command flags.
5. Do not infer behavior from Tailwind CSS v3, older blog posts, framework habits, CSS preprocessors, package source code, or memory unless the Tailwind CSS 4 docs explicitly describe that behavior.

## Reference Map
- Installation with Vite, PostCSS, Tailwind CLI, framework-guide routing, editor support, VS Code IntelliSense, and Prettier class sorting: [installation-and-tooling.md](./references/installation-and-tooling.md)
- Automatic source detection, `@source`, safelisting, excluding, directives, functions, compatibility directives, and `@reference`: [source-and-directives.md](./references/source-and-directives.md)
- `@theme`, theme variable namespaces, default theme behavior, theme customization, custom CSS, arbitrary values, custom utilities, and custom variants: [theme-and-custom-styles.md](./references/theme-and-custom-styles.md)
- Utility-class workflow, variants, conflicts, `!`, `important`, prefixes, responsive design, container queries, dark mode, state variants, attribute variants, child variants, and arbitrary variants: [utilities-variants-responsive.md](./references/utilities-variants-responsive.md)
- Preflight, disabling Preflight, upgrade tool, v3 breaking changes, browser support, Sass/Less/Stylus, CSS modules, and Vue/Svelte/Astro style blocks: [preflight-upgrade-compatibility.md](./references/preflight-upgrade-compatibility.md)

## Workflow
1. Identify the Tailwind surface: setup, source scanning, CSS directive, theme variable, custom utility, variant, responsive behavior, dark mode, Preflight, v3 upgrade, compatibility, editor tooling, or code review.
2. Run a narrow Context7 query for `/websites/tailwindcss` before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For installation, choose only the documented integration path: Vite plugin, PostCSS plugin, Tailwind CLI, or a framework guide when the docs direct framework-specific setup there.
5. For configuration, prefer the documented CSS-first directives and functions: `@import`, `@theme`, `@source`, `@utility`, `@variant`, `@custom-variant`, `@apply`, `@reference`, `--alpha()`, and `--spacing()`.
6. Use `@config`, `@plugin`, and `theme()` only as documented compatibility features for Tailwind CSS v3.x migration or legacy configuration/plugin loading.
7. For source detection, require complete class names in source files, use `@source` or `source()` only as documented, and use `@source inline()` for documented safelisting.
8. For theme work, map design tokens to documented theme variable namespaces and keep `@theme` definitions top-level.
9. For utilities and variants, preserve documented class syntax for responsive prefixes, state variants, arbitrary values, arbitrary variants, `!`, `important`, `prefix()`, dark mode overrides, group/peer/in/has/not variants, child variants, and container query variants.
10. For scoped CSS, CSS modules, Vue, Svelte, Astro, or separately bundled stylesheets, use documented `@reference` behavior or documented CSS variable alternatives.
11. For upgrades from v3, use the upgrade guide reference and do not assume compatibility for removed utilities, changed defaults, JavaScript config options, preprocessors, or browser support.
12. Finish by checking that every command, package, directive, function, class syntax, variant syntax, browser requirement, and upgrade statement is traceable to the current Context7 result or one of these reference files.

## Confirmed Core Patterns
- Tailwind CSS scans source files for class names, generates matching styles, and writes static CSS with zero runtime.
- Tailwind CSS v4 setup uses `@import "tailwindcss";` instead of the old `@tailwind` directives.
- Vite, PostCSS, and Tailwind CLI have separate documented packages: `@tailwindcss/vite`, `@tailwindcss/postcss`, and `@tailwindcss/cli`.
- Tailwind CSS v4 configuration is CSS-first through directives such as `@theme`, `@source`, `@utility`, `@variant`, and `@custom-variant`.
- Theme variables defined with `@theme` influence which utilities and variants exist, and they compile to regular CSS variables.
- Tailwind source detection treats files as plain text and does not understand string concatenation or interpolation.
- Custom utilities registered with `@utility` work with variants and are inserted into the `utilities` layer.
- `@reference` imports theme variables, custom utilities, and custom variants into separately processed CSS without duplicating CSS output.
- Preflight is injected into the `base` layer when importing Tailwind CSS normally.
- Responsive utilities are mobile-first; unprefixed utilities apply to all screen sizes and breakpoint-prefixed utilities apply at that breakpoint and above.
- The default `dark` variant uses `prefers-color-scheme`, and docs show overriding it with `@custom-variant` for class or data-attribute driven dark mode.
- Tailwind CSS v4 targets Chrome 111, Safari 16.4, and Firefox 128; projects needing older browsers should stay on v3.4 according to the docs.

## Completion Check
- A fresh Context7 lookup for `/websites/tailwindcss` was used for the exact requested Tailwind CSS 4 topic.
- The answer does not include undocumented APIs, directives, utility names, variant names, commands, package names, compatibility behavior, or migration steps.
- Code examples preserve documented syntax for `@import`, `@theme`, `@source`, `@utility`, `@variant`, `@custom-variant`, `@apply`, `@reference`, `@config`, `@plugin`, `prefix()`, `important`, `source()`, `--alpha()`, `--spacing()`, `--value()`, and `--modifier()`.
- Upgrade guidance is limited to the Tailwind CSS v4 upgrade guide.
- Unsupported or unconfirmed details are left out or followed by a narrower Context7 lookup.