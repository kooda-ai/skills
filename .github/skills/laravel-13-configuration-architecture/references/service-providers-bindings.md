# Service Providers And Bindings

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x service providers and service container bindings.

## Provider Registration
The docs show custom service providers registered in `bootstrap/providers.php`:

```php
<?php

return [
    App\Providers\AppServiceProvider::class,
    App\Providers\ComposerServiceProvider::class,
];
```

The docs say this file maintains an array of provider class names loaded during the application lifecycle.

## Generating Providers
The docs confirm this Artisan command:

```shell
php artisan make:provider RiakServiceProvider
```

The docs say this command generates a new service provider class and automatically registers it in `bootstrap/providers.php`.

## Writing Providers
The docs state all service providers extend `Illuminate\Support\ServiceProvider`. Most service providers contain `register` and `boot` methods.

The docs state that within the `register` method, you should only bind things into the service container. The docs say you should never attempt to register event listeners, routes, or any other piece of functionality within the `register` method.

## Singleton Binding In A Provider
The docs show registering a service binding in a provider `register()` method:

```php
<?php

namespace App\Providers;

use App\Services\Riak\Connection;
use Illuminate\Contracts\Foundation\Application;
use Illuminate\Support\ServiceProvider;

class RiakServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     */
    public function register(): void
    {
        $this->app->singleton(Connection::class, function (Application $app) {
            return new Connection(config('riak'));
        });
    }
}
```

Confirmed classes and methods: `App\Providers`, `App\Services\Riak\Connection`, `Illuminate\Contracts\Foundation\Application`, `Illuminate\Support\ServiceProvider`, `register(): void`, `$this->app->singleton(...)`, and `config('riak')`.

## Simple Container Bindings
The docs show `bind(...)` in a provider or similar container-aware context:

```php
use App\Services\Transistor;
use App\Services\PodcastParser;
use Illuminate\Contracts\Foundation\Application;

$this->app->bind(Transistor::class, function (Application $app) {
    return new Transistor($app->make(PodcastParser::class));
});
```

The docs show binding via the `App` facade:

```php
use App\Services\Transistor;
use Illuminate\Contracts\Foundation\Application;
use Illuminate\Support\Facades\App;

App::bind(Transistor::class, function (Application $app) {
    // ...
});
```

The docs show conditional binding with `bindIf(...)`:

```php
$this->app->bindIf(Transistor::class, function (Application $app) {
    return new Transistor($app->make(PodcastParser::class));
});
```

The docs show type-inferred binding:

```php
App::bind(function (Application $app): Transistor {
    return new Transistor($app->make(PodcastParser::class));
});
```

Confirmed methods and classes from these snippets: `$this->app->bind(...)`, `App::bind(...)`, `$this->app->bindIf(...)`, `$app->make(...)`, `App\Services\Transistor`, `App\Services\PodcastParser`, and `Illuminate\Support\Facades\App`.

## Facade Boundary
The current Context7 slice confirms the `App` facade for container binding. Run a fresh Context7 lookup before explaining facade concepts, real-time facades, facade root resolution, facade aliases, or facade testing outside the already documented testing skill.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using provider `boot()` examples, deferred providers, provider discovery, package provider registration, publishing config, event listener registration, route registration, view composers, singleton/scoped binding variants, interface-to-implementation binding, resolving services, facade internals, or real-time facades.
