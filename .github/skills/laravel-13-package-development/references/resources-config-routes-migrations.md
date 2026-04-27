# Package Resources, Configuration, Routes, And Migrations

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x package routes, migrations, configuration publishing, and configuration merging.

## Routes
The docs show loading package routes from a service provider `boot()` method:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadRoutesFrom(__DIR__.'/../routes/web.php');
}
```

The docs state `loadRoutesFrom(...)` automatically handles route caching and does not load routes if they are already cached.

## Migrations
The docs show publishing package migrations from a service provider `boot()` method:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->publishesMigrations([
        __DIR__.'/../database/migrations' => database_path('migrations'),
    ]);
}
```

The docs state `publishesMigrations(...)` informs Laravel about the package migration location.

The docs state Laravel automatically updates migration filenames with the current date and time when they are published.

## Configuration Publishing
The docs show publishing a package configuration file from a service provider `boot()` method:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->publishes([
        __DIR__.'/../config/courier.php' => config_path('courier.php'),
    ]);
}
```

The docs state users can override default configuration options after publishing. The returned docs mention accessing the published configuration with `config('courier.option')`.

## Configuration Merging
The docs show merging a package configuration file with the application's published copy in the service provider `register()` method:

```php
/**
 * Register any package services.
 */
public function register(): void
{
    $this->mergeConfigFrom(
        __DIR__.'/../config/courier.php',
        'courier'
    );
}
```

The docs state `mergeConfigFrom(...)` allows users to override only specific options.

The docs state this method only merges the first level of the configuration array.

## Tagged Resource Publishing
The docs show tagged package assets, configuration, and migrations:

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

Confirmed methods and helpers: `publishes(...)`, `publishesMigrations(...)`, `public_path(...)`, `config_path(...)`, and `database_path(...)`.

Confirmed tags: `public`, `courier-config`, and `courier-migrations`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using package route middleware groups, route names, package route caching details beyond the returned statement, migration publishing command names beyond `vendor:publish`, migration stub naming rules, configuration file contents, nested config merge behavior beyond the first-level warning, or package resource paths not shown here.
