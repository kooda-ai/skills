---
name: filament-5-advanced-modular-architecture
description: 'Use when: working with Filament 5 Advanced Modular Architecture, DDD-style domain modules, app-modules, module composer.json, module service providers, module Plugin classes, Panel::configureUsing(), panel IDs, discoverResources(), discoverPages(), discoverWidgets(), per-panel module plugin configuration, Livewire components in module boot(), distributed panels, and PanelProvider packages. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Modular architecture task, DDD module boundary, module plugin, Panel::configureUsing setup, distributed panel, or code to review'
---

# Filament 5 Advanced Modular Architecture

## Purpose
Use this skill to create, review, or explain Filament 5 modular architecture for large-scale applications using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Advanced Modular Architecture, Plugins, or Panel Plugin topic.
2. Do not add DDD concepts, module folder layers, package tools, generator commands, service-provider behavior, lifecycle claims, namespaces, panel IDs, APIs, or conventions unless they appear in the retrieved documentation.
3. If the user asks for DDD concepts not confirmed by the retrieved Filament docs, say that the current documentation context only confirms self-contained domain modules as Composer packages and leave unsupported DDD tactics out.
4. Split broad module work into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, Composer keys, class names, and panel configuration calls.

## Reference Map
- Modular approach, DDD scope, module directory example, and module `composer.json`: [module-foundation.md](./references/module-foundation.md)
- Module plugin class, discovery APIs, conditional panel registration, per-panel configuration, and Livewire component registration: [module-panel-registration.md](./references/module-panel-registration.md)
- Complete panel distribution from a package with `PanelProvider` and Composer provider registration: [distributed-panels.md](./references/distributed-panels.md)

## Workflow
1. Identify the modular architecture surface: module structure, module Composer metadata, Filament resources/pages/widgets inside a module, module plugin class, conditional panel registration, per-panel plugin options, Livewire component registration, distributed panel, or review of existing module code.
2. Run a narrow Context7 query for the exact Filament 5 topic before producing code.
3. Load the relevant reference file from the map above.
4. For DDD requests, limit the explanation to the documented modular approach: large-scale applications split into self-contained modules based on Domain-Driven Design principles, where each module acts as a distinct domain and is structured as a separate Composer package, typically in `app-modules/`.
5. For module structure, use only documented directories and files from the module example, including `composer.json`, `config`, `database`, `resources/views/filament/pages`, `routes/web.php`, `src/AlertsPlugin.php`, `src/Filament/Pages`, `src/Filament/Resources`, `src/Filament/Widgets`, `src/Models`, `src/Providers/AlertsServiceProvider.php`, and `tests`.
6. For module Composer metadata, use only the documented `name`, `type`, `require.filament/filament`, `autoload.psr-4`, and `extra.laravel.providers` shape when confirmed by the current lookup.
7. For module plugin classes, use only documented `Filament\Contracts\Plugin`, `Filament\Panel`, `getId(): string`, `public static function make(): static`, `register(Panel $panel): void`, and `boot(Panel $panel): void` patterns.
8. For registering module Filament classes, use documented `discoverResources(in: ..., for: ...)`, `discoverPages(in: ..., for: ...)`, and `discoverWidgets(in: ..., for: ...)` when the current lookup confirms the module discovery pattern.
9. For conditional panel registration, use documented `Panel::configureUsing(function (Panel $panel): void { ... })`, `$panel->getId()`, and `$panel->plugin(...)` patterns in the module service provider.
10. For per-panel plugin behavior, use documented fluent plugin configuration patterns only when the lookup confirms the setter/getter property and differently configured plugin instances per panel.
11. For custom Livewire components used by Filament inside modules, use the documented `Livewire::component(...)` call from the plugin `boot()` method only when confirmed.
12. For distributing an entire panel, use the documented `PanelProvider` class extending `Filament\PanelProvider`, the `panel(Panel $panel): Panel` method, and Composer `extra.laravel.providers` registration only when confirmed.
13. If the task enters Resource internals, page routes, schema fields, tables, widgets, actions, assets, navigation, users, notifications, or panel runtime configuration beyond the modular touchpoint, load the matching Filament 5 skill after a fresh Context7 lookup for that subtopic.
14. Finish by checking that every class, import, method, Composer key, namespace, path, panel ID rule, lifecycle claim, and code example is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- The docs describe modular architecture for large-scale Filament applications that use Domain-Driven Design principles.
- The docs state that each module acts as a distinct domain and is structured as a separate Composer package, typically housed in an `app-modules` directory.
- The docs show a module containing configuration, database factories/migrations/seeders, Filament page views, routes, source code, models, providers, Filament pages/resources/widgets, and tests.
- The docs show a module `composer.json` requiring `filament/filament` `^5.0`, defining a PSR-4 namespace, and registering a Laravel provider under `extra.laravel.providers`.
- The docs state each module can define a Filament plugin that registers resources, pages, and widgets.
- The docs show module plugin classes implementing `Filament\Contracts\Plugin`, using `getId()`, `make()`, `register(Panel $panel)`, and `boot(Panel $panel)`.
- The docs show `discoverResources()`, `discoverPages()`, and `discoverWidgets()` for module class discovery.
- The docs show module service providers using `Panel::configureUsing()` to register a module plugin only for specific panels or with different plugin options per panel.
- The docs show `$panel->getId()` checks, `match ($panel->getId())`, and `$panel->plugin(...)` for conditional registration.
- The docs show a configurable module plugin storing a boolean option, exposing a fluent setter, reading it with a getter, and registering different plugin instances for `admin` and `staff` panels.
- The docs show registering custom Livewire components used by Filament in the plugin `boot()` method with `Livewire::component(...)`.
- The docs state a Laravel package can distribute an entire panel by providing a class that extends `Filament\PanelProvider` and registering that provider under Composer `extra.laravel.providers`.

## Completion Check
- The answer uses only APIs, folder examples, Composer keys, namespaces, methods, lifecycle details, and code examples confirmed by the current Context7 lookup.
- Every DDD statement is limited to documented self-contained domain modules as Composer packages; unsupported DDD tactical patterns are omitted.
- Module plugin examples keep documented method names, return types, namespace examples, panel calls, and discovery method arguments intact.
- Conditional registration examples are traceable to documented `Panel::configureUsing()`, `$panel->getId()`, `$panel->plugin()`, and `match` or early-return patterns.
- Distributed panel examples are traceable to documented `PanelProvider`, `panel(Panel $panel): Panel`, `id()`, `path()`, `resources()`, `pages()`, `widgets()`, `middleware()`, `authMiddleware()`, and Composer provider registration snippets.
- If the requested modular architecture topic is not confirmed by the retrieved docs, run a narrower Context7 lookup or explicitly leave it out.