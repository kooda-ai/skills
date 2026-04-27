# Authentication

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x authentication and route protection.

## Auth Facade Login Helpers
The docs show manually authenticating user instances and IDs with `Illuminate\Support\Facades\Auth`:

```php
use Illuminate\Support\Facades\Auth;

// Login instance
Auth::login($user);
Auth::login($user, $remember = true);
Auth::guard('admin')->login($user);

// Login by ID
Auth::loginUsingId(1);
Auth::loginUsingId(1, remember: true);
```

Confirmed methods from this snippet: `Auth::login(...)`, `Auth::guard('admin')->login(...)`, and `Auth::loginUsingId(...)`.

## Retrieving The Authenticated User
The docs show retrieving the current user and ID with the `Auth` facade:

```php
use Illuminate\Support\Facades\Auth;

// Retrieve the currently authenticated user...
$user = Auth::user();

// Retrieve the currently authenticated user's ID...
$id = Auth::id();
```

The docs also show retrieving the authenticated user from the request in a controller:

```php
public function update(Request $request): RedirectResponse
{
    $user = $request->user();
    return redirect('/flights');
}
```

Confirmed methods from these snippets: `Auth::user()`, `Auth::id()`, and `$request->user()`.

## Protecting Routes
The docs show protecting routes with the `auth` middleware:

```php
Route::get('/flights', function () {
    // Only authenticated users may access this route...
})->middleware('auth');

// Specifying a guard
Route::get('/flights', function () {
    // Only authenticated users may access this route...
})->middleware('auth:admin');
```

The docs show protecting verified-user routes with the `verified` middleware alias alongside `auth`:

```php
Route::get('/profile', function () {
    // Only verified users may access this route...
})->middleware(['auth', 'verified']);
```

## Sanctum Snippet In Framework Docs
The Laravel 13 framework docs returned this Sanctum route protection snippet:

```php
use Illuminate\Http\Request;

Route::get('/user', function (Request $request) {
    return $request->user();
})->middleware('auth:sanctum');
```

Use this snippet only as a confirmed framework-doc example. For Sanctum setup, token behavior, SPA behavior, middleware installation, configuration, or API authentication details, resolve and query the `/laravel/sanctum` Context7 library.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using authentication starter kits, registration, login form handling, logout, password resets, password confirmation, email verification internals, remember tokens, guard configuration, providers, sessions, custom guards, events, throttling, or route macros beyond the middleware examples here.
