# HTTP Error Pages

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP exceptions and custom error pages.

## HTTP Exceptions
The docs state some exceptions describe HTTP error codes from the server, such as a page not found error `404`, unauthorized error `401`, or developer-generated `500` error.

The docs show the `abort` helper generating an HTTP 404 response from anywhere in the application:

```php
abort(404);
```

## Custom Status Pages
The docs state custom error pages for HTTP status codes can be placed in `resources/views/errors`.

The docs show a 404 page path:

```text
resources/views/errors/404.blade.php
```

The docs state views in this directory should be named to match their HTTP status code.

The docs state the HTTP exception raised by `abort` is passed to the view as an `$exception` variable.

## Fallback Error Pages
The docs state fallback error pages can be defined for specific series of HTTP status codes.

For client-side errors, create:

```text
resources/views/errors/4xx.blade.php
```

For server-side errors, create:

```text
resources/views/errors/5xx.blade.php
```

The docs state these templates are catch-all pages for status codes that lack a dedicated view file.

The docs state fallback pages do not override Laravel's internal dedicated pages for `404`, `500`, and `503` status codes. Define individual error pages for those specific responses when customization is needed.

## Publishing Default Error Pages Boundary
The docs state Laravel's default error page templates may be published using the `vendor:publish` Artisan command.

Run a fresh lookup before writing the exact `vendor:publish` command arguments.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using exact publish tags, custom 503 maintenance pages, error page data beyond `$exception`, rendering behavior for specific HTTP exceptions beyond the documented examples, or error-page localization behavior.
