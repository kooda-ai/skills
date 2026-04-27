# Core Framework

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x routing, controllers, middleware, initial configuration, and application routing configuration.

## Initial Configuration
The Laravel 13 documentation says Laravel requires minimal configuration out of the box. Configuration files are located in the `config` directory. The docs specifically mention reviewing `config/app.php` for options like `url` and `locale`.

Do not add additional configuration files, config keys, environment variables, cache commands, or deployment configuration unless a fresh Context7 lookup confirms them.

## Application Routing Bootstrap
The docs show default application routing configured in `bootstrap/app.php`:

```php
<?php

use Illuminate\Foundation\Application;

return Application::configure(basePath: dirname(__DIR__))
    ->withRouting(
        web: __DIR__.'/../routes/web.php',
        commands: __DIR__.'/../routes/console.php',
        health: '/up',
    )->create();
```

Confirmed paths and values from this snippet:

- `bootstrap/app.php`
- `routes/web.php`
- `routes/console.php`
- `/up`
- `Illuminate\Foundation\Application`
- `Application::configure(...)`
- `withRouting(...)`
- `create()`

## Basic Routes
The docs show basic routes using closures and controller actions:

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\UserController;

Route::get('/greeting', function () {
    return 'Hello World';
});

Route::get('/user', [UserController::class, 'index']);
```

Confirmed route details:

- Use `Illuminate\Support\Facades\Route` for the documented route examples.
- `Route::get()` is confirmed with a closure route and a controller action route.
- The docs describe routes as typically placed in `routes/web.php` for web requests.

Run a narrower Context7 lookup before using route groups, route names, route parameters, route model binding, redirects, fallback routes, rate limiting, route caching, or route listing commands.

## Controllers
The docs confirm this Artisan command:

```shell
php artisan make:controller UserController
```

The docs say the generated controller class is created in `app/Http/Controllers` by default.

Run a narrower Context7 lookup before using invokable controllers, resource controllers, single action controllers, dependency injection, request validation inside controllers, controller middleware, or controller route generation.

## Middleware
The docs confirm this Artisan command:

```shell
php artisan make:middleware EnsureTokenIsValid
```

The docs say the generated middleware is created in `app/Http/Middleware`.

Run a narrower Context7 lookup before adding middleware registration, aliases, groups, priority, parameters, terminable middleware, exclusion behavior, or route middleware examples.

## Topics Requiring Fresh Lookup
The Context7 snapshot used for this reference did not confirm concrete APIs for requests, responses, Blade, Vite, frontend assets, request lifecycle, service container, service providers, facades beyond the examples above, error handling, logging, or Artisan console internals. Query Context7 for the exact topic before adding those details.
