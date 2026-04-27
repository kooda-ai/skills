---
name: laravel-13-blade-vite
description: 'Use when: working with Laravel 13 Blade views, resources/views, .blade.php files, view(), passing data to views, Blade echo syntax, escaped output, Blade directives, @if, @foreach, @forelse, @switch, form state directives, @props, Blade components, x-alert style components, Vite, @vite, resources/css/app.css, resources/js/app.js, vite.config.js, laravel-vite-plugin, HMR, npm run build, and Laravel 13 Blade/Vite code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 Blade view/component/directive, Vite asset, @vite, frontend build, or review task'
---

# Laravel 13 Blade And Vite

## Purpose
Use this skill to create, review, or explain Laravel 13 Blade views, Blade directives/components, and Vite asset integration using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Blade, view, component, directive, Vite, or frontend asset topic.
2. Do not add Blade directives, component commands, component class APIs, view paths, helper behavior, escaping behavior, Vite commands, package names, config options, JavaScript framework setup, HMR behavior, aliases, environment variables, or build behavior unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented directives, file paths, package names, commands, config keys, and method names.
5. Do not infer behavior from older Laravel versions, Vite docs, frontend framework docs, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Returning views, `resources/views/*.blade.php`, `view()`, passing data, `with()`, and Blade echo syntax: [blade-views-templates.md](./references/blade-views-templates.md)
- Blade directives, loops, switch statements, form element state directives, `@props`, component attributes, and `<x-alert>` style usage: [blade-directives-components.md](./references/blade-directives-components.md)
- Vite default integration, `@vite`, `resources/css/app.css`, `resources/js/app.js`, `vite.config.js`, `laravel-vite-plugin`, HMR, production builds, and plugin options: [vite-assets.md](./references/vite-assets.md)

## Workflow
1. Identify the exact surface: returning a view, passing view data, Blade echoing, directive syntax, loop, switch, form attribute directive, Blade component props, component attributes, Vite asset loading, Vite config, HMR, production build, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented helpers, directives, component syntax, package names, commands, file paths, config options, and examples.
5. For Blade topics not in the references, such as layouts, sections, stacks, includes, anonymous/class-based component generation, slots, attribute bags beyond the shown merge, `@csrf`, `@method`, auth directives, environment directives, raw output, comments, JavaScript rendering, or custom directives, rely on the fresh Context7 lookup.
6. For Vite topics not in the references, such as installing dependencies, `npm run dev`, React/Vue plugin setup, asset aliases, environment variables, SSR, CSP nonces, integrity hashes, preloading, or testing Vite, rely on the fresh Context7 lookup.
7. For reviews, flag only documented mismatches: wrong view path, unconfirmed directive, unconfirmed component API, wrong Vite entry path, unsupported plugin option, unconfirmed package name, or build behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Standard Blade templates are stored under `resources/views` and may use the `.blade.php` extension, as shown by `resources/views/greeting.blade.php`.
- `return view('greeting', ['name' => 'Finn'])` and `return view('greeting', ['name' => 'James'])` are documented patterns for returning views with data.
- View data can also be passed with chained `with(...)` calls.
- Blade double curly braces such as `{{ $name }}` display data and automatically encode HTML entities to help prevent XSS attacks.
- Any valid PHP expression may be placed within Blade echo braces according to the docs.
- The docs confirm loop directives `@for`, `@foreach`, `@forelse`, `@empty`, `@endforelse`, and `@while`.
- The docs confirm switch directives `@switch`, `@case`, `@break`, `@default`, and `@endswitch`.
- The docs confirm form element state directives `@checked`, `@selected`, `@disabled`, `@readonly`, and `@required`.
- The docs describe Blade conditional directives such as `@if`, `@elseif`, `@else`, `@endif`, `@unless`, `@isset`, and `@empty`.
- Component templates can use `@props(...)`, `$attributes->merge(...)`, and `<x-alert ... />` style invocation in the returned docs.
- Laravel uses Vite by default to bundle CSS and JavaScript assets.
- Every new Laravel application includes `vite.config.js` configured with the Laravel Vite plugin according to the docs.
- `@vite(['resources/css/app.css', 'resources/js/app.js'])` is documented for loading compiled scripts and styles in the root template.
- `@vite('resources/js/app.js')` is documented when CSS is imported through JavaScript.
- The docs state `@vite` automatically injects the Vite client for HMR in development and loads versioned assets in production.
- `npm run build` is documented for versioning and bundling assets for production deployment.
- The docs show `laravel({ hotFile, buildDirectory, input })` and `build.manifest` options in `vite.config.js`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Blade, view, component, directive, Vite, or frontend asset topic.
- Every helper, directive, path, package, command, config option, and behavior is traceable to the lookup or references.
- Frontend framework and Vite details are not inferred from non-Laravel docs unless the relevant package docs are separately queried.
- Unconfirmed Blade/Vite features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
