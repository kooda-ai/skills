---
name: wave-plugins-concepts
description: 'Use when: working with Wave plug-ins, resources/plugins, installed.json, plugin register/boot lifecycle, plugin autoloading, Volt pages, Folio route mapping in Wave themes, Wave Blade directives, adding custom functionality with Volt pages, and Filament-with-Volt concepts documented by Wave. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave plugin, Volt page, Folio mapping, Blade directive, or functionality pattern task'
---

# Wave Plugins And Concepts

## Purpose
Use this skill for Wave extension patterns around plugins, Volt pages, Folio route mapping, Blade directives, and the documented approach for adding custom functionality.

## Source Rule
1. Before giving final plugin or concept guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add plugin folder structure, loading order, Volt route mapping, directive names, or Filament-with-Volt patterns unless they appear in the current Wave docs.
3. If the task needs deeper Laravel service provider, Folio, Volt, Livewire, or Filament behavior, say that the Wave docs defer to those products.
4. Keep examples close to documented paths, directives, and code patterns.

## Reference Map
- Plugin structure, loading lifecycle, Volt/Folio mapping, Blade directives, and Filament-with-Volt patterns: [plugins-volt-and-functionality-patterns.md](./references/plugins-volt-and-functionality-patterns.md)

## Related Wave Skills
- Use `wave-customization-theming` for theme folders, layouts, assets, view namespace behavior, and visual customization work.
- Use `wave-installation-development` for setup defaults, stack questions, and the higher-level documented starting point for new development.
- Use `wave-access-control-admin` when the task is really about admin behavior, roles, permissions, analytics, or Wave directives in access-control contexts.
- Use `wave-volt-pages` when the task is specifically about theme page routing, Folio mapping, or single-file Volt pages.
- Use `wave-blade-directives` when the task is specifically about documented Wave directive selection or usage.
- Use `wave-upgrading-guides` when plugin or Volt work is being evaluated for upgrade impact or against published Wave guides.

## Workflow
1. Identify whether the task is plugin installation, plugin lifecycle, Volt page mapping, Blade directives, custom functionality structure, or Filament-with-Volt usage.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Hand off to `wave-volt-pages` for page-routing and Volt-only questions, or `wave-blade-directives` for directive-only questions.
5. Use documented Wave plugin directories, lifecycle order, page paths, and directive names only.
6. Prefer the documented single-file Volt pattern for new functionality when the Wave docs recommend it.
7. Omit framework details not confirmed by the Wave docs.

## Confirmed Core Patterns
- Plugins are stored in `resources/plugins`.
- Installed plugin names are tracked in `resources/plugins/installed.json`.
- Plugins are activated from `/admin/plugins`.
- The docs describe a main plugin class such as `resources/plugins/example/ExamplePlugin.php`.
- The plugin `boot()` method is documented for loading views, migrations, routes, and Livewire components.
- The plugin `register()` method is documented for binding services and registering utilities before boot logic runs.
- The plugin system autoloads classes from the plugin `src` folder with PSR-4 style behavior.
- The documented plugin loading order is: read `installed.json`, instantiate each plugin class, call `register()` on all plugins, then call `boot()` on each plugin.
- Theme `pages` directories are mapped to routes using Laravel Folio.
- The docs show page-to-route examples such as `pages/index.blade.php` to `/`, `pages/about.blade.php` to `/about`, and `pages/blog/[post].blade.php` to `/blog/{post}`.
- The docs say those page files can contain single-file Volt components.
- Wave documents these Blade directives: `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`.
- The `your-functionality` docs recommend single-file Volt pages in `resources/themes/{theme}/pages` for new functionality.
- The docs say complex logic can still move into services or controllers.
- The Filament-with-Volt guide demonstrates using Filament table and form builders directly inside Wave theme Volt pages.
- The guide shows rendering a table with `{{ $this->table }}` and a form with `{{ $this->form }}` in a Volt page.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact plugin or concept topic.
- Every folder path, directive, lifecycle statement, route mapping, and documented pattern is traceable to the current Wave docs.
- Deeper Laravel, Livewire, Volt, Folio, or Filament behavior is not inferred beyond what the Wave docs confirm.
