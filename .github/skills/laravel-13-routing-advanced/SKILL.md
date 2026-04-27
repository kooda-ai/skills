---
name: laravel-13-routing-advanced
description: 'Use when: working with Laravel 13 advanced routing, Route::redirect(), Route::permanentRedirect(), Route::view(), route:list options, route parameters, optional parameters, where() constraints, whereNumber(), whereUuid(), whereIn(), named routes, redirect()->route(), to_route(), route groups, prefixes, name prefixes, route model binding, withTrashed(), scopeBindings(), withoutScopedBindings(), missing(), Route::model(), Route::bind(), resolveRouteBinding(), fallback routes, route:cache, route:clear, nested resource routes, shallow nesting, scoped resources, and Laravel 13 routing code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 route parameter, model binding, named route, fallback route, route cache, or advanced routing review task'
---

# Laravel 13 Advanced Routing

## Purpose
Use this skill to create, review, or explain Laravel 13 advanced routing behavior such as route parameters, named routes, route model binding, fallback routes, route caching, and advanced resource routing using only details confirmed in the current Laravel 13.x documentation.

## Source Rule
1. Before giving final code, commands, or review findings, query the current Laravel 13.x documentation for the exact advanced routing topic.
2. Do not add route helpers, route cache commands, route group methods, route model binding APIs, resource nesting methods, or middleware-priority behavior unless they appear in the current documentation result or the reference files below.
3. If a requested detail is not confirmed by the current documentation result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, helper names, class names, commands, route parameter names, and example values.
5. Do not infer behavior from older Laravel versions, blog posts, source code, package docs, or general Laravel memory.
6. Keep basic route registration and controller generation in `laravel-13-routing-controllers`; use this slice when the task is specifically about advanced routing behavior, route model binding, or route registration patterns beyond the basic slice.

## Reference Map
- Redirect routes, view routes, `route:list` options, route parameters, constraints, named routes, route groups, fallback routes, and route cache commands: [route-parameters-named-routes.md](./references/route-parameters-named-routes.md)
- Implicit binding, enum binding, custom keys, scoped bindings, missing-model behavior, explicit binding, and model binding overrides: [route-model-binding.md](./references/route-model-binding.md)
- Nested resources, shallow nesting, scoped resources, parameter naming, `withTrashed()`, resource `missing()`, and URL defaults middleware priority: [resource-routing-and-url-defaults.md](./references/resource-routing-and-url-defaults.md)

## Workflow
1. Identify the exact surface: redirect route, view route, `route:list` inspection, route parameter, optional parameter, route constraint, named route, route-group prefixing, route name prefixing, route model binding, enum binding, explicit binding, missing-model customization, fallback route, route caching, nested resource route, shallow nesting, scoped resource route, resource parameter rename, resource soft-delete binding, or URL default parameter middleware.
2. Query the current Laravel 13.x documentation for that exact topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, helpers, methods, classes, route patterns, resource APIs, and examples.
5. For routing topics not in the references, such as route macro APIs, controller action URLs beyond the URL docs, package-specific route registration, domain-specific binding edge cases, route testing helpers, or middleware behavior not shown in the routing and URL docs, rely on the fresh documentation lookup.
6. For reviews, flag only documented mismatches: unsupported route helper, unconfirmed cache command, wrong parameter constraint, unconfirmed binding behavior, missing documented scoping call, unsupported resource route modifier, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The docs show `Route::redirect(...)`, `Route::permanentRedirect(...)`, and `Route::view(...)` for simple routing shortcuts.
- The docs show `php artisan route:list`, `route:list -v`, `route:list -vv`, `route:list --path=api`, `route:list --except-vendor`, and `route:list --only-vendor`.
- Required route parameters, optional parameters, and dependency-injected parameters are documented.
- The docs confirm route constraints with `where(...)`, `Route::pattern(...)`, `whereNumber(...)`, `whereAlpha(...)`, `whereAlphaNumeric(...)`, `whereUuid(...)`, `whereUlid(...)`, and `whereIn(...)`.
- Named routes use `->name(...)`, and the docs show URL generation with `route(...)`, redirects with `redirect()->route(...)`, and `to_route(...)`.
- Route groups can use `middleware(...)`, `controller(...)`, `domain(...)`, `prefix(...)`, and `name(...)` prefixes.
- Implicit route model binding resolves type-hinted Eloquent models when the route segment name matches the variable name.
- The docs show `withTrashed()`, custom keys like `{post:slug}`, `getRouteKeyName()`, `scopeBindings()`, `withoutScopedBindings()`, and `missing(...)` for implicit binding behavior.
- Implicit enum binding is documented for string-backed PHP enums.
- Explicit binding is documented with `Route::model(...)`, `Route::bind(...)`, `resolveRouteBinding(...)`, and `resolveChildRouteBinding(...)`.
- The docs show `Route::fallback(...)` for unmatched requests.
- The docs show `php artisan route:cache` and `php artisan route:clear` for route caching.
- The docs show nested resource routes with dot notation, shallow nesting via `->shallow()`, scoped resources via `->scoped([...])`, and parameter renaming via `->parameters([...])`.
- Resource routes and nested resources can customize missing-model behavior with `->missing(...)`, and resource routes can allow soft-deleted models with `->withTrashed()`.
- The docs show `URL::defaults(...)` in middleware and warn that middleware setting URL defaults should run before `SubstituteBindings` using `prependToPriorityList(...)`.

## Completion Check
- A fresh Laravel 13 documentation lookup was performed for the exact advanced routing topic.
- Every helper, command, route method, binding API, resource route modifier, middleware-priority statement, and example is traceable to the lookup or references.
- Basic controller generation and ordinary route registration remain delegated to `laravel-13-routing-controllers`.
- Unconfirmed advanced routing features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.