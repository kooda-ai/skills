# Errors, Retries, And Middleware

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP client errors, retries, and middleware.

## Default Error Behavior
The docs state that Laravel's HTTP client wrapper does not throw exceptions for client or server errors by default. They point to response status methods such as `successful()`, `clientError()`, and `serverError()` for checking the response.

## Throwing Exceptions
The docs show response methods that throw `Illuminate\Http\Client\RequestException` based on status or conditions:

```php
use Illuminate\Http\Client\Response;

$response = Http::post(/* ... */);

// Throw an exception if a client or server error occurred...
$response->throw();

// Throw an exception if an error occurred and the given condition is true...
$response->throwIf($condition);

// Throw an exception if an error occurred and the given closure resolves to true...
$response->throwIf(fn (Response $response) => true);

// Throw an exception if an error occurred and the given condition is false...
$response->throwUnless($condition);

// Throw an exception if an error occurred and the given closure resolves to false...
$response->throwUnless(fn (Response $response) => false);

// Throw an exception if the response has a specific status code...
$response->throwIfStatus(403);

// Throw an exception unless the response has a specific status code...
$response->throwUnlessStatus(200);

// Throw an exception if a server error occurred (status >500)...
$response->throwIfServerError();

// Throw an exception if a client error occurred (status >400 and <500)...
$response->throwIfClientError();

return $response['user']['id'];
```

Preserve the documented `Illuminate\Http\Client\Response` import when using the closure examples.

## Error Callbacks
The docs state that `onError()` executes a callback immediately when a client or server error occurs.

Run a fresh lookup before writing a concrete callback example.

## Retry Failure Boundary
The docs show disabling exception throwing when all retries fail:

```php
$response = Http::retry(3, 100, throw: false)->post(/* ... */);
```

The docs state this returns the last response instead of throwing a `RequestException` when all retries fail.

Run a fresh lookup before using additional retry arguments, conditional retry callbacks, or exception mutation behavior.

## Request And Response Middleware
The docs state that Laravel's HTTP client is built on Guzzle and can use Guzzle middleware to manipulate outgoing requests or inspect incoming responses. They confirm specific-request middleware registration with `withRequestMiddleware()` and `withResponseMiddleware()`.

Run a fresh lookup before writing concrete middleware callbacks or using global middleware.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `throw()` callbacks beyond the documented snippets, detailed `onError()` signatures, retry backoff strategies, request middleware callback signatures, response middleware callback signatures, global middleware, or direct Guzzle options.
