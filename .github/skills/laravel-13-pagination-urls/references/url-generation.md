# URL Generation

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x URL generation.

## Named Route URLs
The docs show the `route()` helper generating URLs for named routes:

```php
// Basic named route generation
echo route('post.show', ['post' => 1]);

// Multiple parameters
echo route('comment.show', ['post' => 1, 'comment' => 3]);

// Extra parameters as query string
echo route('post.show', ['post' => 1, 'search' => 'rocket']);
```

The docs state extra arguments are appended to the query string.

The docs show generating a route URL from an Eloquent model parameter:

```php
echo route('post.show', ['post' => $post]);
```

The docs state the `route` helper can automatically extract the route key from an Eloquent model when routes are defined using model binding.

## Arbitrary URLs And Query Strings
The docs show the `url()` helper generating arbitrary URLs based on the current request scheme and host:

```php
$post = App\Models\Post::find(1);
echo url("/posts/{$post->id}");
```

The docs show adding query parameters:

```php
echo url()->query('/posts', ['search' => 'Laravel']);
```

The docs show overwriting existing query parameters:

```php
echo url()->query('/posts?sort=latest', ['sort' => 'oldest']);
```

The docs show array parameters:

```php
$url = url()->query('/posts', ['columns' => ['title', 'body']]);
echo urldecode($url);
```

## Current And Previous URLs
The docs show current URL helpers:

```php
echo url()->current();
echo url()->full();
```

The docs show the URL facade form:

```php
use Illuminate\Support\Facades\URL;
echo URL::current();
```

The docs show previous URL helpers:

```php
echo url()->previous();
echo url()->previousPath();
```

Confirmed import for facade usage: `Illuminate\Support\Facades\URL`.

## URL Defaults Boundary
Context7 returned a URL defaults middleware example with malformed namespaces and imports. The confirmed concept is that `URL::defaults(['locale' => $request->user()->locale])` can set default values for URL parameters, but exact middleware namespaces/imports must be verified with a narrower Context7 lookup before use.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using controller action URLs, asset URLs, secure URL helpers, URL macros, force root URL, force scheme, default URL middleware imports, localization URL patterns, route model binding internals, or generated URL encoding behavior beyond the returned snippets.
