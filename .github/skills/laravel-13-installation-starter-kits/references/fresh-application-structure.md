# Fresh Application Structure

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x directory structure and fresh application structure details.

## Route Bootstrap
The docs show the default route configuration in `bootstrap/app.php`:

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

Confirmed paths and values: `bootstrap/app.php`, `routes/web.php`, `routes/console.php`, and health route `/up`.

## The Bootstrap Directory
The docs state the `bootstrap` directory contains the `app.php` file, which initializes the framework.

The docs also state the `bootstrap` directory contains a `cache` folder for framework-generated files such as route and service caches.

## The Storage Directory
The docs state the `storage` directory contains logs, compiled Blade templates, file-based sessions, file caches, and other framework-generated files.

The docs state the `storage` directory is split into `app`, `framework`, and `logs` directories.

The docs state `storage/app/public` is used for user-generated files that must be publicly accessible.

The docs state public access for `storage/app/public` requires a symbolic link created with:

```shell
php artisan storage:link
```

## The Providers Directory
The docs state the `Providers` directory contains service providers for the application.

The docs state service providers bootstrap the application by binding services in the service container, registering events, or performing other tasks to prepare the application for incoming requests.

The docs state a fresh Laravel application already contains `AppServiceProvider` in this directory.

## Topics Requiring Fresh Lookup
Run a new Context7 query before describing unconfirmed directories such as `app`, `app/Http`, `app/Models`, `config`, `database`, `public`, `resources`, `routes`, `tests`, `vendor`, or any generated file not listed in this reference.
