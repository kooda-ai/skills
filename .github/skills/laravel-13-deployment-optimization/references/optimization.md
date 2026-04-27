# Optimization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x deployment optimization and cache commands.

## Optimize Command
The deployment docs state Laravel can cache configuration, events, routes, and views to improve production performance.

The docs show:

```shell
php artisan optimize
```

The deployment docs state the `optimize` command performs these caching tasks at once and should be integrated into the deployment workflow.

## Clearing Optimized Caches
The deployment docs show:

```shell
php artisan optimize:clear
```

The docs describe this as clearing optimized caches when necessary.

## Configuration Cache
The configuration docs show:

```shell
php artisan config:cache
php artisan config:clear
```

The docs describe these as commands to cache configuration files for production performance or clear existing caches.

## View Cache
The view docs show:

```shell
php artisan view:cache
php artisan view:clear
```

The docs describe `view:cache` as precompiling all application views for improved performance and `view:clear` as clearing the existing view cache.

## Event Cache
The events docs state that in production, event discovery can be optimized by caching a manifest of all application listeners using `optimize` or `event:cache`.

The events docs state `event:clear` removes the event cache.

Run a fresh lookup before writing concrete `event:cache` or `event:clear` command snippets in user-facing code.

## Route Cache Boundary
The routing docs show clearing the route cache:

```shell
php artisan route:clear
```

Run a fresh lookup before using `route:cache` or describing route cache limitations.

## Package Optimize Hooks Boundary
The package docs state packages can use the `optimizes` method in a service provider to register package commands that run automatically when `optimize` or `optimize:clear` are executed.

Run a fresh lookup before writing concrete `optimizes(...)` code.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `route:cache`, concrete `event:cache` snippets, package `optimizes(...)` examples, config cache caveats, route cache caveats, view cache caveats, cache clearing sequences, or deployment ordering beyond the documented `optimize` guidance.
