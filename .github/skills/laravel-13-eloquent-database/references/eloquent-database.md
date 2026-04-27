# Eloquent And Database

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent model generation, model factories, database testing, custom casts, and pagination.

## Eloquent Model Location And Base Class
The docs state Eloquent models are typically stored in `app\Models` and extend `Illuminate\Database\Eloquent\Model`.

## Model Generation
The docs confirm the `make:model` command and related generation options.

Generate a model with a migration:

```shell
php artisan make:model Flight --migration
```

Generate a model and related classes:

```shell
php artisan make:model Flight --all
```

```shell
php artisan make:model Flight -a
```

The docs state `--all` / `-a` generates a model, migration, factory, seeder, policy, controller, and form requests all at once.

## Factories In Seeders
The docs describe model factories as a way to define default attributes for Eloquent models and generate random data for testing and seeding.

The docs show:

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

Confirmed methods from this snippet: `factory()`, `count(50)`, `hasPosts(1)`, and `create()`.

## Factories In Tests
The docs show creating a model in tests with a factory:

```php
$user = User::factory()->create();
```

The Context7 result included Pest and PHPUnit examples for this pattern. Run a narrower lookup before adding imports or database test traits.

## Custom Eloquent Casts
The docs confirm generating a custom cast with:

```shell
php artisan make:cast AsJson
```

The docs show a cast implementing `Illuminate\Contracts\Database\Eloquent\CastsAttributes`:

```php
namespace App\Casts;

use Illuminate\Contracts\Database\Eloquent\CastsAttributes;
use Illuminate\Database\Eloquent\Model;

class AsJson implements CastsAttributes
{
    public function get(Model $model, string $key, mixed $value, array $attributes): array {
        return json_decode($value, true);
    }

    public function set(Model $model, string $key, mixed $value, array $attributes): string {
        return json_encode($value);
    }
}
```

The docs show registering the cast from a model method:

```php
namespace App\Models;

use App\Casts\AsJson;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected function casts(): array
    {
        return [
            'options' => AsJson::class,
        ];
    }
}
```

Confirmed cast details: `App\Casts\AsJson`, `CastsAttributes`, `get(Model $model, string $key, mixed $value, array $attributes)`, `set(Model $model, string $key, mixed $value, array $attributes)`, and `protected function casts(): array`.

## Eloquent Pagination
The docs show paginating Eloquent model results:

```php
use App\Models\User;

$users = User::paginate(15);
```

The docs describe this as fetching `User` models and paginating them with 15 items per page.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using migration schema methods, database connection configuration, seed commands, factory definitions, factory states, relationship methods beyond `hasPosts(1)` in the seeder example, query builder APIs, Eloquent relationship definitions, mass assignment, casts beyond the shown custom cast, accessors, mutators, scopes, model events, transactions, database assertions, pagination links, or pagination customization.
