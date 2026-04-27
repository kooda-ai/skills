# Many To Many And Pivot Data

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x many-to-many relationships and intermediate table operations.

## Many-To-Many Definition Boundary
The docs state many-to-many relationships are established by defining a method that returns `belongsToMany(...)` with the related model as the primary argument.

The custom pivot example below confirms `BelongsToMany` as a return type and `belongsToMany(User::class)` as a relationship definition pattern. Run a fresh lookup before adding table-name, key-name, or timestamp options.

## Attaching And Detaching
The docs show attaching a role ID:

```php
use App\Models\User;

$user = User::find(1);

$user->roles()->attach($roleId);
```

The docs show attaching intermediate table data:

```php
$user->roles()->attach($roleId, ['expires' => $expires]);
```

The docs show detaching a single role and all roles:

```php
// Detach a single role from the user...
$user->roles()->detach($roleId);

// Detach all roles from the user...
$user->roles()->detach();
```

The docs show detaching multiple roles and attaching multiple roles with pivot data:

```php
$user = User::find(1);

$user->roles()->detach([1, 2, 3]);

$user->roles()->attach([
    1 => ['expires' => $expires],
    2 => ['expires' => $expires],
]);
```

Confirmed methods: `find(...)`, relationship method call `roles()`, `attach(...)`, and `detach(...)`.

## Pivot Attributes
The docs show accessing intermediate table columns through the `pivot` attribute:

```php
use App\Models\User;

$user = User::find(1);

foreach ($user->roles as $role) {
    echo $role->pivot->created_at;
}
```

Confirmed dynamic properties: `$user->roles`, `$role->pivot`, and `$role->pivot->created_at`.

## Pivot Constraints
The docs show filtering a `belongsToMany` query by an intermediate table column with `wherePivot(...)`:

```php
return $this->belongsToMany(Role::class)
    ->wherePivot('approved', 1);
```

Confirmed methods: `belongsToMany(...)` and `wherePivot(...)`.

## Syncing Associations
The docs show `sync(...)`:

```php
$user->roles()->sync([1, 2, 3]);
```

The docs show `sync(...)` with pivot data:

```php
$user->roles()->sync([1 => ['expires' => true], 2, 3]);
```

The docs show `syncWithPivotValues(...)`:

```php
$user->roles()->syncWithPivotValues([1, 2, 3], ['active' => true]);
```

The docs show `syncWithoutDetaching(...)`:

```php
$user->roles()->syncWithoutDetaching([1, 2, 3]);
```

Confirmed methods: `sync(...)`, `syncWithPivotValues(...)`, and `syncWithoutDetaching(...)`.

## Custom Pivot Models
The docs show specifying a custom model class for the intermediate table using `using(...)`. The docs state the custom pivot model must extend `Illuminate\Database\Eloquent\Relations\Pivot`.

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;

class Role extends Model
{
    /**
     * The users that belong to the role.
     */
    public function users(): BelongsToMany
    {
        return $this->belongsToMany(User::class)->using(RoleUser::class);
    }
}
```

Confirmed return type and methods: `BelongsToMany`, `belongsToMany(...)`, and `using(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `withPivot`, `withTimestamps`, custom pivot accessors, custom intermediate table names, custom foreign keys, `toggle`, `updateExistingPivot`, pivot events, custom pivot model restrictions, or polymorphic many-to-many relationship definitions.
