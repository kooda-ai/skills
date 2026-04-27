# Route Model Binding

Sources used: Current Laravel 13.x documentation pages for routing.

## Implicit Binding
The docs show implicit model binding:

```php
use App\Models\User;

Route::get('/users/{user}', function (User $user) {
    return $user->email;
});
```

The docs state Laravel resolves the model automatically when the type-hinted variable name matches the route segment name. If no matching model is found, a 404 response is returned.

The docs also show implicit binding with a controller method:

```php
use App\Http\Controllers\UserController;
use App\Models\User;

Route::get('/users/{user}', [UserController::class, 'show']);

public function show(User $user)
{
    return view('user.profile', ['user' => $user]);
}
```

## Soft Deleted Models
The docs show allowing soft-deleted models in implicit binding:

```php
use App\Models\User;

Route::get('/users/{user}', function (User $user) {
    return $user->email;
})->withTrashed();
```

## Custom Keys
The docs show binding by a custom key directly in the route parameter:

```php
use App\Models\Post;

Route::get('/posts/{post:slug}', function (Post $post) {
    return $post;
});
```

The docs show overriding `getRouteKeyName()` on the model:

```php
/**
 * Get the route key for the model.
 */
public function getRouteKeyName(): string
{
    return 'slug';
}
```

## Scoped Bindings
The docs show nested implicit binding with a custom key:

```php
use App\Models\Post;
use App\Models\User;

Route::get('/users/{user}/posts/{post:slug}', function (User $user, Post $post) {
    return $post;
});
```

The docs state Laravel automatically scopes the nested model to the parent model when a custom keyed child binding is used.

The docs show forcing scoped bindings even without a custom key:

```php
use App\Models\Post;
use App\Models\User;

Route::get('/users/{user}/posts/{post}', function (User $user, Post $post) {
    return $post;
})->scopeBindings();
```

The docs also show group-wide scoped bindings:

```php
Route::scopeBindings()->group(function () {
    Route::get('/users/{user}/posts/{post}', function (User $user, Post $post) {
        return $post;
    });
});
```

The docs show disabling scoping explicitly:

```php
Route::get('/users/{user}/posts/{post:slug}', function (User $user, Post $post) {
    return $post;
})->withoutScopedBindings();
```

## Missing Model Behavior
The docs show customizing missing-model behavior:

```php
use App\Http\Controllers\LocationsController;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Redirect;

Route::get('/locations/{location:slug}', [LocationsController::class, 'show'])
    ->name('locations.view')
    ->missing(function (Request $request) {
        return Redirect::route('locations.index');
    });
```

## Implicit Enum Binding
The docs show implicit enum binding for string-backed enums:

```php
use App\Enums\Category;
use Illuminate\Support\Facades\Route;

Route::get('/categories/{category}', function (Category $category) {
    return $category->value;
});
```

The docs state Laravel returns 404 if the segment does not match a valid enum value.

## Explicit Binding
The docs show explicit model binding in `AppServiceProvider`:

```php
use App\Models\User;
use Illuminate\Support\Facades\Route;

public function boot(): void
{
    Route::model('user', User::class);
}
```

The docs show custom binding resolution logic:

```php
use App\Models\User;
use Illuminate\Support\Facades\Route;

public function boot(): void
{
    Route::bind('user', function (string $value) {
        return User::where('name', $value)->firstOrFail();
    });
}
```

The docs show overriding `resolveRouteBinding()` on the model:

```php
public function resolveRouteBinding($value, $field = null)
{
    return $this->where('name', $value)->firstOrFail();
}
```

The docs show `resolveChildRouteBinding()` for child binding resolution:

```php
public function resolveChildRouteBinding($childType, $value, $field)
{
    return parent::resolveChildRouteBinding($childType, $value, $field);
}
```

## Topics Requiring Fresh Lookup
Run a new documentation lookup before using polymorphic binding edge cases, custom binding behavior across packages, authorization assumptions built on bindings, or binding behavior not shown in the current routing docs.