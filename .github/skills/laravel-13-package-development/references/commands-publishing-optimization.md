# Package Commands, Publishing, And Optimization Hooks

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x package commands, publishing, public assets, optimize commands, and reload commands.

## Package Artisan Commands
The docs show registering package Artisan commands inside a service provider `boot()` method when running in the console:

```php
use Courier\Console\Commands\InstallCommand;
use Courier\Console\Commands\NetworkCommand;

/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    if ($this->app->runningInConsole()) {
        $this->commands([
            InstallCommand::class,
            NetworkCommand::class,
        ]);
    }
}
```

Confirmed methods and classes from this snippet: `$this->app->runningInConsole()`, `$this->commands([...])`, `InstallCommand::class`, and `NetworkCommand::class`.

## Publishing File Groups
The docs state packages can tag different groups of publishable assets and resources, such as configuration files or migrations, to give users more control during publishing.

The docs show public assets, configuration, and migrations being registered with tags:

```php
public function boot(): void
{
    $this->publishes([
        __DIR__.'/../public' => public_path('vendor/courier'),
    ], 'public');

    $this->publishes([
        __DIR__.'/../config/package.php' => config_path('package.php')
    ], 'courier-config');

    $this->publishesMigrations([
        __DIR__.'/../database/migrations/' => database_path('migrations')
    ], 'courier-migrations');
}
```

The docs state packages often include JavaScript, CSS, and images that need to be made available to the host application and can be copied into the application's public directory with `publishes(...)`.

## Running Vendor Publish
The docs show publishing package files with Artisan:

```shell
php artisan vendor:publish --tag=public --force
php artisan vendor:publish --tag=courier-config
php artisan vendor:publish --provider="Your\Package\ServiceProvider"
```

The docs state the `--tag` option can target specific publish groups and the `--provider` flag can publish all files associated with a package service provider.

The docs state the `--force` flag can overwrite existing public assets when a package is updated.

## Optimize And Reload Hooks
The docs show package optimize and reload commands registered inside a console guard:

```php
public function boot(): void
{
    if ($this->app->runningInConsole()) {
        $this->optimizes(
            optimize: 'package:optimize',
            clear: 'package:clear-optimizations',
        );
        $this->reloads('package:reload');
    }
}
```

The package docs state Laravel provides an `optimize` command that caches application configuration, events, routes, and views.

The package docs state `optimizes(...)` can register package commands that are invoked automatically when `optimize` or `optimize:clear` are executed.

The returned docs describe `reloads(...)` as registering a custom command for Laravel service reload processes.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using package command generation, command signatures, package install command conventions, publish tag naming conventions beyond examples, asset compilation, package Vite integration, reload command execution details, optimize command ordering, package cache file paths, or deployment workflow beyond the documented optimize hook.
