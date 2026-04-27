# Middleware Parameters, Terminable Middleware, And Priority

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x middleware parameters, terminable middleware, and middleware priority.

## Middleware Parameters
The docs show a middleware accepting an additional `string $role` parameter after `$next`:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class EnsureUserHasRole
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next, string $role): Response
    {
        if (! $request->user()->hasRole($role)) {
            // Redirect...
        }

        return $next($request);
    }
}
```

The docs show passing parameters in route definitions by appending them to the middleware name with a colon:

```php
use App\Http\Middleware\EnsureUserHasRole;

Route::put('/post/{id}', function (string $id) {
    // ...
})->middleware(EnsureUserHasRole::class.':editor');
```

The docs show multiple parameters separated by commas:

```php
Route::put('/post/{id}', function (string $id) {
    // ...
})->middleware(EnsureUserHasRole::class.':editor,publisher');
```

## Terminable Middleware
The docs state terminable middleware can execute tasks after the HTTP response has been sent to the browser.

The docs show a middleware with `terminate(Request $request, Response $response): void`:

```php
<?php

namespace Illuminate\Session\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class TerminatingMiddleware
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next): Response
    {
        return $next($request);
    }

    /**
     * Handle tasks after the response has been sent to the browser.
     */
    public function terminate(Request $request, Response $response): void
    {
        // ...
    }
}
```

The docs state Laravel automatically invokes terminable middleware after the response has been sent if the web server is using FastCGI.

The docs show registering a terminable middleware as a singleton so the same instance is used for `handle` and `terminate`:

```php
use App\Http\Middleware\TerminatingMiddleware;

/**
 * Register any application services.
 */
public function register(): void
{
    $this->app->singleton(TerminatingMiddleware::class);
}
```

## Middleware Priority
The docs state that when middleware must execute in a specific order but the order assigned to routes is not controllable, priority can be specified in `bootstrap/app.php`.

The docs show:

```php
->withMiddleware(function (Middleware $middleware): void {
    $middleware->priority([
        \Illuminate\Foundation\Http\Middleware\HandlePrecognitiveRequests::class,
        \Illuminate\Cookie\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        \Illuminate\View\Middleware\ShareErrorsFromSession::class,
        \Illuminate\Foundation\Http\Middleware\PreventRequestForgery::class,
        \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
        \Illuminate\Routing\Middleware\ThrottleRequests::class,
        \Illuminate\Routing\Middleware\ThrottleRequestsWithRedis::class,
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
        \Illuminate\Contracts\Auth\Middleware\AuthenticatesRequests::class,
        \Illuminate\Auth\Middleware\Authorize::class,
    ]);
})
```

The URL docs returned a `prependToPriorityList(...)` example for URL-default middleware, but the returned namespace formatting was malformed. Run a fresh lookup before using that method or writing exact imports for that example.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using additional parameter type patterns, variadic parameters, middleware parameter aliases beyond shown syntax, terminable middleware state management beyond singleton registration, FastCGI server configuration, Octane-specific behavior, priority helper methods beyond `priority(...)`, or Sanctum/auth/throttle middleware behavior beyond the class names shown in the priority list.
