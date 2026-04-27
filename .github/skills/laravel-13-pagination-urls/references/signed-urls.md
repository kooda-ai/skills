# Signed URLs

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x signed URLs.

## Creating Signed URLs
The docs show creating a signed URL to a named route:

```php
use Illuminate\Support\Facades\URL;

return URL::signedRoute('unsubscribe', ['user' => 1]);
```

The docs state signed URLs append a signature hash so Laravel can verify the URL has not been tampered with.

The docs show creating a relative signed URL:

```php
use Illuminate\Support\Facades\URL;

return URL::signedRoute('unsubscribe', ['user' => 1], absolute: false);
```

The docs show creating a temporary signed URL:

```php
use Illuminate\Support\Facades\URL;

return URL::temporarySignedRoute(
    'unsubscribe',
    now()->plus(minutes: 30),
    ['user' => 1]
);
```

The docs state Laravel validates the expiration timestamp for temporary signed URLs.

Confirmed import: `Illuminate\Support\Facades\URL`.

## Validating Signed URLs
The docs show validating a signature with the incoming request:

```php
use Illuminate\Http\Request;

Route::get('/unsubscribe/{user}', function (Request $request) {
    if (! $request->hasValidSignature()) {
        abort(401);
    }

    // ...
})->name('unsubscribe');
```

The docs show ignoring specified query parameters when validating a signature:

```php
if (! $request->hasValidSignatureWhileIgnoring(['page', 'order'])) {
    abort(401);
}
```

Confirmed import for request examples: `Illuminate\Http\Request`.

## Signed Middleware
The docs show applying the `signed` middleware to automatically validate incoming signed URLs:

```php
use Illuminate\Http\Request;

Route::post('/unsubscribe/{user}', function (Request $request) {
    // ...
})->name('unsubscribe')->middleware('signed');
```

The docs state the middleware returns a `403` response if the signature is invalid.

The docs show configuring the middleware for relative URLs:

```php
use Illuminate\Http\Request;

Route::post('/unsubscribe/{user}', function (Request $request) {
    // ...
})->name('unsubscribe')->middleware('signed:relative');
```

## Invalid Signature Response
The docs show customizing the response for expired signed URLs in `bootstrap/app.php`:

```php
use Illuminate\Routing\Exceptions\InvalidSignatureException;

->withExceptions(function (Exceptions $exceptions): void {
    $exceptions->render(function (InvalidSignatureException $e) {
        return response()->view('errors.link-expired', status: 403);
    });
})
```

Confirmed exception import: `Illuminate\Routing\Exceptions\InvalidSignatureException`.

Run a fresh lookup before writing the exact import for the `Exceptions` type in this snippet.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using middleware-based parameter ignoring, signed URL testing helpers, expiration edge cases, custom exception rendering beyond the returned closure, signed route URL defaults, proxy/domain behavior, or route model binding behavior in signed URL parameters.
