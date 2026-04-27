# Route And Controller Middleware

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x route middleware, route exclusions, and controller middleware.

## Applying Middleware To Routes
The docs show applying an alias to a route:

```php
Route::get('/profile', function () {
    // ...
})->middleware('subscribed');
```

The docs show assigning a custom group to a route:

```php
Route::get('/', function () {
    // ...
})->middleware('group-name');
```

Run a fresh lookup before writing exact imports for `Route` in these examples.

## Excluding Middleware From Routes
The docs show excluding middleware from a route inside a middleware group:

```php
use App\Http\Middleware\EnsureTokenIsValid;

Route::middleware([EnsureTokenIsValid::class])->group(function () {
    Route::get('/', function () {
        // ...
    });

    Route::get('/profile', function () {
        // ...
    })->withoutMiddleware([EnsureTokenIsValid::class]);
});
```

The docs show excluding middleware from an entire route group:

```php
Route::withoutMiddleware([EnsureTokenIsValid::class])->group(function () {
    Route::get('/profile', function () {
        // ...
    });
});
```

Confirmed method: `withoutMiddleware(...)`.

## Controller Middleware
The controller docs show defining middleware directly in a controller by implementing `HasMiddleware`:

```php
class UserController implements HasMiddleware
{
	public static function middleware(): array
	{
		return [
			'auth',
			new Middleware('log', only: ['index']),
			new Middleware('subscribed', except: ['store']),
			function (Request $request, Closure $next) {
				return $next($request);
			},
		];
	}
}
```

Confirmed controller middleware concepts: `HasMiddleware`, static `middleware(): array`, string middleware, `new Middleware(...)`, `only`, `except`, and closure middleware.

Run a fresh lookup before writing exact imports for `HasMiddleware`, `Middleware`, `Request`, or `Closure` in this controller example.

## Resource Controller Middleware
The controller docs show applying middleware to specific resource controller methods:

```php
Route::resource('users', UserController::class)
    ->middlewareFor('show', 'auth');

Route::apiResource('users', UserController::class)
    ->middlewareFor(['show', 'update'], 'auth');

Route::singleton('profile', ProfileController::class)
    ->middlewareFor('show', 'auth');
```

The controller docs show excluding middleware from specific resource controller methods:

```php
Route::middleware(['auth', 'verified', 'subscribed'])->group(function () {
    Route::resource('users', UserController::class)
        ->withoutMiddlewareFor('index', ['auth', 'verified'])
        ->withoutMiddlewareFor(['create', 'store'], 'verified');
});
```

Confirmed methods: `middlewareFor(...)` and `withoutMiddlewareFor(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using controller middleware imports, invokable-controller middleware details, route middleware arrays beyond shown examples, middleware exclusion behavior for global middleware, API singleton resource middleware examples, route caching interactions, or package-specific route middleware.
