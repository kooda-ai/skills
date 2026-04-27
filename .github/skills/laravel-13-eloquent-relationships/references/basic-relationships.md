# Basic Relationships

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent relationship definitions.

## `hasMany()`
The docs show a `hasMany` relationship method on a model:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class User extends Model
{
    /**
     * Get all of the posts for the user.
     */
    public function posts(): HasMany
    {
        return $this->hasMany(Post::class);
    }
}
```

The docs also show a `Post::comments()` relationship:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Post extends Model
{
    /**
     * Get the comments for the blog post.
     */
    public function comments(): HasMany
    {
        return $this->hasMany(Comment::class);
    }
}
```

Confirmed return type and method: `Illuminate\Database\Eloquent\Relations\HasMany` and `hasMany(...)`.

## `hasOne()`
The docs state that a `hasOne` relationship is placed as a method on the parent model and returns the result of the `hasOne` method.

The returned snippet confirmed this method body and return type:

```php
public function phone(): HasOne
{
    return $this->hasOne(Phone::class);
}
```

The returned snippet also confirmed `Illuminate\Database\Eloquent\Relations\HasOne`, but its namespace line was malformed. Run a fresh lookup before producing a full `hasOne` class example.

## `belongsTo()`
The docs show a standard `belongsTo` relationship:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;

class Book extends Model
{
    /**
     * Get the author that wrote the book.
     */
    public function author(): BelongsTo
    {
        return $this->belongsTo(Author::class);
    }
}
```

The docs also show the inverse of a `hasMany` relationship:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;

class Comment extends Model
{
    /**
     * Get the post that owns the comment.
     */
    public function post(): BelongsTo
    {
        return $this->belongsTo(Post::class);
    }
}
```

The docs state the inverse of a `hasOne` relationship is defined using `belongsTo` on the related model, and that Eloquent infers the foreign key name and parent's primary key unless customized.

## `belongsToMany()` Boundary
The docs state many-to-many relationships are established by defining a method that returns the result of `belongsToMany(...)`. The method is provided by the Eloquent base model class and requires the related model name as its primary argument.

Use [many-to-many-pivot.md](./many-to-many-pivot.md) for confirmed pivot operations. Run a narrower lookup before writing a full `belongsToMany` definition beyond the custom pivot example.

## Dynamic Relationship Properties
The docs show accessing related models through a dynamic property:

```php
$post = Post::find(1);

foreach ($post->tags as $tag) {
    // ...
}
```

The returned snippet's import line was malformed, so do not copy its import without a fresh lookup.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using custom foreign keys, custom local keys, custom owner keys, default models, relationship existence queries beyond `withWhereHas`, relationship counting, touching parents, preventing lazy loading, route model binding interactions, or relationship testing helpers.
