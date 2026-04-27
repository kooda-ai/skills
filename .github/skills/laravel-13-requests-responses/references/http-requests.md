# HTTP Requests

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP request access and dependency injection.

## Request Object
The docs describe `Illuminate\Http\Request` as an object-oriented interface for managing incoming HTTP requests. The docs say it allows access to request data such as input, cookies, and uploaded files.

Run a narrower Context7 lookup before using concrete request APIs for cookies or uploaded files, since the current result confirms those categories but not their method names.

## Dependency Injection In Controllers
The docs show injecting `Illuminate\Http\Request` into a controller method. The service container automatically provides the incoming request:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;

class UserController extends Controller
{
    /**
     * Store a new user.
     */
    public function store(Request $request): RedirectResponse
    {
        $name = $request->input('name');

        // Store the user...

        return redirect('/users');
    }
}
```

Confirmed classes and methods from this snippet: `Illuminate\Http\Request`, `Illuminate\Http\RedirectResponse`, and `$request->input('name')`.

## Dependency Injection In Route Closures
The docs show type-hinting the request object in route closures:

```php
use Illuminate\Http\Request;

Route::get('/', function (Request $request) {
    // ...
});
```

The docs say the service container automatically injects the current request instance without manual intervention.

## Controller Dependency Injection
The docs show constructor injection and method injection in a controller:

```php
class UserController extends Controller
{
    public function __construct(protected UserRepository $users) {}

    public function store(Request $request): RedirectResponse
    {
        return redirect('/users');
    }

    public function update(Request $request, string $id): RedirectResponse
    {
        return redirect('/users');
    }
}
```

Confirmed patterns from this snippet: constructor injection, `Request $request` method injection, and combining request injection with a route parameter such as `string $id`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using request path, URL, full URL, host, HTTP method, IP, headers, bearer tokens, query input, post input, JSON input, boolean/date/enum retrieval, uploaded file methods, cookie methods, old input, flashing input from the request object, merging input, or request macros.
