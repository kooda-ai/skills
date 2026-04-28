---
name: wave-volt-pages
description: 'Use when: working with Wave Volt pages, Laravel Folio route mapping in Wave themes, single-file Volt pages inside resources/themes/{theme}/pages, and the documented Wave pattern for adding functionality through theme pages. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave Volt page, Folio route mapping, or theme page functionality task'
---

# Wave Volt Pages

## Purpose
Use this skill for Wave theme page routing through Laravel Folio, single-file Volt pages, and the documented Wave pattern for adding functionality inside theme page files.

## Source Rule
1. Before giving final Wave Volt or theme-page guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add route mapping behavior, theme page paths, Volt usage patterns, or Wave functionality structure unless it appears in the current Wave docs.
3. If the task needs deeper Folio, Volt, Livewire, or Laravel behavior, say that the Wave docs defer to those products.
4. Keep examples close to documented paths, route examples, and Wave-specific patterns.

## Reference Map
- Theme page mapping, Volt usage, and the documented Wave functionality pattern: [volt-pages-and-folio-mapping.md](./references/volt-pages-and-folio-mapping.md)

## Related Wave Skills
- Use `wave-plugins-concepts` for plugin lifecycle, Filament-with-Volt, and broader extension patterns beyond page routing.
- Use `wave-customization-theming` for theme layouts, theme assets, view namespace behavior, and visual theme structure.
- Use `wave-installation-development` for first-run setup, stack details, and the broader Wave development starting point.

## Workflow
1. Identify whether the task is Folio route mapping, single-file Volt page behavior, adding functionality in `resources/themes/{theme}/pages`, or choosing the documented Wave implementation pattern.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only documented Wave theme page paths, route mapping examples, and Volt usage guidance.
5. Prefer the documented single-file Volt pattern when the Wave docs recommend it.
6. Omit framework details not confirmed by the Wave docs.

## Confirmed Core Patterns
- Theme `pages` directories are mapped to routes using Laravel Folio.
- The docs show route examples such as `pages/index.blade.php` to `/`, `pages/about.blade.php` to `/about`, and `pages/blog/[post].blade.php` to `/blog/{post}`.
- The docs say those page files can contain single-file Volt components.
- The `your-functionality` docs recommend single-file Volt pages in `resources/themes/{theme}/pages` for new functionality.
- The docs say complex logic can still move into services or controllers.
- The Wave guide `Using Filament With Volt` demonstrates using Filament form and table builders directly inside Wave theme Volt pages.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact Volt-page topic.
- Every route mapping, page path, and implementation-pattern statement is traceable to the current Wave docs.
- Deeper Folio, Volt, Livewire, or Laravel behavior is not inferred beyond what the Wave docs confirm.
