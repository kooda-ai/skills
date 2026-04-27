# Eloquent Serialization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent serialization.

## Serializing To JSON
The docs show converting a model to JSON with `toJson()`:

```php
use App\Models\User;

$user = User::find(1);

// Explicit JSON conversion
return $user->toJson();
return $user->toJson(JSON_PRETTY_PRINT);
```

The docs state `toJson()` is recursive like `toArray()`, so all attributes and relations are converted to JSON.

The docs state JSON encoding options supported by PHP may be passed to `toJson()`.

## String Casting And Route Responses
The docs show casting a model to a string:

```php
return (string) User::find(1);
```

The docs state casting an Eloquent model or collection to a string automatically calls `toJson()`.

The docs show Eloquent objects returned from routes being automatically serialized:

```php
Route::get('/users', function () {
    return User::all();
});
```

The docs state Laravel automatically serializes Eloquent models and collections to JSON when they are returned from routes or controllers.

## Runtime Visibility Changes
The docs show methods for dynamically showing or hiding attributes during serialization:

```php
return $user->makeVisible('attribute')->toArray();
return $user->mergeVisible(['name', 'email'])->toArray();
return $user->makeHidden('attribute')->toArray();
return $user->mergeHidden(['name', 'email'])->toArray();
return $user->setVisible(['id', 'name'])->toArray();
return $user->setHidden(['email', 'password', 'remember_token'])->toArray();
```

Confirmed methods: `makeVisible()`, `mergeVisible()`, `makeHidden()`, `mergeHidden()`, `setVisible()`, and `setHidden()`.

## Appended Accessor Attributes
The docs show an accessor and the `Appends` attribute for including a non-database attribute in array and JSON output:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Casts\Attribute;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected function isAdmin(): Attribute
    {
        return new Attribute(
            get: fn () => 'yes',
        );
    }
}

#[Appends(['is_admin'])]
class User extends Model
{
    // ...
}
```

Confirmed import from the accessor snippet: `Illuminate\Database\Eloquent\Casts\Attribute`.

Run a fresh lookup before writing the exact import for the `Appends` attribute.

## Custom Date Cast Format
The docs show a custom date cast format used when a model is serialized to an array or JSON:

```php
/**
 * Get the attributes that should be cast.
 *
 * @return array<string, string>
 */
protected function casts(): array
{
    return [
        'created_at' => 'datetime:Y-m-d',
    ];
}
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `$hidden`, `$visible`, runtime `append()`, `setAppends()`, relationship hiding, date serialization methods beyond cast formats, custom casts beyond the returned date example, array serialization examples beyond shown `toArray()` usage, exact `Appends` imports, or route imports not shown clearly in the returned docs.
