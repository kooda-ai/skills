# Observers And Pruning

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent observers, model events, and pruning.

## Observer Generation
The docs show generating an observer class for a specific model:

```shell
php artisan make:observer UserObserver --model=User
```

The docs state this command places the observer in the `app/Observers` directory.

## Observer Registration With Attribute
The docs show registering an observer by applying `ObservedBy` to the model class:

```php
use App\Observers\UserObserver;
use Illuminate\Database\Eloquent\Attributes\ObservedBy;

#[ObservedBy([UserObserver::class])]
class User extends Authenticatable
{
    //
}
```

Confirmed import: `Illuminate\Database\Eloquent\Attributes\ObservedBy`.

Run a fresh lookup before writing the exact parent class import for `Authenticatable`.

## Model Lifecycle Events Boundary
The docs state Eloquent models dispatch events for moments in a model's lifecycle such as retrieval, creation, updating, saving, deletion, and restoration.

The docs state events ending with `-ing` are dispatched before persistence and events ending with `-ed` are dispatched after persistence.

Run a fresh lookup before listing exact event names or writing observer method names.

## Prunable Models
The docs show a model using the `Prunable` trait and defining `prunable(): Builder`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Prunable;

class Flight extends Model
{
    use Prunable;

    /**
     * Get the prunable model query.
     */
    public function prunable(): Builder
    {
        return static::where('created_at', '<=', now()->minus(months: 1));
    }
}
```

Confirmed imports: `Illuminate\Database\Eloquent\Builder`, `Illuminate\Database\Eloquent\Model`, and `Illuminate\Database\Eloquent\Prunable`.

The docs state the `prunable()` method defines the query for models that should be pruned and should return an Eloquent query builder.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using exact model event names, observer method names, observer discovery behavior, manual observer registration, muting events, queued anonymous event listeners, `MassPrunable`, `model:prune`, pruning schedules, pruning soft-deleted models, pruning events, or testing model events.
