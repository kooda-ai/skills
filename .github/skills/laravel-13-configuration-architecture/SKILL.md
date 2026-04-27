---
name: laravel-13-configuration-architecture
description: 'Use when: working with Laravel 13 configuration, config directory, config/app.php, .env, .env.example, env(), config:cache, config:clear, bootstrap/app.php, withRouting(), service container, dependency injection, zero configuration resolution, constructor injection, method injection, contextual binding, service providers, bootstrap/providers.php, make:provider, register(), boot(), bind(), bindIf(), singleton(), App facade binding, and Laravel 13 architecture code reviews. Use laravel-13-lifecycle-structure for request lifecycle and directory structure, and laravel-13-facades for full facade behavior, real-time facades, and facade-specific testing patterns. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 config, env, lifecycle, service container, provider, binding, DI, facade, or architecture review task'
---

# Laravel 13 Configuration And Architecture

## Purpose
Use this skill to create, review, or explain Laravel 13 configuration, environment setup, service container usage, dependency injection, service providers, and architecture concepts using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, architecture guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact configuration, container, provider, or architecture topic.
2. Do not add installation commands, config keys, environment variable behavior, cache commands, lifecycle details, container methods, provider registration rules, generated paths, or binding patterns unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented file names, commands, helper names, class names, imports, method names, and binding chains.
5. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Initial configuration, `config`, `config/app.php`, `.env`, `.env.example`, `env()`, `config:cache`, `config:clear`, and `bootstrap/app.php` routing: [configuration-environment.md](./references/configuration-environment.md)
- Service container zero configuration resolution, controller constructor/method injection, route request injection, and contextual binding: [container-dependency-injection.md](./references/container-dependency-injection.md)
- Service providers, `bootstrap/providers.php`, `make:provider`, `register()`, `boot()`, `singleton()`, `bind()`, `bindIf()`, and `App::bind()`: [service-providers-bindings.md](./references/service-providers-bindings.md)

## Workflow
1. Identify the exact surface: initial configuration, environment file, config helper, config cache command, application bootstrap routing, zero configuration resolution, constructor injection, method injection, route injection, contextual binding, service provider generation, provider registration, container binding, singleton binding, or architecture/code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, file paths, helpers, methods, imports, service provider rules, container APIs, and examples.
5. For installation or project creation commands, rely on a fresh lookup because the current reference does not confirm exact project creation commands.
6. Route full facade behavior, real-time facades, and facade-specific testing patterns to `laravel-13-facades`.
7. Route request lifecycle and directory structure tasks to `laravel-13-lifecycle-structure`.
8. For bootstrapping beyond `bootstrap/app.php` routing, config publishing, maintenance mode, or deployment optimization, rely on the fresh Context7 lookup before adding details.
9. For reviews, flag only documented mismatches: unsupported config command, unconfirmed file path, unconfirmed `env()` usage, wrong provider registration file, binding non-container work in `register()`, or unconfirmed container method.

## Confirmed Core Patterns
- Laravel requires minimal configuration out of the box.
- Configuration files are located in the `config` directory.
- The docs recommend reviewing `config/app.php` options like `url` and `locale`.
- Laravel uses DotEnv for environment configuration; a fresh installation root contains `.env`, populated from `.env.example`.
- Teams should update `.env.example` with placeholder values for required environment variables.
- The `env()` function can read environment variables and accept a default value, as in `(bool) env('APP_DEBUG', false)`.
- `php artisan config:cache` and `php artisan config:clear` are documented for configuration caching and clearing.
- `bootstrap/app.php` can configure application routes with `Application::configure(...)->withRouting(...)->create()`.
- The service container can resolve classes with no dependencies or only concrete class dependencies without configuration.
- Controllers, event listeners, middleware, and queued job `handle` methods are documented as places where dependencies may be automatically injected.
- Controller constructor injection and method injection are documented.
- Route closures may type-hint `Illuminate\Http\Request`, and the container injects the current request.
- Contextual binding is documented with `$this->app->when(...)->needs(...)->give(...)`.
- Service providers are registered in `bootstrap/providers.php`.
- `php artisan make:provider RiakServiceProvider` generates a service provider and automatically registers it in `bootstrap/providers.php`.
- Service providers extend `Illuminate\Support\ServiceProvider`, and most contain `register()` and `boot()` methods.
- The docs state the `register()` method should only bind things into the service container and should not register event listeners, routes, or other functionality.
- The docs show `$this->app->singleton(...)`, `$this->app->bind(...)`, `$this->app->bindIf(...)`, and `App::bind(...)` container binding examples.
- Use `laravel-13-lifecycle-structure` when the task is about request entry points, kernel flow, provider boot order, or documented directory structure rather than configuration or container APIs.
- Use `laravel-13-facades` when the task is about facade concepts, real-time facades, helper equivalence, or facade testing patterns rather than container binding itself.

## Completion Check
- A fresh Context7 lookup was performed for the exact configuration, architecture, container, provider, or binding topic.
- Every command, file path, helper, class, import, method, config behavior, provider rule, and binding chain is traceable to the lookup or references.
- Request lifecycle and directory structure topics are delegated to `laravel-13-lifecycle-structure`.
- Facade-specific concepts are delegated to `laravel-13-facades`.
- Installation, lifecycle, and deployment details are not inferred when the current lookup did not confirm them.
- Unconfirmed architecture features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
