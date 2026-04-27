---
name: laravel-13-lifecycle-structure
description: 'Use when: working with Laravel 13 request lifecycle, public/index.php, bootstrap/app.php bootstrapping, handleRequest(), handleCommand(), HTTP kernel bootstrappers, middleware flow, service provider register and boot order, directory structure, root directories, app directory subdirectories, and Laravel 13 architecture or structure code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 request lifecycle, bootstrapping, directory structure, app directory layout, or structure review task'
---

# Laravel 13 Lifecycle And Structure

## Purpose
Use this skill to create, review, or explain Laravel 13 request lifecycle and documented application directory structure using only details confirmed in the current Laravel 13.x documentation.

## Source Rule
1. Before giving final code, commands, architecture guidance, or review findings, query the current Laravel 13.x documentation for the exact lifecycle or structure topic.
2. Do not add bootstrapping flow details, entry-point behavior, kernel behavior, provider-order statements, directory descriptions, generated-directory claims, or command examples unless they appear in the current documentation result or the reference files below.
3. If a requested detail is not confirmed by the current documentation result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples and descriptions close to documented snippets and preserve documented file paths, method names, class names, directory names, and commands.
5. Do not infer behavior from older Laravel versions, framework source, package docs, blog posts, or general Laravel memory.
6. Use feature-specific split skills for the underlying APIs inside these directories, such as routing, middleware, providers, events, jobs, mail, notifications, policies, validation rules, broadcasting, queues, or testing. Use this slice when the task is specifically about lifecycle flow or application structure.

## Reference Map
- Request entry point, `public/index.php`, `bootstrap/app.php`, kernels, bootstrappers, middleware flow, providers, routing dispatch, and response send flow: [request-lifecycle.md](./references/request-lifecycle.md)
- Root directory descriptions for `app`, `bootstrap`, `config`, `database`, `public`, `resources`, `routes`, `storage`, `tests`, and `vendor`: [root-directory.md](./references/root-directory.md)
- `app` directory descriptions for generated subdirectories such as `Broadcasting`, `Console`, `Events`, `Exceptions`, `Http`, `Jobs`, `Listeners`, `Mail`, `Models`, `Notifications`, `Policies`, `Providers`, and `Rules`: [app-directory.md](./references/app-directory.md)

## Workflow
1. Identify the exact surface: request entry point, application bootstrapping, HTTP or console kernel, middleware traversal, provider registration order, router handoff, response send flow, root directory description, app subdirectory description, generated-directory behavior, or lifecycle/structure review.
2. Query the current Laravel 13.x documentation for that exact topic.
3. Load the relevant reference file from the map above.
4. Use only documented file paths, class names, method names, directory names, and commands.
5. Route feature-specific implementation questions to the owning split skill when the real task is about routing, middleware, service providers, queues, events, mail, notifications, policies, validation, or testing rather than lifecycle or structure itself.
6. For reviews, flag only documented mismatches: wrong entry-point path, unconfirmed kernel behavior, unsupported provider-order claim, wrong directory purpose, unsupported generated-directory statement, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The request lifecycle docs identify `public/index.php` as the entry point for all requests to a Laravel application.
- The docs state `public/index.php` loads Composer's autoloader and retrieves the application instance from `bootstrap/app.php`.
- The docs state incoming requests are sent to the HTTP or console kernel through `handleRequest()` or `handleCommand()` on the application instance.
- The docs describe the HTTP kernel as an instance of `Illuminate\Foundation\Http\Kernel`.
- The docs state the HTTP kernel runs bootstrappers before the request is executed and passes the request through the middleware stack.
- The docs state service providers are instantiated, then all `register()` methods run, then all `boot()` methods run.
- The docs state the request is handed to the router after the application has been bootstrapped and providers have been registered.
- The docs state the response returns outward through middleware and is finally sent to the browser by the response `send()` method.
- The structure docs state the default Laravel application structure is only a starting point and Laravel imposes almost no restrictions on where classes are located as long as Composer can autoload them.
- The docs describe the root directories `app`, `bootstrap`, `config`, `database`, `public`, `resources`, `routes`, `storage`, `tests`, and `vendor`.
- The docs describe generated `app` subdirectories such as `Broadcasting`, `Events`, `Jobs`, `Listeners`, `Mail`, `Notifications`, `Policies`, and `Rules` as directories that may not exist until their make commands are used.
- The docs say `php artisan list make` can be used to review available make commands.

## Completion Check
- A fresh Laravel 13 documentation lookup was performed for the exact lifecycle or structure topic.
- Every lifecycle statement, file path, method name, directory description, and generation claim is traceable to the lookup or references.
- Feature-specific APIs remain delegated to their owning split skills.
- Unconfirmed lifecycle or structure behavior is omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.