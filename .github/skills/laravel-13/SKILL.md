---
name: laravel-13
description: 'Use when: working with Laravel 13, Laravel 13.x framework docs, installation, configuration, routing, middleware, controllers, requests, responses, Blade, Vite, service container, service providers, facades, AI-assisted development, Laravel Boost, Laravel MCP, package development, package discovery, database, Eloquent, migrations, seeders, factories, localization, translations, locale, pagination, URL generation, signed URLs, collections, lazy collections, string helpers, security, hashing, encryption, CSRF, rate limiting, search, semantic vector search, validation, authentication, authorization, cache, session, Redis, queues, jobs, events, broadcasting, notifications, mail, filesystem, HTTP client, scheduling, testing, deployment, optimization, upgrades, and Laravel code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 task, exact framework topic, command/API/code to create, explain, or review'
---

# Laravel 13

## Purpose
Use this skill to create, review, or explain Laravel 13 framework code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, architecture guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Laravel 13 topic the user asks about.
2. Do not add commands, file paths, namespaces, classes, methods, helpers, facades, config keys, environment variables, middleware names, route features, Eloquent behavior, validation rules, authentication or authorization behavior, queue settings, test helpers, deployment commands, or upgrade notes unless they appear in the current Context7 result or in the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower Context7 lookup. If it is still not confirmed, explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented class names, facades, method names, command flags, file paths, route strings, and namespaces.
5. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, community examples, or general PHP/Laravel memory unless the Laravel 13.x docs returned by Context7 confirm that behavior.

## Reference Map
- Application setup, initial configuration, routing bootstrap, routes, controllers, and middleware: [core-framework.md](./references/core-framework.md)
- Eloquent models, model generation, factories, seeders, and policy registration: [data-auth-validation.md](./references/data-auth-validation.md)
- Scheduling, queued Artisan commands, HTTP tests, console tests, and facade testing: [async-testing-operations.md](./references/async-testing-operations.md)

## Related Split Skills
- Use `laravel-13-ai-boost-mcp` for AI-assisted development, Laravel Boost, Boost MCP server configuration, custom AI guidelines, Laravel MCP servers, MCP tools/prompts/resources/app resources, MCP metadata, authentication, authorization, and testing boundaries.
- Use `laravel-13-api-resources-serialization` for Eloquent API resources, resource collections, JSON:API resources, model JSON serialization, visibility controls, and appended attributes.
- Use `laravel-13-authentication-account-flows` for starter-kit account scaffolding, manual login/logout, password reset, password confirmation, email verification, verified routes, and end-user authentication account flows.
- Use `laravel-13-installation-starter-kits` for installation, application creation, starter kits, local startup commands, Laravel Sail install boundaries, and confirmed fresh-app structure.
- Use `laravel-13-lifecycle-structure` for request lifecycle, public/index.php and bootstrap/app.php bootstrapping, kernel and middleware flow, provider register/boot order, and documented root/app directory structure.
- Use `laravel-13-configuration-architecture` for configuration, environment files, config caching, service container, dependency injection, service providers, and bindings.
- Use `laravel-13-blade-vite` for Blade views, Blade directives/components, Vite asset loading, `@vite`, and frontend build configuration.
- Use `laravel-13-broadcasting` for event broadcasting, channel authorization, Laravel Echo, Reverb/Pusher setup snippets, broadcast payload naming, and frontend broadcast consumers.
- Use `laravel-13-cache-session-filesystem` for cache access, sessions, flash data, filesystem storage, public disks, storage links, and file URLs.
- Use `laravel-13-collections-strings` for support collections, `collect()`, lazy collections, `LazyCollection`, `cursor()`, `lazy()`, `lazyById()`, `Str::of()`, `str()`, `Stringable`, and string helper boundaries.
- Use `laravel-13-console-scheduling` for Artisan console commands, programmatic Artisan calls, queued Artisan commands, and task scheduling.
- Use `laravel-13-deployment-optimization` for deployment, production debug settings, server configuration, optimization caches, maintenance mode, queue/scheduler deployment, and narrow Laravel 13 upgrade boundaries.
- Use `laravel-13-errors-logging` for exception handling, HTTP error pages, `abort()`, manual exception reporting, logging, log levels, channels, and logging configuration.
- Use `laravel-13-factories-seeders` for model factories, DatabaseSeeder, seeder execution, factory states, factory callbacks, relationship builders, and development or test data generation.
- Use `laravel-13-facades` for facade concepts, facade vs dependency injection, facade vs helper functions, real-time facades, facade root resolution, and facade-specific testing patterns.
- Use `laravel-13-http-client` for outbound HTTP requests, HTTP client response inspection, exceptions, retries, middleware, fakes, and sent-request assertions.
- Use `laravel-13-localization` for locales, language files, translations, placeholders, pluralized translations, pluralizer language, localized resource route verbs, and package translation overrides.
- Use `laravel-13-middleware` for middleware classes, global middleware registration, middleware groups, aliases, route/controller middleware, middleware parameters, terminable middleware, and middleware priority.
- Use `laravel-13-package-development` for package discovery, package service providers, package routes/migrations/config/views/translations/components, package commands, publish tags, public assets, optimize hooks, and reload hooks.
- Use `laravel-13-pagination-urls` for paginator methods, pagination links/views/JSON, URL generation, named route URLs, query URL helpers, signed URLs, and signed URL validation.
- Use `laravel-13-redis` for Redis configuration, PhpRedis client selection, Redis connections, facade commands, pipelines, transactions, Lua scripts, publish/subscribe, and wildcard subscriptions.
- Use `laravel-13-search` for full-text search, full-text indexes, semantic/vector search, PostgreSQL pgvector, vector columns, vector distance queries, and AI SDK embedding boundaries.
- Use `laravel-13-security` for hashing, encryption, CSRF protection, CSRF request headers, named rate limiters, throttle middleware, and manually rate-limited actions.
- Use `laravel-13-routing-advanced` for route parameters, route constraints, named routes, route model binding, fallback routes, route caching, nested resource routing, and URL default parameter middleware.
- Use `laravel-13-routing-controllers` for routing, controllers, resource routes, and controller route registration tasks.
- Use `laravel-13-requests-responses` for HTTP requests, request injection, responses, JSON, views, downloads, redirects, and stream frontend consumption.
- Use `laravel-13-database-migrations-query-builder` for migrations, schema builder, query builder, raw database access, and transactions.
- Use `laravel-13-eloquent-database` for Eloquent models, factories, custom casts, and database-adjacent tasks.
- Use `laravel-13-eloquent-advanced` for local scopes, custom Eloquent collections, advanced casts, observers, model events, and pruning.
- Use `laravel-13-eloquent-relationships` for relationship definitions, eager loading, pivots, polymorphic relationships, through relationships, and one-of-many patterns.
- Use `laravel-13-mail-notifications` for mailables, notifications, mail/notification fakes, queued mail assertions, and queued notifications.
- Use `laravel-13-queues-events` for jobs, queues, workers, failed jobs, events, listeners, subscribers, and broadcasting basics.
- Use `laravel-13-validation-auth` for validation, form requests, authentication helpers, route auth middleware, gates, and policies.
- Use `laravel-13-testing` for Pest, PHPUnit, HTTP, console, facade, exception, and time-sensitive test tasks.

