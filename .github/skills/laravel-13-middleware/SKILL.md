---
name: laravel-13-middleware
description: 'Use when: working with Laravel 13 middleware, php artisan make:middleware, app/Http/Middleware, middleware handle(), before middleware, after middleware, bootstrap/app.php withMiddleware(), global middleware append(), prepend(), use(), middleware groups, appendToGroup(), group(), web(), api(), middleware aliases, route middleware, withoutMiddleware(), middleware parameters, terminable middleware, middleware priority, controller HasMiddleware, Middleware only/except, and Laravel 13 middleware code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 middleware definition, registration, groups, aliases, parameters, priority, controller middleware, or review task'
---

# Laravel 13 Middleware

## Purpose
Use this skill to create, review, or explain Laravel 13 middleware definitions, registration, assignment, exclusions, parameters, terminable middleware, and middleware priority using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact middleware topic.
2. Do not add middleware commands, generated paths, class namespaces, method signatures, bootstrap APIs, global stack methods, group methods, alias methods, route methods, controller middleware APIs, priority APIs, middleware parameter syntax, terminable behavior, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or class name in a malformed way, do not copy it into final code. Run a narrower lookup or omit the exact import while preserving only confirmed methods and behavior.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented class names, methods, command names, route paths, middleware aliases, group names, and option names.
6. Do not infer behavior from older Laravel versions, Symfony docs, package docs, framework source code, blog posts, community examples, or general Laravel memory.

## Reference Map
- Middleware generation, `app/Http/Middleware`, `handle(...)`, before/after middleware patterns, and request/response imports: [defining-middleware.md](./references/defining-middleware.md)
- Global middleware, `withMiddleware(...)`, `append()`, `prepend()`, `use()`, `web()`, `api()`, `appendToGroup()`, `group()`, aliases, and route alias usage: [registration-groups-aliases.md](./references/registration-groups-aliases.md)
- Route-level middleware, `withoutMiddleware(...)`, controller `HasMiddleware`, resource `middlewareFor(...)`, and `withoutMiddlewareFor(...)`: [route-controller-middleware.md](./references/route-controller-middleware.md)
- Middleware parameters, terminable middleware, singleton registration, middleware priority, and priority-boundary details: [parameters-terminable-priority.md](./references/parameters-terminable-priority.md)

## Workflow
1. Identify the exact surface: middleware generation, middleware class body, before middleware, after middleware, global middleware stack, middleware group, default `web` / `api` group adjustment, alias registration, route assignment, route exclusion, controller-defined middleware, resource-specific middleware, middleware parameters, terminable middleware, singleton terminable middleware, priority order, or middleware review.
2. Query Context7 for that exact Laravel 13 middleware topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, classes, imports, bootstrap methods, route methods, group names, alias names, parameter syntax, and examples.
5. For middleware topics not in the references, such as CSRF exclusion APIs, Sanctum middleware setup, authentication middleware behavior, throttle middleware internals, middleware testing, middleware package registration, request lifecycle details beyond `handle` / `terminate`, or URL-default priority helpers beyond returned snippets, rely on the fresh Context7 lookup or the relevant split skill.
6. For reviews, flag only documented mismatches: wrong generated path, missing `handle(...)`, returning before `$next` when after-middleware behavior is intended, unconfirmed bootstrap method, malformed imports copied from Context7, route middleware exclusion assumptions, parameter syntax errors, retrieving unconfirmed state from terminable middleware, missing singleton registration when same instance state is needed, or priority claims not confirmed by the current lookup.

## Confirmed Core Patterns
- `php artisan make:middleware EnsureTokenIsValid` is documented for generating middleware.
- The docs state generated middleware is created in `app/Http/Middleware`.
- Middleware classes in the returned examples use `App\Http\Middleware`, `Closure`, `Illuminate\Http\Request`, and `Symfony\Component\HttpFoundation\Response`.
- The docs show `handle(Request $request, Closure $next): Response` as the middleware method.
- A before middleware performs work before returning `$next($request)`.
- An after middleware stores `$response = $next($request)`, performs work, and returns `$response`.
- The docs show global middleware configured in `bootstrap/app.php` using `withMiddleware(...)`, including `append(...)`, `prepend(...)`, and `use(...)` concepts.
- The docs show modifying the default `web` and `api` groups with `web(append: [...])`, `api(prepend: [...])`, `web(replace: [...])`, and `web(remove: [...])`.
- The docs show defining custom middleware groups with `appendToGroup('group-name', [...])` and assigning the group to a route with `middleware('group-name')`.
- The docs show manually defining `web` and `api` groups with `group(...)`.
- The docs show middleware aliases configured with `$middleware->alias([...])` and used on routes with `->middleware('subscribed')`.
- The docs show excluding middleware with `withoutMiddleware(...)` on a route or a route group.
- The controller docs show `HasMiddleware`, a static `middleware(): array` method, string middleware, `new Middleware('log', only: ['index'])`, `new Middleware('subscribed', except: ['store'])`, and inline closure middleware.
- The controller docs show resource middleware assignment with `middlewareFor(...)` and resource middleware exclusion with `withoutMiddlewareFor(...)`.
- Middleware parameters are passed after `$next` in `handle(...)`, and route definitions append them with `:`, using comma delimiters for multiple parameters.
- Terminable middleware defines `terminate(Request $request, Response $response): void`, and Laravel automatically invokes it after the response has been sent when the web server uses FastCGI according to the docs.
- The docs show registering terminable middleware as a singleton with `$this->app->singleton(TerminatingMiddleware::class)` when the same instance should be used for `handle` and `terminate`.
- The docs show middleware priority configured in `bootstrap/app.php` with `$middleware->priority([...])`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 middleware topic.
- Every command, generated path, namespace, class, method, bootstrap API, route API, controller API, group name, alias, parameter syntax, priority statement, and terminable behavior statement is traceable to the lookup or references.
- Authentication, authorization, CSRF, rate limiting, Sanctum, URL defaults, and package-specific middleware details are not inferred when the Laravel 13 middleware docs did not confirm them.
- Unconfirmed middleware features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
