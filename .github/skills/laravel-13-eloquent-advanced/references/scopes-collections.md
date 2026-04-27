# Scopes And Collections

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent scopes and custom collections.

## Local Scopes
The docs show defining reusable query constraints with the `Scope` attribute:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Attributes\Scope;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * Scope a query to only include popular users.
     */
    #[Scope]
    protected function popular(Builder $query): void
    {
        $query->where('votes', '>', 100);
    }

    /**
     * Scope a query to only include active users.
     */
    #[Scope]
    protected function active(Builder $query): void
    {
        $query->where('active', 1);
    }
}
```

The docs state scopes should return the query builder instance or `void`.

Confirmed imports: `Illuminate\Database\Eloquent\Attributes\Scope`, `Illuminate\Database\Eloquent\Builder`, and `Illuminate\Database\Eloquent\Model`.

## Dynamic Scopes
The docs show adding parameters after the `$query` parameter:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Attributes\Scope;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * Scope a query to only include users of a given type.
     */
    #[Scope]
    protected function ofType(Builder $query, string $type): void
    {
        $query->where('type', $type);
    }
}
```

The docs show calling the dynamic scope:

```php
$users = User::ofType('admin')->get();
```

## Pending Attributes
The docs show `withAttributes(...)` inside a scope:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Attributes\Scope;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    /**
     * Scope the query to only include drafts.
     */
    #[Scope]
    protected function draft(Builder $query): void
    {
        $query->withAttributes([
            'hidden' => true,
        ]);
    }
}
```

The docs show creating a model through the scope:

```php
$draft = Post::draft()->create(['title' => 'In Progress']);

$draft->hidden; // true
```

The docs state `withAttributes` applies attributes to both the query `WHERE` clause and models created by the scope.

The docs show applying attributes only to created models:

```php
$query->withAttributes([
    'hidden' => true,
], asConditions: false);
```

## Chaining Scopes And Or Conditions
The docs show chaining local scopes:

```php
use App\Models\User;

$users = User::popular()->active()->orderBy('created_at')->get();
```

The docs show logical grouping for `orWhere` with scopes:

```php
$users = User::popular()->orWhere(function (Builder $query) {
    $query->active();
})->get();
```

The docs also show a higher-order `orWhere` form:

```php
$users = User::popular()->orWhere->active()->get();
```

## Custom Eloquent Collections
The docs show using the `CollectedBy` attribute on a model:

```php
namespace App\Models;

use App\Support\UserCollection;
use Illuminate\Database\Eloquent\Attributes\CollectedBy;
use Illuminate\Database\Eloquent\Model;

#[CollectedBy(UserCollection::class)]
class User extends Model
{
    // ...
}
```

The docs also show overriding `newCollection(...)`:

```php
namespace App\Models;

use App\Support\UserCollection;
use Illuminate\Database\Eloquent\Collection;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    public function newCollection(array $models = []): Collection
    {
        $collection = new UserCollection($models);

        if (Model::isAutomaticallyEagerLoadingRelationships()) {
            $collection->withRelationshipAutoloading();
        }

        return $collection;
    }
}
```

Confirmed methods: `newCollection(...)`, `Model::isAutomaticallyEagerLoadingRelationships()`, and `withRelationshipAutoloading()`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using global scopes, anonymous global scopes, removing scopes, `#[ScopedBy]`, additional pending attribute behavior, collection methods not shown here, collection generation commands, automatic eager loading details, or scope APIs not listed here.
