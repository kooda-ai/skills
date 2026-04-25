---
name: livewire-4-pages
description: 'Use when: working with Livewire 4 Pages, page components, full-page components, Route::livewire(), pages:: components, livewire:layout, layouts::app, #[Layout], layout(), #[Title], title(), route parameters, route model binding, named layout slots, wire:navigate, redirects to page components, #[Url] query strings, component namespaces, and page routing troubleshooting. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 page component task, page route/layout/title/navigation/URL-state concern'
---

# Livewire 4 Pages

## Purpose
Use this skill to create, review, or explain Livewire 4 page components using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 Pages topic.
2. Do not add page routes, commands, paths, namespaces, component formats, attributes, methods, directives, configuration keys, JavaScript hooks, redirect helpers, URL-query behavior, caveats, or troubleshooting advice unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented command flags, namespaces, attributes, directive names, method names, parameter names, configuration keys, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controller habits, Alpine patterns, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Page component creation, routing, layouts, titles, named slots, route parameters, and model binding: [page-routing-layouts.md](./references/page-routing-layouts.md)
- `wire:navigate`, redirects, persisted elements, active links, JavaScript navigation hooks, script evaluation, progress bar settings, and URL query parameters: [navigation-url-redirects.md](./references/navigation-url-redirects.md)
- Page component formats, namespaced component organization, programmatic registration, stubs, and troubleshooting: [organization-troubleshooting.md](./references/organization-troubleshooting.md)

## Workflow
1. Identify the page concern: page component creation, route registration, layout selection, title handling, named layout slot, route parameter, route model binding, SPA navigation, redirect, URL query state, component namespace, component discovery, or troubleshooting.
2. Run a narrow Context7 query for the exact Livewire 4 Pages topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For a new page component, confirm the documented component format and use the `pages::` namespace when the component belongs in `resources/views/pages/`.
5. For routing, use documented `Route::livewire()` examples and preserve component aliases such as `pages::post.create`.
6. For layouts, confirm whether the task needs the default `layouts::app`, `php artisan livewire:layout`, `component_layout`, `#[Layout]`, or `->layout()`.
7. For titles, confirm that the layout exposes a dynamic title and then choose documented `#[Title]` or `->title()` usage.
8. For route data, match documented route parameter names to `mount()` parameters, or use documented route model binding with a `mount(Post $post)` parameter or matching public `Post $post` property.
9. For navigation, confirm whether the task needs `wire:navigate`, `.hover` prefetching, `data-current`, `wire:current`, `@persist`, `wire:navigate:scroll`, navigation JavaScript hooks, or navigation progress bar settings.
10. For redirects, use documented Livewire redirect helpers and add `navigate: true` only when the docs confirm SPA navigation should be used for the redirect.
11. For shareable page state, confirm documented `#[Url]`, nullable properties, `as`, `except`, `keep`, `history`, `queryString()`, or trait query string hooks.
12. Finish by checking that every class, method, attribute, command, flag, directive, modifier, configuration key, path, namespace, and caveat in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Livewire components can be assigned directly to routes and rendered as complete pages with `Route::livewire('/posts/create', 'pages::post.create')`.
- `php artisan make:livewire pages::post.create` creates a page component at `resources/views/pages/post/⚡create.blade.php`.
- By default, `pages::` points to `resources/views/pages/` and `layouts::` points to `resources/views/layouts/`.
- Page components work like regular components, but are rendered as full pages with access to custom layouts, page titles, route parameters and model binding, and named slots for layouts.
- Components rendered via routes use `layouts::app` at `resources/views/layouts/app.blade.php` unless the default layout is changed or the component specifies another layout.
- Page titles require a layout title slot such as `{{ $title ?? config('app.name') }}` and can be set with `#[Title]` or `->title()`.
- Route parameters are passed to matching `mount()` parameters, and Laravel route model binding works with a type-hinted `mount()` parameter or a matching public model property.
- `wire:navigate` intercepts links, requests the next page in the background, and replaces the current page URL, `<title>`, and `<body>` with the new page.
- Livewire redirects can target full-page components by path, and `redirect(..., navigate: true)` uses Livewire navigation for the redirect.
- `#[Url]` syncs component properties with the browser query string so page state can survive refreshes and be shared.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Pages topic.
- The answer does not include APIs, configuration, behavior, or caveats absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 paths, namespaces, route examples, command flags, directive names, attributes, method signatures, and configuration keys.
- Page layout guidance includes the required `{{ $slot }}` placeholder when discussing layout files.
- Navigation guidance accounts for documented `wire:navigate` behavior, active-link handling, persisted elements, scripts, and progress bar settings only when relevant.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.