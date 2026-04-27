# Resource Routing And URL Defaults

Sources used: Current Laravel 13.x documentation pages for controllers and URL generation.

## Nested Resource Routes
The docs show nesting resource routes with dot notation:

```php
use App\Http\Controllers\PhotoCommentController;

Route::resource('photos.comments', PhotoCommentController::class);
```

The docs state this produces nested URIs such as `/photos/{photo}/comments/{comment}`.

## Shallow Nesting
The docs show shallow nesting:

```php
use App\Http\Controllers\CommentController;

Route::resource('photos.comments', CommentController::class)->shallow();
```

The docs show shallow routes moving member routes to top-level comment URIs such as `/comments/{comment}` while keeping collection routes nested under `/photos/{photo}/comments`.

## Scoped Resource Routes
The docs show scoped nested resources:

```php
use App\Http\Controllers\PhotoCommentController;

Route::resource('photos.comments', PhotoCommentController::class)->scoped([
    'comment' => 'slug',
]);
```

The docs state this produces URIs like `/photos/{photo}/comments/{comment:slug}` and uses scoped implicit binding to ensure the child model belongs to the parent.

## Resource Route Naming And Parameters
The docs show customizing resource route names:

```php
use App\Http\Controllers\PhotoController;

Route::resource('photos', PhotoController::class)->names([
    'create' => 'photos.build',
]);
```

The docs show customizing resource route parameter names:

```php
use App\Http\Controllers\AdminUserController;

Route::resource('users', AdminUserController::class)->parameters([
    'users' => 'admin_user',
]);
```

The docs state this changes the `show` URI to `/users/{admin_user}`.

## Resource Missing And Soft-Delete Behavior
The docs show customizing missing-model behavior on a resource route:

```php
use App\Http\Controllers\PhotoController;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Redirect;

Route::resource('photos', PhotoController::class)
    ->missing(function (Request $request) {
        return Redirect::route('photos.index');
    });
```

The docs show allowing soft-deleted models on resource routes:

```php
use App\Http\Controllers\PhotoController;

Route::resource('photos', PhotoController::class)->withTrashed();
Route::resource('photos', PhotoController::class)->withTrashed(['show']);
```

## URL Defaults
The docs show setting URL defaults in middleware:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\URL;
use Symfony\Component\HttpFoundation\Response;

class SetDefaultLocaleForUrls
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next): Response
    {
        URL::defaults(['locale' => $request->user()->locale]);

        return $next($request);
    }
}
```

The docs state this is useful when many routes share a common parameter such as `{locale}`.

## URL Defaults Middleware Priority
The docs warn that URL defaults can interfere with implicit model binding and show prioritizing the middleware before `SubstituteBindings`:

```php
->withMiddleware(function (Middleware $middleware): void {
    $middleware->prependToPriorityList(
        before: \Illuminate\Routing\Middleware\SubstituteBindings::class,
        prepend: \App\Http\Middleware\SetDefaultLocaleForUrls::class,
    );
})
```

## Topics Requiring Fresh Lookup
Run a new documentation lookup before using resource macros, package-specific resource routing patterns, implicit-binding assumptions beyond the documented scoped resource behavior, or middleware-priority helpers beyond the shown URL-defaults example.