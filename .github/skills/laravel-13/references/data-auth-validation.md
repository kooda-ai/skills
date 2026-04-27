# Data, Auth, And Validation

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent model generation, factories, seeders, and authorization policy registration.

## Eloquent Models
The docs say Eloquent models are typically stored in the `app\Models` directory and extend `Illuminate\Database\Eloquent\Model`.

The docs confirm the `make:model` Artisan command and the `--all` / `-a` options for generating model-related classes:

```shell
php artisan make:model Flight --all
```

```shell
php artisan make:model Flight -a
```

The docs state these options generate a model, migration, factory, seeder, policy, controller, and form requests all at once.

Run a narrower Context7 lookup before adding model properties, casts, mass assignment, accessors, mutators, scopes, pruning, events, relationships, collections, serialization, route binding, or query behavior.

## Factories And Seeding
The docs describe model factories as a way to define default attributes for Eloquent models and generate random data for testing and seeding.

The docs show factories used from a seeder:

```php
use App\Models\User;

/**
 * Run the database seeders.
 */
public function run(): void
{
    User::factory()
        ->count(50)
        ->hasPosts(1)
        ->create();
}
```

Confirmed methods and classes from this snippet:

- `App\Models\User`
- `User::factory()`
- `count(50)`
- `hasPosts(1)`
- `create()`
- `run(): void`

Run a narrower Context7 lookup before adding factory definitions, factory states, callbacks, sequences, relationships beyond this exact snippet, seeder commands, or database refreshing behavior.

## Authorization Policy Registration
The docs show manual policy registration with the `Gate` facade in the `boot` method of `AppServiceProvider`:

```php
use App\Models\Order;
use App\Policies\OrderPolicy;
use Illuminate\Support\Facades\Gate;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Gate::policy(Order::class, OrderPolicy::class);
}
```

Confirmed details from this snippet:

- `App\Models\Order`
- `App\Policies\OrderPolicy`
- `Illuminate\Support\Facades\Gate`
- `boot(): void`
- `Gate::policy(Order::class, OrderPolicy::class)`
- Policy registration occurs in `AppServiceProvider` in the documented example.

Run a narrower Context7 lookup before adding gate definitions, policy method names, authorization helpers, controller authorization, Blade authorization directives, model policy discovery, response customization, or inline authorization behavior.

## Topics Requiring Fresh Lookup
The Context7 snapshot used for this reference did not confirm concrete APIs for database connections, migrations, schema builders, relationships, query builder methods, pagination, validation rules, form request internals, authentication starters, password reset, email verification, guards, gates beyond policy registration, or policy method behavior. Query Context7 for the exact topic before adding those details.
