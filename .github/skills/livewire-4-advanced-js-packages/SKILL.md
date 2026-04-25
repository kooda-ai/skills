---
name: livewire-4-advanced-js-packages
description: 'Use when: working with Livewire 4 JavaScript and package-facing development, Alpine $wire, @script, @assets, @livewireScriptConfig, Livewire.start(), Livewire.hook, $wire APIs, component JavaScript files, component CSS files, Livewire::addComponent, addLocation, addNamespace, stubs, reusable component registration, and package development boundaries. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 JavaScript, Alpine, hooks, assets, manual bundling, reusable component registration, or package-facing development concern'
---

# Livewire 4 Advanced JavaScript Packages

## Purpose
Use this skill to create, review, or explain Livewire 4 JavaScript integration and package-facing reusable component development using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact JavaScript, Alpine, `$wire`, `@script`, `@assets`, manual bundling, hook, component registration, namespace, location, stub, or package development topic.
2. Do not add JavaScript APIs, Alpine behavior, script loading rules, asset-publishing behavior, package skeletons, Composer metadata, service-provider lifecycle claims, registration APIs, stubs, or testing guidance unless they appear in the retrieved documentation.
3. If a package-development detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm a dedicated Livewire 4 package-development rule and constrain guidance to documented reusable component primitives.
4. Preserve documented directive names, method names, import paths, component registration parameter names, command names, file names, and option names exactly.
5. Do not infer behavior from Livewire 3 package docs, Laravel package habits, Vite package habits, Alpine docs outside Livewire, package source code, or memory.

## Covered Topics
- Alpine integration and `$wire`
- `$wire` property, method, event, upload, island, hook, and interceptor APIs
- JavaScript actions with `$js()` and `$wire.$js`
- Component scripts, `@script`, and `@assets`
- Manual Alpine and Livewire bundling with `@livewireScriptConfig`
- `Livewire.hook(...)`
- Multi-file component JavaScript and CSS files
- Component namespaces and component locations
- Programmatic component registration
- Component stubs and make-command options
- Package development boundaries when dedicated docs are not confirmed

## Workflow
1. Identify the concern: Alpine interop, `$wire` property access, action call, JavaScript action, event API, upload API, hook, component script, shared asset, manual bundle, generated JavaScript or CSS file, namespace, registration, stubs, reusable component distribution, or package-development request.
2. Run a narrow Context7 query for the exact Livewire 4 JavaScript or package-facing topic before producing code or review findings.
3. For Alpine, use `$wire` only inside documented Livewire component contexts and only for documented property access, mutation, action calls, refreshes, events, uploads, hooks, islands, or interceptors.
4. For `$wire` property mutation, distinguish documented immediate client-side mutation from network-triggering `$wire.$set(name, value, live = true)` behavior only when confirmed.
5. For JavaScript actions, define `$js()` in a component `<script>` tag, call it from Blade with `wire:click="$js.name"`, call it from Alpine with `$wire.$js.name()`, or call it from PHP with `$this->js('name')` only as documented.
6. For class-based component JavaScript, wrap component scripts with `@script ... @endscript` when the docs require component scoping.
7. For shared assets loaded with a component, use `@assets ... @endassets` only as documented, including the docs-confirmed rule that assets load before component scripts and only once per page.
8. For manual bundling, require `@livewireScriptConfig`, import `Livewire` and `Alpine` from `../../vendor/livewire/livewire/dist/livewire.esm`, register directives or plugins, and call `Livewire.start()` only as documented.
9. For JavaScript hooks, use documented `Livewire.hook(...)` names and parameters only.
10. For multi-file components, use generated JavaScript or CSS files only when the `make:livewire` options and file names are confirmed by the docs.
11. For reusable component organization, use documented `component_namespaces`, `component_locations`, `Livewire::addComponent(...)`, `Livewire::addLocation(...)`, and `Livewire::addNamespace(...)` patterns only.
12. For class-based reusable components, use documented `class`, `classNamespace`, `classPath`, and `classViewPath` registration parameters only when confirmed.
13. For stubs, use `php artisan livewire:stubs` and documented stub file names only.
14. For package development, do not invent a package skeleton, publish command, Composer `extra`, asset pipeline, config merge, or testing setup unless a fresh Context7 lookup confirms a Livewire 4 package-development page or rule.
15. Finish by checking that every JavaScript API, directive, import path, registration method, parameter name, command, file name, and package-development claim is traceable to the current Context7 result.

## Confirmed Core Patterns
- Livewire exposes `$wire` inside Alpine expressions in a Livewire component.
- `$wire` can access or mutate public properties, call public component methods, refresh the component, dispatch events, listen for events, upload files, scope island actions, and register hooks or interceptors when those APIs are confirmed by the docs.
- JavaScript actions run on the client side without a server request.
- Class-based component scripts require `@script` and `@endscript` so Livewire can scope and time script execution correctly.
- `@assets` loads component script or stylesheet assets before component scripts and loads those assets only once per page.
- Manual bundling uses `@livewireScriptConfig`, imports `Livewire` and `Alpine` from `../../vendor/livewire/livewire/dist/livewire.esm`, and calls `Livewire.start()`.
- Programmatic registration is documented with `Livewire::addComponent(...)`, `Livewire::addLocation(...)`, and `Livewire::addNamespace(...)`.
- Additional component namespaces can be configured in `config/livewire.php` under `component_namespaces`.
- Additional component discovery directories can be configured in `config/livewire.php` under `component_locations`.
- `php artisan livewire:stubs` publishes customizable component stubs.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact JavaScript or package-facing topic.
- No JavaScript API, Alpine behavior, script loading rule, asset behavior, registration API, namespace behavior, stub name, package skeleton, Composer rule, or testing claim absent from the retrieved Livewire 4.x docs was added.
- Examples preserve documented directive names, method names, import paths, registration parameter names, command names, and file names.
- Package-development answers explicitly stay within documented Livewire 4 reusable component primitives when a dedicated package-development page is not confirmed.
- Unconfirmed package-development details are explicitly left out or followed by a narrower Context7 lookup.
