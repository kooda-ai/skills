# Polymorphic, Through, And One Of Many

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x polymorphic relationships, through relationships, and one-of-many relationships.

## Polymorphic `morphTo()` And `morphMany()`
The docs show the child model using `morphTo()` and parent models using `morphMany(...)`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphTo;

class Comment extends Model
{
    /**
     * Get the parent commentable model (post or video).
     */
    public function commentable(): MorphTo
    {
        return $this->morphTo();
    }
}

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphMany;

class Post extends Model
{
    /**
     * Get all of the post's comments.
     */
    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphMany;

class Video extends Model
{
    /**
     * Get all of the video's comments.
     */
    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
```

Confirmed return types and methods: `MorphTo`, `MorphMany`, `morphTo()`, and `morphMany(Comment::class, 'commentable')`.

## Factory Polymorphic Helper Boundary
The docs show creating polymorphic `morphMany` relationships using factory magic methods when a `morphMany` relationship is defined:

```php
use App\Models\Post;

$post = Post::factory()->hasComments(3)->create();
```

Run a narrower lookup before adding other factory relationship methods or factory definitions.

## `loadMorph()`
The docs show eager loading a `morphTo` relationship and nested relationships with `loadMorph(...)`:

```php
$activities = ActivityFeed::with('parentable')
    ->get()
    ->loadMorph('parentable', [
        Event::class => ['calendar'],
        Photo::class => ['tags'],
        Post::class => ['author'],
    ]);
```

Confirmed methods: `with(...)`, `get()`, and `loadMorph(...)`.

## Polymorphic Many-To-Many Boundary
The docs state polymorphic many-to-many relationships such as `morphToMany` and `morphedByMany` can be created using factories in the same way as non-polymorphic many-to-many relationships, including `hasAttached` or magic `has` methods.

Run a fresh lookup before adding concrete `morphToMany(...)` or `morphedByMany(...)` relationship definitions.

## `hasManyThrough()`
The docs show a `hasManyThrough` relationship:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasManyThrough;

class Application extends Model
{
    /**
     * Get all of the deployments for the application.
     */
    public function deployments(): HasManyThrough
    {
        return $this->hasManyThrough(Deployment::class, Environment::class);
    }
}
```

Confirmed return type and method: `HasManyThrough` and `hasManyThrough(...)`.

## One Of Many Relationships
The docs show latest and oldest has-one-of-many relationships:

```php
/**
 * Get the user's most recent order.
 */
public function latestOrder(): HasOne
{
    return $this->hasOne(Order::class)->latestOfMany();
}
```

```php
/**
 * Get the user's oldest order.
 */
public function oldestOrder(): HasOne
{
    return $this->hasOne(Order::class)->oldestOfMany();
}
```

The docs show a custom aggregate one-of-many relationship:

```php
/**
 * Get the user's largest order.
 */
public function largestOrder(): HasOne
{
    return $this->hasOne(Order::class)->ofMany('price', 'max');
}
```

The docs show converting an existing `hasMany` relationship to a has-one relationship with `one()`:

```php
/**
 * Get the user's orders.
 */
public function orders(): HasMany
{
    return $this->hasMany(Order::class);
}

/**
 * Get the user's largest order.
 */
public function largestOrder(): HasOne
{
    return $this->orders()->one()->ofMany('price', 'max');
}
```

The docs show a `HasOneThrough` one-of-many pattern:

```php
public function latestDeployment(): HasOneThrough
{
    return $this->deployments()->one()->latestOfMany();
}
```

Confirmed methods: `latestOfMany()`, `oldestOfMany()`, `ofMany(...)`, and `one()`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `morphOne()` concrete definitions, polymorphic one-of-many concrete definitions, `hasOneThrough()` full definitions, custom keys for through relationships, fluent `through()` syntax, morph maps, `whereHasMorph`, `whereDoesntHaveMorph`, or concrete polymorphic many-to-many definitions.
