# Middleware Registration, Groups, And Aliases

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x global middleware, middleware groups, and aliases.

## Global Middleware
The docs state global middleware are executed during every HTTP request to the application.

The docs show appending middleware to the global stack in `bootstrap/app.php`:

```php
use App\Http\Middleware\EnsureTokenIsValid;

->withMiddleware(function (Middleware $middleware): void {
     $middleware->append(EnsureTokenIsValid::class);
});
```

The returned docs also state `prepend(...)` adds middleware to the beginning of the global stack.

The docs show manually defining the entire global middleware stack with `use(...)`:

```php
->withMiddleware(function (Middleware $middleware): void {
    $middleware->use([
        \Illuminate\Foundation\Http\Middleware\InvokeDeferredCallbacks::class,
        \Illuminate\Http\Middleware\TrustProxies::class,
        \Illuminate\Http\Middleware\HandleCors::class,
        \Illuminate\Foundation\Http\Middleware\PreventRequestsDuringMaintenance::class,
        \Illuminate\Http\Middleware\ValidatePostSize::class,
        \Illuminate\Foundation\Http\Middleware\TrimStrings::class,
        \Illuminate\Foundation\Http\Middleware\ConvertEmptyStringsToNull::class,
    ]);
});
```

Run a fresh lookup before writing the exact import for the `Middleware` type in `bootstrap/app.php` snippets.

## Default Web And API Groups
The docs show modifying the default `web` and `api` groups:

```php
use App\Http\Middleware\EnsureTokenIsValid;
use App\Http\Middleware\EnsureUserIsSubscribed;

->withMiddleware(function (Middleware $middleware): void {
    $middleware->web(append: [
        EnsureUserIsSubscribed::class,
    ]);

    $middleware->api(prepend: [
        EnsureTokenIsValid::class,
    ]);
});
```

The docs show replacing middleware in the `web` group:

```php
use App\Http\Middleware\StartCustomSession;
use Illuminate\Session\Middleware\StartSession;

$middleware->web(replace: [
    StartSession::class => StartCustomSession::class,
]);
```

The docs show removing middleware from the `web` group:

```php
$middleware->web(remove: [
    StartSession::class,
]);
```

## Custom Groups
The docs show adding middleware to a custom group:

```php
use App\Http\Middleware\First;
use App\Http\Middleware\Second;

->withMiddleware(function (Middleware $middleware): void {
    $middleware->appendToGroup('group-name', [
        First::class,
        Second::class,
    ]);
});

Route::get('/', function () {
    // ...
})->middleware('group-name');
```

The docs show manually defining the default `web` and `api` groups with `group(...)`:

```php
->withMiddleware(function (Middleware $middleware): void {
    $middleware->group('web', [
        \Illuminate\Cookie\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        \Illuminate\View\Middleware\ShareErrorsFromSession::class,
        \Illuminate\Foundation\Http\Middleware\PreventRequestForgery::class,
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ]);

    $middleware->group('api', [
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ]);
});
```

Confirmed group methods: `appendToGroup(...)`, `group(...)`, `web(...)`, and `api(...)`.

## Aliases
The docs show defining an alias in `bootstrap/app.php`:

```php
use App\Http\Middleware\EnsureUserIsSubscribed;

->withMiddleware(function (Middleware $middleware): void {
    $middleware->alias([
        'subscribed' => EnsureUserIsSubscribed::class
    ]);
})
```

The docs show using the alias on a route:

```php
Route::get('/profile', function () {
    // ...
})->middleware('subscribed');
```

Confirmed alias method and alias: `alias(...)` and `subscribed`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using default middleware stacks not shown here, middleware priority list modification helpers beyond `priority(...)`, route group behavior beyond shown examples, group replacement for `api`, alias collision behavior, named middleware aliases outside shown examples, or package-specific middleware registration.
