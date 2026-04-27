# Factory Structure and Basics

## Factory Purpose and Shape
- The Eloquent factories docs state factories are classes that extend Laravel's base factory class.
- The docs state factories define a `definition` method that returns the default set of attribute values applied when creating a model through the factory.
- The docs state factories have access to Faker through the `fake` helper.

## Factory Generation Boundaries
- The current Laravel 13 docs context confirms the `make:factory` Artisan command exists and that generated factory classes are placed in `database/factories`.
- The current Context7 result did not return a concrete `php artisan make:factory ...` shell block, so run a fresh lookup before writing exact command arguments.

## Model Generation With Factory
The Eloquent docs show generating a model with its associated factory in one step:

```shell
php artisan make:model Flight --factory
```

```shell
php artisan make:model Flight -f
```

## Linking Models and Factories
- The docs confirm the `HasFactory` trait as the standard model-factory linkage trait.
- The current returned snippet showed `HasFactory` on an Eloquent model in a broadcasting example.
- The docs also show explicit linkage through `#[UseFactory(...)]`, `#[UseModel(...)]`, and overriding `newFactory()` when naming conventions do not apply.

```php
use Illuminate\Database\Eloquent\Attributes\UseFactory;
use Database\Factories\Administration\FlightFactory;

#[UseFactory(FlightFactory::class)]
class Flight extends Model
{
    // ...
}
```

```php
use Database\Factories\Administration\FlightFactory;

/**
 * Create a new factory instance for the model.
 */
protected static function newFactory()
{
    return FlightFactory::new();
}
```

```php
use App\Administration\Flight;
use Illuminate\Database\Eloquent\Factories\Attributes\UseModel;
use Illuminate\Database\Eloquent\Factories\Factory;

#[UseModel(Flight::class)]
class FlightFactory extends Factory
{
    // ...
}
```

## Built-In Trashed State
The Eloquent factories docs show the built-in `trashed()` state for soft-deletable models:

```php
use App\Models\User;

$user = User::factory()->trashed()->create();
```

## Boundaries
- Run a fresh lookup before using a full `definition(): array` example, the exact generated factory stub, `Sequence` code blocks, or command arguments for `make:factory`.
- Do not infer extra factory attributes or naming conventions beyond what the current Laravel 13 docs result confirms.
