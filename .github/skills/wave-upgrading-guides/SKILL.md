---
name: wave-upgrading-guides
description: 'Use when: working with Wave upgrades, manual Wave upgrade steps, theme upgrade implications, the Wave guides index, current Wave guides, support/help links, and using the documented Filament-with-Volt guide as a Wave-specific reference. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave upgrade, guide lookup, support resource, or documented guide task'
---

# Wave Upgrading And Guides

## Purpose
Use this skill for Wave upgrade steps, upgrade constraints, guide discovery, and Wave-specific guidance that comes from the published guides index and current guide pages.

## Source Rule
1. Before giving final upgrade or guide-based guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add upgrade steps, replacement paths, cache commands, guide names, or support links unless they appear in the current Wave docs.
3. If the task needs deeper framework or package guidance than the published Wave guide provides, say that clearly and query those product docs separately.
4. Keep examples close to documented folder names, commands, and guide titles.

## Reference Map
- Manual upgrade steps, theme-upgrade implications, and published guide/support surfaces: [manual-upgrades-and-guides.md](./references/manual-upgrades-and-guides.md)

## Related Wave Skills
- Use `wave-installation-development` for setup, defaults, stack, and documented development entry points before upgrade work begins.
- Use `wave-customization-theming` when upgrade questions focus on theme files, layouts, assets, or manually porting visual changes.
- Use `wave-plugins-concepts` when guide or upgrade questions depend on plugins, Volt pages, Folio mapping, or Filament-with-Volt patterns.

## Workflow
1. Identify whether the task is upgrade planning, theme-upgrade impact, locating a Wave guide, or applying the Filament-with-Volt guide.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only the documented manual upgrade path until the docs confirm a different process.
5. When answering from a guide, stay inside what that guide explicitly shows.
6. Omit unconfirmed guide or upgrade behavior.

## Confirmed Core Patterns
- The upgrading docs currently describe a manual upgrade path.
- The documented upgrade flow says to replace the root `wave` folder and the `app/Filament` folder with the latest copies.
- The upgrade docs then show `composer dump-autoload` and `php artisan cache:clear`.
- The docs say admin customizations may need to be ported manually.
- The docs say theme upgrades are usually not required unless a new feature introduces corresponding views that you want to bring over.
- The guides index currently lists `Using Filament With Volt` as the current guide confirmed by the fetched docs.
- The guides index also mentions planned guides for adding the table builder to a page, adding the form builder to a page, and adding the billing component to any page.
- The guides page links to Wave documentation, DevDojo Questions, and DevDojo help/support.
- The `Using Filament with Volt` guide demonstrates using a Filament table, a Filament form, and a combined table-plus-form Volt page inside Wave theme pages.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact upgrade or guide topic.
- Every upgrade step, replacement path, command, guide title, and support link is traceable to the current Wave docs.
- Broader framework or package behavior is not inferred beyond what the Wave docs or current Wave guides confirm.
