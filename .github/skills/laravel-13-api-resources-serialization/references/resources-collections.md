# Resources And Collections

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent API resources and resource collections.

## Returning A Single Resource
The docs show returning a resource directly from a route:

```php
use App\Http\Resources\PostResource;
use App\Models\Post;

Route::get('/api/posts/{post}', function (Post $post) {
    return new PostResource($post);
});
```

The docs also show returning a resource via the model's `toResource()` method:

```php
Route::get('/api/posts/{post}', function (Post $post) {
    return $post->toResource();
});
```

Run a fresh lookup before writing exact imports for `Route` in this example.

## Returning Resource Collections
The docs show returning multiple resources with `collection(...)`:

```php
return PostResource::collection(Post::all());
```

The docs also show returning a resource collection from a model collection:

```php
return Post::all()->toResourceCollection();
```

The docs show returning a resource collection from a route:

```php
use App\Http\Resources\UserResource;
use App\Models\User;

Route::get('/users', function () {
    return UserResource::collection(User::all());
});
```

## Custom Resource Collections
The docs show a custom resource collection class extending `Illuminate\Http\Resources\Json\ResourceCollection`:

```php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\ResourceCollection;

class CommentsCollection extends ResourceCollection
{
    /**
     * Transform the resource collection into an array.
     *
     * @return array<string, mixed>
     */
    public function toArray(Request $request): array
    {
        return ['data' => $this->collection];
    }
}
```

The returned docs state Laravel prevents double-wrapping even when nested.

Run a fresh lookup before writing the exact `Request` import for this snippet.

## Metadata Boundary
The docs state metadata such as `links` or other resource-specific information can be added to resource and resource collection responses within the `toArray()` method.

The docs state any `links` defined by the resource are merged with links automatically provided by Laravel for paginated responses.

Run a fresh lookup before writing concrete `links` or `meta` array examples.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using standard `php artisan make:resource` without `--json-api`, exact `JsonResource` imports, conditional attributes, conditional relationships, data wrapping configuration, pagination response examples, `additional()`, `with()`, exact `links` or `meta` payloads, or request imports not shown clearly in the returned docs.
