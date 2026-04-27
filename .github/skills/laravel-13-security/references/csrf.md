# CSRF Protection

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x CSRF protection.

## Form Tokens
The docs show adding a CSRF token to an HTML form with the Blade `@csrf` directive:

```blade
<form method="POST" action="/profile">
    @csrf

    <!-- Equivalent to... -->
    <input type="hidden" name="_token" value="{{ csrf_token() }}" />
</form>
```

Confirmed helper/directive names: `@csrf` and `csrf_token()`.

## AJAX Header
The docs state the CSRF middleware supports the `X-CSRF-TOKEN` request header in addition to checking CSRF tokens as POST parameters.

The docs show configuring jQuery to include the header from a Blade meta tag:

```javascript
$.ajaxSetup({
    headers: {
        'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
    }
});
```

## XSRF Cookie Header
The docs state Laravel provides an encrypted `XSRF-TOKEN` cookie with every response.

The docs state libraries such as Angular and Axios can automatically read this cookie and include its value in the `X-XSRF-TOKEN` request header for same-origin requests.

Context7 also returned Sanctum SPA examples for `/sanctum/csrf-cookie`. Treat those as package-specific SPA authentication details and run a fresh lookup before adding Sanctum flow guidance.

## Excluding URIs
The docs show excluding URIs from CSRF protection in `bootstrap/app.php`:

```php
->withMiddleware(function (Middleware $middleware): void {
    $middleware->preventRequestForgery(except: [
        'stripe/*',
        'http://example.com/foo/bar',
        'http://example.com/foo/*',
    ]);
})
```

The docs state this is useful for routes like payment webhooks, and also state that best practice is to place such routes outside the `web` middleware group.

The docs state CSRF middleware is automatically disabled during automated tests.

Run a fresh lookup before writing the exact import for the `Middleware` type in this snippet.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using CSRF middleware class names, route-specific exclusion APIs beyond `preventRequestForgery`, test helper behavior, Sanctum SPA authentication flows, token rotation details, frontend library setup beyond returned jQuery/Axios/Angular statements, or cookie/session behavior beyond the returned snippets.