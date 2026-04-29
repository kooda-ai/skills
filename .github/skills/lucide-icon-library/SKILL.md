---
name: lucide-icon-library
description: 'Use when: working with Lucide icons, lucide, lucide-react, lucide-preact, lucide-solid, lucide-react-native, @lucide/vue, @lucide/svelte, @lucide/astro, @lucide/angular, @lucide/icons, lucide-static, createIcons, DynamicIcon, LucideProvider, setLucideProps, provideLucideIcons, provideLucideConfig, lucideLegacyIcon, IconNode, LucideProps, aliased names, accessibility, global styling, custom icons, filled icons, static assets, and Angular migration. Requires Context7 /websites/lucide_dev_guide docs before adding details.'
argument-hint: 'Lucide package selection, installation, web/core usage, framework package usage, static assets, builders API, accessibility, custom icons, Angular migration, or code review'
---

# Lucide Icon Library

## Purpose
Use this skill to create, review, or explain Lucide usage using only details confirmed in the current Context7 documentation for `/websites/lucide_dev_guide`.

## Source Rule
1. Before giving final code or guidance, query Context7 for the exact Lucide topic the user asked about.
2. Do not add package names, commands, imports, components, props, directives, helper functions, builder functions, type names, migration mappings, or accessibility behavior unless they appear in the retrieved Lucide docs or the reference files below.
3. If the docs for one Lucide page show a different install command or package variant than another page, do not normalize them from memory. Re-query the exact page or topic and follow that page.
4. Keep examples close to documented snippets and preserve documented casing, import paths, prop names, attribute names, and package names.
5. Do not infer behavior from framework habits, SVG conventions, package source code, old Lucide versions, or memory when the current Lucide docs did not confirm it.

## Reference Map
- Package selection and install surfaces: [package-selection-and-installation.md](./references/package-selection-and-installation.md)
- Core web usage, static assets, and raw icon data builders: [core-web-static-and-builders.md](./references/core-web-static-and-builders.md)
- Framework component usage, styling, props, and package-specific patterns: [framework-components-and-styling.md](./references/framework-components-and-styling.md)
- Accessibility, dynamic loading, custom icons, and composition patterns: [accessibility-dynamic-and-custom-icons.md](./references/accessibility-dynamic-and-custom-icons.md)
- Angular package details, provider APIs, typing, and migration: [angular-package-and-migration.md](./references/angular-package-and-migration.md)

## Workflow
1. Identify the Lucide surface first: package selection, installation, core web, framework component usage, static assets, builders, accessibility, dynamic loading, custom icons, styling, Angular, or migration.
2. Run a narrow Context7 query for `/websites/lucide_dev_guide` before producing code or review findings.
3. Load the matching reference file from the map above.
4. Choose the documented package only for the target surface: `lucide`, `lucide-static`, `@lucide/icons`, framework-specific component packages, or `@lucide/angular`.
5. For core web usage, stay within documented `createIcons()` behavior, `data-lucide`, CDN usage, and documented `createIcons` options such as `attrs`, `nameAttr`, `root`, and `inTemplates`.
6. For framework packages, use only the documented imports, props, provider APIs, and type helpers for that package.
7. For styling, verify whether the docs show prop-based styling, parent `currentColor`, CSS class styling, Tailwind `size-*`, context/provider defaults, or global `.lucide` styling for that package.
8. For accessibility, confirm whether the docs show `aria-label`, `<title>`, button labeling, visually hidden text, or default hidden behavior for the specific package.
9. For dynamic loading, keep the docs' cautions about importing all icons, build size, and performance. Do not invent a safer API if the docs did not provide one.
10. For custom icons and Lucide Lab, use only documented `Icon` or package-specific APIs such as `iconNode`, `lucideLegacyIcon`, `LucideIconBase`, or `provideLucideIcons`.
11. For `@lucide/icons`, treat imports as icon data, not rendered components, and use only documented builder helpers and build parameters.
12. Finish by checking that every command, import path, component, prop, helper, type, and migration claim is traceable to the current Context7 result or the reference files.

## Confirmed Core Patterns
- Lucide is documented as an open-source icon library with over 1000 vector SVG files and official packages.
- The docs separate core web usage (`lucide`), static asset usage (`lucide-static`), raw icon data and builders (`@lucide/icons`), and framework-specific component packages.
- Core web usage replaces elements such as `<i data-lucide="menu"></i>` with SVGs via `createIcons()`.
- Framework packages document importing icons as components, and multiple package pages explicitly recommend importing only the icons you need for tree-shaking.
- Some package docs show direct icon subpath imports such as `@lucide/astro/icons/...`, `@lucide/svelte/icons/...`, and `lucide-solid/icons/...`.
- Lucide icons use `currentColor` by default in multiple package docs, so parent text color can drive icon color.
- Docs across packages show `size`, `color`, `strokeWidth`, and `absoluteStrokeWidth`, but exact prop naming and casing must be checked per package.
- Multiple docs warn that generic loaders or importing all icons can significantly increase build size and negatively impact performance.
- `@lucide/icons` exports icon data and builder helpers; the docs explicitly say imported icons there are icon data, not rendered components.
- Angular has a separate documented surface with `LucideIcon`, `LucideDynamicIcon`, `provideLucideIcons`, `provideLucideConfig`, `lucideLegacyIcon`, and migration guidance from `lucide-angular`.

## Completion Check
- A fresh Context7 lookup for `/websites/lucide_dev_guide` was used for the user's exact Lucide topic.
- The answer does not include undocumented Lucide packages, props, helper names, migration rules, or accessibility claims.
- The answer keeps package boundaries clear between `lucide`, `lucide-static`, `@lucide/icons`, framework component packages, and Angular-specific APIs.
- Any mismatch between install pages and package pages is resolved by re-querying the exact requested topic instead of guessing.
- Unconfirmed details are omitted or explicitly described as not confirmed by the current Lucide documentation context.
