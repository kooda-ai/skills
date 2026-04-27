# Defining Middleware

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x middleware generation and middleware class definitions.

## Generating Middleware
The docs show generating a middleware class with Artisan:

```shell
php artisan make:middleware EnsureTokenIsValid
```

The docs state this command creates the basic file structure in the `app/Http/Middleware` directory.

## Middleware Class Shape
The docs show a middleware class with a `handle(...)` method:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class EnsureTokenIsValid
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next): Response
    {
        if ($request->input('token') !== 'my-secret-token') {
            return redirect('/home');
        }

        return $next($request);
    }
}
```

Confirmed imports and classes: `App\Http\Middleware`, `Closure`, `Illuminate\Http\Request`, and `Symfony\Component\HttpFoundation\Response`.

Confirmed request method and helper from this snippet: `$request->input('token')` and `redirect('/home')`.

## Before Middleware Pattern
The docs show a middleware that performs work before the request continues:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class BeforeMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        // Perform action

        return $next($request);
    }
}
```

## After Middleware Pattern
The docs show a middleware that performs work after the request passes through the application:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class AfterMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        $response = $next($request);

        // Perform action

        return $response;
    }
}
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using dependency injection in middleware constructors, middleware testing, middleware package registration, request lifecycle details beyond `handle(...)`, response mutation examples, custom response types, or middleware behavior from authentication, authorization, CSRF, Sanctum, or rate limiter packages.
