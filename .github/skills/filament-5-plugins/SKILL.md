---
name: filament-5-plugins
description: 'Use when: working with Filament 5 Plugins, Panel Plugins, Standalone Plugins, plugin objects, Filament\Contracts\Plugin, getId(), register(), boot(), plugin(), make(), per-panel plugin configuration, filament(''id''), Panel::configureUsing(), modular architecture plugins, discoverResources(), discoverPages(), discoverWidgets(), distributing panels with PanelProvider, plugin assets, plugin skeletons, and plugin upgrades. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Plugin task, panel plugin class, package/plugin code, modular plugin registration, distributed panel, upgrade, or code to review'
---

# Filament 5 Plugins

## Purpose
Use this skill to create, review, or explain Filament 5 plugins using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Plugins topic.
2. Do not add behavior, APIs, commands, package structure, lifecycle timing, service-provider details, asset behavior, modular architecture patterns, panel configuration options, namespaces, or conventions unless they appear in the retrieved documentation.
3. If a requested Plugins topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad plugin tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, command names, Composer keys, and class names.

## Reference Map
- Plugin contexts, plugin object scope, asset registration, plugin skeleton, and upgrade notes: [plugin-concepts.md](./references/plugin-concepts.md)
- Panel plugin class shape, lifecycle, panel registration, fluent instantiation, and per-panel options: [panel-plugin-class.md](./references/panel-plugin-class.md)
- Modular architecture plugins, conditional panel registration, module discovery, Livewire components, and distributing full panels: [modular-distribution.md](./references/modular-distribution.md)

## Workflow
1. Identify the plugin surface: plugin concepts, panel plugin class, standalone plugin service-provider behavior, per-panel configuration, asset registration, modular architecture, conditional registration, full panel distribution, plugin skeleton setup, upgrade review, or package code review.
2. Run a narrow Context7 query for the exact Filament 5 Plugins topic before producing code.
3. Load the relevant reference file from the map above.
4. For plugin object work, distinguish Panel Plugins from Standalone Plugins. The docs state the Plugin object is only used for Panel Providers; Standalone Plugin configuration belongs in the plugin service provider.
5. For panel plugin classes, use only documented `Filament\Contracts\Plugin`, `getId(): string`, `register(Panel $panel): void`, `boot(Panel $panel): void`, and `Filament\Panel` patterns confirmed for the task.
6. In `register()`, use only panel configuration options confirmed by the current lookup. If the task enters resources, pages, widgets, navigation, styling, render hooks, forms, tables, actions, users, or notifications, load the matching Filament 5 skill after a fresh Context7 lookup for that subtopic.
7. In `boot()`, include only runtime work confirmed by the docs, such as module Livewire component registration when the modular architecture docs are the active source.
8. For fluent plugin creation, use only the documented `public static function make(): static { return app(static::class); }` pattern and panel usage with `->plugin(BlogPlugin::make())` when confirmed.
9. For per-panel plugin options, use documented setter/getter property patterns, `filament('blog')->hasAuthorResource()`, or a documented static `get()` helper only when the lookup confirms that configuration access pattern.
10. For modular architecture, use documented `Panel::configureUsing()`, `$panel->getId()`, `$panel->plugin(...)`, `discoverResources()`, `discoverPages()`, and `discoverWidgets()` patterns only when confirmed.
11. For distributing a whole panel, use the documented `PanelProvider` service-provider pattern and Composer `extra.laravel.providers` registration only when confirmed.
12. Finish by checking that every command, class, method, interface, import, Composer key, package path, lifecycle claim, and code example is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Filament has two plugin contexts: Panel Plugins for Panel Builder features or complete panels, and Standalone Plugins for contexts outside a Panel Builder.
- Panel Plugin examples include dashboard widgets and sets of resources or functionality such as Blog or User Management features.
- Standalone Plugin examples include custom form fields, table columns, and table filters.
- The Plugin object is a PHP class implementing `Filament\Contracts\Plugin`; the docs state it is the main entry point for configuring a plugin and registering resources and icons.
- The Plugin object is only used for Panel Providers; Standalone Plugin configuration should be handled in the plugin service provider.
- The docs state plugin assets, including CSS, JavaScript, and Alpine components, should be registered through the plugin service provider in `packageBooted()`.
- The docs recommend the Filament Plugin Skeleton for creating a plugin and confirm running `php ./configure.php` from the project root after using the template and cloning it.
- Existing plugin upgrades should account for the deprecation of `PluginServiceProvider`; the docs show extending `PackageServiceProvider`, adding `public static string $name`, and configuring the package name in `configurePackage(Package $package): void`.
- Panel plugin classes implement `Filament\Contracts\Plugin` and define `getId()`, `register(Panel $panel)`, and `boot(Panel $panel)`.
- `getId()` returns a unique plugin identifier specific enough not to clash with other plugins in the same project.
- `register()` can use panel configuration options, including resources, custom pages, themes, render hooks, and more.
- `boot()` runs only when the panel receiving the plugin is actually in use, and the docs state it is executed by middleware.
- Users can add a plugin to a panel with `->plugin(new BlogPlugin())` or, with the documented fluent pattern, `->plugin(BlogPlugin::make())`.
- Per-panel options use documented setter/getter methods backed by a property, and the setter returns `static` for fluent chaining.
- Plugin configuration can be accessed by ID with `filament('blog')->hasAuthorResource()`, and the docs show an optional static `get()` helper returning `filament(app(static::class)->getId())`.
- Modular architecture plugins can register module resources, pages, and widgets with `discoverResources()`, `discoverPages()`, and `discoverWidgets()`.
- `Panel::configureUsing()` can conditionally register a module plugin for specific panels based on `$panel->getId()`.
- A package can distribute an entire panel by providing a `PanelProvider` and registering it in Composer under `extra.laravel.providers`.

## Completion Check
- The answer uses only APIs, commands, package paths, Composer keys, classes, interfaces, and lifecycle details confirmed by the current Context7 lookup.
- Each plugin object pattern, service-provider claim, asset instruction, modular architecture pattern, panel registration choice, and distributed-panel example is traceable to retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Laravel habits, Livewire habits, Spatie Package Tools habits, package source code, or memory.
- If the user asks for plugin behavior not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, return types, Composer keys, package paths, and command strings intact.