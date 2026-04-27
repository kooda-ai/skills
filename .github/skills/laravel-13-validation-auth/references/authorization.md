# Authorization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x authorization gates, policies, authorization responses, Blade directives, and controller authorization attributes.

## Gate Authorization In Controllers
The docs show authorizing an action that does not require a model instance with `Gate::authorize(...)`:

```php
use App\Models\Post;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Gate;

/**
 * Create a new blog post.
 *
 * @throws \Illuminate\Auth\Access\AuthorizationException
 */
public function create(Request $request): RedirectResponse
{
    Gate::authorize('create', Post::class);

    // The current user can create blog posts...

    return redirect('/posts');
}
```

The docs state that if the action is unauthorized, an `AuthorizationException` is thrown, resulting in a 403 HTTP response.

Confirmed classes and methods from this snippet: `App\Models\Post`, `Illuminate\Support\Facades\Gate`, `Gate::authorize(...)`, and `Illuminate\Auth\Access\AuthorizationException`.

## Policy Methods
The docs show a policy method that checks whether a user can update a post:

```php
<?php

namespace App\Policies;

use App\Models\Post;
use App\Models\User;

class PostPolicy
{
    /**
     * Determine if the given post can be updated by the user.
     */
    public function update(User $user, Post $post): bool
    {
        return $user->id === $post->user_id;
    }
}
```

The docs state policies are resolved via the service container, allowing dependency injection.

## Policy Registration Baseline
The broad Laravel 13 skill reference confirmed manual policy registration in `AppServiceProvider`:

```php
use App\Models\Order;
use App\Policies\OrderPolicy;
use Illuminate\Support\Facades\Gate;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Gate::policy(Order::class, OrderPolicy::class);
}
```

Run a narrower lookup before adding policy discovery behavior, policy generation commands, or policy registration variants.

## Authorization Responses In Gates
The docs show returning explicit authorization responses from gates:

```php
use App\Models\User;
use Illuminate\Auth\Access\Response;
use Illuminate\Support\Facades\Gate;

Gate::define('edit-settings', function (User $user) {
    return $user->isAdmin
        ? Response::allow()
        : Response::denyWithStatus(404);
});
```

```php
use App\Models\User;
use Illuminate\Auth\Access\Response;
use Illuminate\Support\Facades\Gate;

Gate::define('edit-settings', function (User $user) {
    return $user->isAdmin
        ? Response::allow()
        : Response::denyAsNotFound();
});
```

Confirmed methods and classes: `Gate::define(...)`, `Response::allow()`, `Response::denyWithStatus(404)`, and `Response::denyAsNotFound()`.

## Blade Authorization Directives
The docs show Blade directives for conditionally rendering content based on authorization policies:

```blade
@can('update', $post)
    <!-- Authorized -->
@elsecan('create', App\Models\Post::class)
    <!-- Authorized -->
@endcan

@canany(['update', 'view', 'delete'], $post)
    <!-- Authorized for any -->
@endcanany
```

Confirmed directives from this snippet: `@can`, `@elsecan`, `@endcan`, `@canany`, and `@endcanany`.

## Controller Authorization Attribute
The docs show the `Authorize` attribute as a shortcut for policy-based authorization on controller methods:

```php
class CommentController
{
    #[Authorize('create', [Comment::class, 'post'])]
    public function store(Post $post) { ... }
}
```

Run a narrower lookup before using imports, additional attribute options, or non-shown attribute patterns.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Gate::allows`, `Gate::denies`, `can` / `cannot` user methods, authorization middleware, policy generation commands, policy discovery, guest users, before/after policy hooks, inline authorization, custom denial messages, controller helper methods, or authorization tests.