## Workflow
1. Identify the Laravel surface: setup, configuration, request lifecycle, routing, middleware, controller, request/response, Blade, Vite, container, provider, facade, package development, package discovery, database, Eloquent, migration, seeder, factory, localization, translation, locale, pagination, URL generation, signed URL, collection, lazy collection, string helper, support utility, security, hashing, encryption, CSRF, rate limiting, search, validation, authentication, authorization, cache, session, Redis, queue, job, event, broadcast, notification, mail, filesystem, HTTP client, scheduling, console, testing, deployment, optimization, upgrade, or code review.
2. Run a narrow Context7 query for `/websites/laravel_13_x` before producing code, commands, or review findings.
3. Load the closest reference file from the map above.
4. Use the reference files only as a baseline. If the user's exact topic is broader or more specific than the baseline, rely on the fresh Context7 result.
5. For framework code, verify every import, facade, class, method, command, flag, config file, route file, generated path, and example value against the current lookup or the reference files.
6. For package-specific Laravel topics, do not assume the framework docs cover the package. Resolve and query the package's Context7 library when the user asks about package behavior.
7. For reviews, lead with documented mismatches: wrong command, wrong path, wrong namespace, unsupported method, unconfirmed behavior, missing documented registration, or test code that uses helpers not confirmed by the current lookup.
8. Finish by checking that unsupported or unconfirmed details are omitted or clearly called out as not confirmed by the current Laravel 13 documentation context.

## Confirmed Core Patterns
- Context7 resolves Laravel 13 framework docs as `/websites/laravel_13_x`.
- Laravel 13 application routing can be configured in `bootstrap/app.php` with `Application::configure(...)->withRouting(...)` for `web`, `commands`, and `health` routes.
- The docs confirm `routes/web.php`, `routes/console.php`, and the health route `/up` in the default routing configuration snippet.
- The docs confirm basic routes with `Route::get()` using either a closure or a controller action array.
- The docs confirm `php artisan make:controller UserController` and say the controller is created in `app/Http/Controllers` by default.
- The docs confirm `php artisan make:middleware EnsureTokenIsValid` and say middleware is created in `app/Http/Middleware`.
- The docs confirm `php artisan make:model Flight --all` and `php artisan make:model Flight -a` for generating a model plus related classes.
- The docs state Eloquent models are typically stored in `app\Models` and extend `Illuminate\Database\Eloquent\Model`.
- The docs confirm model factories as a way to define default attributes and generate random data for testing and seeding.
- The docs confirm manual policy registration with `Gate::policy(Order::class, OrderPolicy::class)` in the `boot` method of `AppServiceProvider`.
- The docs confirm scheduling Artisan commands with `Schedule::command(...)->daily()`.
- The docs confirm queuing Artisan commands with `Artisan::queue(...)`, including `onConnection()` and `onQueue()` in the returned chain.
- The docs confirm console tests with `expectsQuestion()`, `expectsOutput()`, `doesntExpectOutput()`, and `assertExitCode()`.
- The docs confirm HTTP tests using `actingAs()`, `withSession()`, and request helpers such as `get('/')`.
- The docs confirm facade testing with `Cache::shouldReceive(...)->with(...)->andReturn(...)`.

## Completion Check
- A fresh Context7 lookup for `/websites/laravel_13_x` was performed for the user's exact Laravel 13 topic.
- Every command, method, facade, namespace, class, helper, config key, file path, route path, flag, testing helper, and deployment or upgrade statement is traceable to the current lookup or the reference files.
- Version-specific claims are limited to Laravel 13.x documentation.
- Package-specific claims are not made from framework docs alone.
- Unconfirmed topics are handled by a narrower lookup or are explicitly omitted.
