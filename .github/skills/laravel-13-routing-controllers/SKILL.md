---
name: laravel-13-routing-controllers
description: 'Use when: working with Laravel 13 routing, routes/web.php, routes/api.php, Route::get(), Route::controller(), controllers, make:controller, resource controllers, Route::resource(), resource route actions, resource route names, Route::singleton(), middleware(), middlewareFor(), controller routing, and Laravel 13 routing/controller code reviews. Use laravel-13-routing-advanced for route parameters, named routes, model binding, fallback routes, route caching, and advanced resource routing. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 route/controller task, route definition, resource route, middleware assignment, or code review'
---

# Laravel 13 Routing And Controllers

## Purpose
Use this skill to create, review, or explain Laravel 13 basic routing and controller code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact routing or controller topic.
2. Do not add route methods, route file paths, middleware APIs, controller commands, controller methods, route names, generated paths, flags, or registration behavior unless they appear in the current Context7 result or [routing-controllers.md](./references/routing-controllers.md).
3. If a Context7 result renders a namespace or import in a malformed way, run a narrower lookup before using that import in code.
4. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Basic routes, application routing bootstrap, controllers, middleware generation, resource routes, controller groups, and resource middleware: [routing-controllers.md](./references/routing-controllers.md)

## Workflow
1. Identify the exact surface: basic route, application route bootstrap, route file, controller action, generated controller, resource controller, resource route table, controller route group, middleware on resource routes, method-specific resource middleware, singleton resource, or route review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load [routing-controllers.md](./references/routing-controllers.md).
4. Use only documented route declarations, commands, methods, route names, route paths, and middleware APIs.
5. Route route-parameter, named-route, model-binding, fallback-route, route-cache, and advanced resource-routing tasks to `laravel-13-routing-advanced`.
6. For features not in the reference, such as API route registration beyond the documented mentions or controller dependency injection, rely on the fresh Context7 lookup before adding code.
7. For reviews, flag only documented mismatches: unsupported method, wrong command or flag, wrong generated path, unconfirmed middleware API, unconfirmed route name, or unconfirmed route file.

## Confirmed Core Patterns
- `bootstrap/app.php` can configure `web`, `commands`, and `health` routing through `Application::configure(...)->withRouting(...)->create()`.
- `routes/web.php`, `routes/console.php`, and `/up` appear in the documented routing bootstrap snippet.
- Basic routes can use `Route::get()` with a closure or a controller action array.
- `php artisan make:controller UserController` creates a controller in `app/Http/Controllers` by default.
- `php artisan make:middleware EnsureTokenIsValid` creates middleware in `app/Http/Middleware`.
- `php artisan make:controller PhotoController --resource` generates a controller at `app/Http/Controllers/PhotoController.php` with methods for resource operations.
- `Route::resource('photos', PhotoController::class)` registers resource routes for the documented resource controller actions.
- The docs confirm the resource action names `index`, `create`, `store`, `show`, `edit`, `update`, and `destroy`.
- The docs confirm resource route names like `photos.index`, `photos.create`, `photos.store`, `photos.show`, `photos.edit`, `photos.update`, and `photos.destroy`.
- `Route::controller(OrderController::class)->group(...)` groups routes by controller.
- Resource routes can call `middleware([...])` or `middleware('auth')`.
- Resource, API resource, and singleton routes can call `middlewareFor(...)` for specific methods.
- Use `laravel-13-routing-advanced` when the task needs route parameters, named routes, route model binding, fallback routes, route cache commands, or nested and scoped resource-routing behavior.

## Completion Check
- A fresh Context7 lookup was performed for the exact routing/controller topic.
- Every basic route method, controller command, flag, generated path, middleware method, resource route name, and route URI is traceable to the lookup or reference.
- Advanced routing features are delegated to `laravel-13-routing-advanced`.
- Unconfirmed route and controller features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
