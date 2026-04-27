# Requests And Responses

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP client requests and response inspection.

## Making Requests
The docs show the `Http` facade for outbound HTTP requests:

```php
use Illuminate\Support\Facades\Http;

$response = Http::get('http://example.com');
```

The docs confirm HTTP client methods including `head`, `get`, `post`, `put`, `patch`, and `delete`.

## JSON Request Data
The docs show a `POST` request with an array payload:

```php
use Illuminate\Support\Facades\Http;

$response = Http::post('http://example.com/users', [
    'name' => 'Steve',
    'role' => 'Network Administrator',
]);
```

When making `POST`, `PUT`, and `PATCH` requests, the docs state that an array passed as the second argument is sent with the `application/json` content type by default.

## Headers Boundary
The docs show `withHeaders()` in an HTTP client assertion example:

```php
Http::withHeaders([
    'X-First' => 'foo',
])->post('http://example.com/users', [
    'name' => 'Taylor',
    'role' => 'Developer',
]);
```

Run a fresh lookup before using other request header helpers or authentication helpers.

## Inspecting Responses
The docs describe the response object as `Illuminate\Http\Client\Response` and confirm these methods:

```php
$response->body() : string;
$response->json($key = null, $default = null) : mixed;
$response->object() : object;
$response->collect($key = null) : Illuminate\Support\Collection;
$response->resource() : resource;
$response->status() : int;
$response->successful() : bool;
$response->redirect(): bool;
$response->failed() : bool;
$response->clientError() : bool;
$response->header($header) : string;
$response->headers() : array;
```

The error-handling docs also mention `serverError()` as a status-check method.

## Array Access
The docs state the response object implements `ArrayAccess` for direct JSON data access:

```php
return Http::get('http://example.com/users/1')['name'];
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using query parameters, form requests, raw bodies, `acceptJson()`, bearer tokens, basic authentication, timeout settings, connection timeout settings, attachments, cookies, request pooling, macros, or any request option not listed here.
