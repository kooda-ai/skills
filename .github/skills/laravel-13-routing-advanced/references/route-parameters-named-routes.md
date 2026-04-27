# Route Parameters, Named Routes, And Route Cache

Sources used: Current Laravel 13.x documentation pages for routing and URL generation.

## Redirect And View Routes
The docs show redirect routes:

```php
Route::redirect('/here', '/there');
Route::redirect('/here', '/there', 301);
Route::permanentRedirect('/here', '/there');
```

The docs state `destination` and `status` are reserved route parameter names for redirect routes.

The docs show view routes:

```php
Route::view('/welcome', 'welcome');
Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

The docs state `view`, `data`, `status`, and `headers` are reserved route parameter names for view routes.

## Route Inspection
The docs show route inspection commands:

```shell
php artisan route:list
php artisan route:list -v
php artisan route:list -vv
php artisan route:list --path=api
php artisan route:list --except-vendor
php artisan route:list --only-vendor
```

## Route Parameters
The docs show required route parameters:

```php
Route::get('/user/{id}', function (string $id) {
    return 'User '.$id;
});
```

The docs show multiple route parameters:

```php
Route::get('/posts/{post}/comments/{comment}', function (string $postId, string $commentId) {
    // ...
});
```

The docs state route callback argument names do not need to match parameter names, because parameters are injected by order.

The docs show optional parameters:

```php
Route::get('/user/{name?}', function (?string $name = null) {
    return $name;
});

Route::get('/user/{name?}', function (?string $name = 'John') {
    return $name;
});
```

The docs also show route parameters after injected dependencies:

```php
use Illuminate\Http\Request;

Route::get('/user/{id}', function (Request $request, string $id) {
    return 'User '.$id;
});
```

## Route Constraints
The docs show direct `where(...)` constraints:

```php
Route::get('/user/{name}', function (string $name) {
    // ...
})->where('name', '[A-Za-z]+');

Route::get('/user/{id}', function (string $id) {
    // ...
})->where('id', '[0-9]+');

Route::get('/user/{id}/{name}', function (string $id, string $name) {
    // ...
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```

The docs show helper constraints:

```php
Route::get('/user/{id}/{name}', function (string $id, string $name) {
    // ...
})->whereNumber('id')->whereAlpha('name');

Route::get('/user/{name}', function (string $name) {
    // ...
})->whereAlphaNumeric('name');

Route::get('/user/{id}', function (string $id) {
    // ...
})->whereUuid('id');

Route::get('/user/{id}', function (string $id) {
    // ...
})->whereUlid('id');

Route::get('/category/{category}', function (string $category) {
    // ...
})->whereIn('category', ['movie', 'song', 'painting']);
```

The docs show global constraints:

```php
use Illuminate\Support\Facades\Route;

public function boot(): void
{
    Route::pattern('id', '[0-9]+');
}
```

The docs show allowing encoded forward slashes only in the last segment:

```php
Route::get('/search/{search}', function (string $search) {
    return $search;
})->where('search', '.*');
```

## Named Routes And Groups
The docs show naming routes:

```php
Route::get('/user/profile', function () {
    // ...
})->name('profile');
```

The docs show URL generation and redirect generation:

```php
$url = route('profile');

return redirect()->route('profile');

return to_route('profile');
```

The docs show parameters with named routes:

```php
Route::get('/user/{id}/profile', function (string $id) {
    // ...
})->name('profile');

$url = route('profile', ['id' => 1]);
$url = route('profile', ['id' => 1, 'photos' => 'yes']);
```

The docs show inspecting the current named route:

```php
if ($request->route()->named('profile')) {
    // ...
}
```

The docs show route group prefixing and name prefixing:

```php
Route::prefix('admin')->group(function () {
    Route::get('/users', function () {
        // Matches "/admin/users"
    });
});

Route::name('admin.')->group(function () {
    Route::get('/users', function () {
        // Route assigned name "admin.users"...
    })->name('users');
});
```

## Fallback Routes And Route Cache
The docs show fallback routes:

```php
Route::fallback(function () {
    // ...
});
```

The docs state fallback routes defined in `routes/web.php` receive the `web` middleware group by default.

The docs show route cache commands:

```shell
php artisan route:cache
php artisan route:clear
```

The docs state `route:cache` should be used during deployment and regenerated whenever routes change.

## Topics Requiring Fresh Lookup
Run a new documentation lookup before using route macros, custom route registrars, domain-specific caching caveats, route serialization limitations, or advanced URL-generation behavior not shown in the current routing and URL docs.