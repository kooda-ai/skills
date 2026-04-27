# Package Discovery And Service Providers

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x package discovery and service providers.

## Package Discovery
The docs state a Laravel application's `bootstrap/providers.php` file contains the list of service providers that should be loaded by Laravel.

Instead of requiring users to manually add a package service provider to that list, the docs say a package may define providers in the `extra` section of the package's `composer.json` file so Laravel loads them automatically.

The docs show:

```json
"extra": {
    "laravel": {
        "providers": [
            "Barryvdh\\Debugbar\\ServiceProvider"
        ],
        "aliases": {
            "Debugbar": "Barryvdh\\Debugbar\\Facade"
        }
    }
},
```

Confirmed Composer keys: `extra`, `laravel`, `providers`, and `aliases`.

The docs state Laravel automatically registers service providers and facades when the package is installed and configured for discovery.

## Opting Out Of Discovery
The docs show disabling package discovery for a specific package in an application's `composer.json`:

```json
"extra": {
    "laravel": {
        "dont-discover": [
            "barryvdh/laravel-debugbar"
        ]
    }
},
```

The docs show disabling discovery for all packages:

```json
"extra": {
    "laravel": {
        "dont-discover": [
            "*"
        ]
    }
},
```

Confirmed key and values: `dont-discover`, a concrete package name, and `*`.

## Service Provider Purpose
The package docs state service providers are the connection point between a package and Laravel.

The docs state a package service provider is responsible for binding things into Laravel's service container and informing Laravel where to load package resources such as views, configuration, and language files.

The docs state a service provider contains `register` and `boot` methods.

The docs state the base `ServiceProvider` class is located in the `illuminate/support` Composer package, which should be added to the package's dependencies.

The returned package docs rendered the service provider namespace in malformed form. Run a fresh lookup before writing the exact `ServiceProvider` import for a package service provider.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using package skeleton layout, Composer autoload configuration, package installation commands, provider class imports, facade class imports, package testing setup, package discovery cache behavior, manual provider registration beyond `bootstrap/providers.php`, or package distribution workflows.
