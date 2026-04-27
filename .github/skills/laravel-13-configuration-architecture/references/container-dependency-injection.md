# Container And Dependency Injection

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x service container, zero configuration resolution, dependency injection, and contextual binding.

## Zero Configuration Resolution
The docs state that if a class has no dependencies or only depends on other concrete classes, the container does not need to be instructed on how to resolve that class.

The docs say many application classes automatically receive dependencies through the container, including controllers, event listeners, middleware, and queued job `handle` methods.

Run a narrower Context7 lookup before adding the exact route example for zero configuration resolution, since the current result described it but did not return the full code block.

## Controller Constructor Injection
The docs show controller constructor injection with a service class:

```php
<?php

namespace App\Http\Controllers;

use App\Services\AppleMusic;

class PodcastController extends Controller
{
    /**
     * Create a new controller instance.
     */
    public function __construct(
        protected AppleMusic $apple,
    ) {}

    /**
     * Show information about the given podcast.
     */
    public function show(string $id): Podcast
    {
        return $this->apple->findPodcast($id);
    }
}
```

The docs state the Laravel service container automatically resolves and injects controller constructor dependencies when they are type-hinted.

## Controller Method Injection
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

Confirmed patterns from this snippet: controller constructor injection, `Request $request` method injection, return type `RedirectResponse`, and route parameter injection such as `string $id`.

## Route Closure Request Injection
The docs show type-hinting the request object in route closures:

```php
use Illuminate\Http\Request;

Route::get('/', function (Request $request) {
    // ...
});
```

The docs state the container automatically injects the current request instance.

## Contextual Binding
The docs show contextual binding for different implementations:

```php
use App\Http\Controllers\PhotoController;
use App\Http\Controllers\UploadController;
use App\Http\Controllers\VideoController;
use Illuminate\Contracts\Filesystem\Filesystem;
use Illuminate\Support\Facades\Storage;

$this->app->when(PhotoController::class)
    ->needs(Filesystem::class)
    ->give(function () {
        return Storage::disk('local');
    });

$this->app->when([VideoController::class, UploadController::class])
    ->needs(Filesystem::class)
    ->give(function () {
        return Storage::disk('s3');
    });
```

Confirmed contextual binding chain: `when(...)`, `needs(...)`, and `give(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `make`, `bound`, `instance`, singleton variants beyond provider examples, scoped bindings, interface binding details, primitive contextual binding, tags, resolving callbacks, method invocation, container events, or full request lifecycle details.
