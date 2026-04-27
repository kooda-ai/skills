# HTTP Client Testing

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP client testing.

## Faking Requests
The docs show `Http::fake()` before making an HTTP client request in a test:

```php
use Illuminate\Http\Client\Request;
use Illuminate\Support\Facades\Http;

Http::fake();
```

Run a fresh lookup before returning fake responses, matching URLs, or using response sequences.

## Asserting Sent Requests
The docs show `Http::assertSent()` to verify that at least one sent request matches a closure. The closure receives an `Illuminate\Http\Client\Request` instance:

```php
use Illuminate\Http\Client\Request;
use Illuminate\Support\Facades\Http;

Http::fake();

Http::withHeaders([
    'X-First' => 'foo',
])->post('http://example.com/users', [
    'name' => 'Taylor',
    'role' => 'Developer',
]);

Http::assertSent(function (Request $request) {
    return $request->hasHeader('X-First', 'foo') &&
           $request->url() == 'http://example.com/users' &&
           $request['name'] == 'Taylor' &&
           $request['role'] == 'Developer';
});
```

Confirmed request inspection in this example: `hasHeader(...)`, `url()`, and array access to request payload values.

## Failed Request Simulation
The docs show `Http::failedRequest()` to simulate an `Illuminate\Http\Client\RequestException` being thrown:

```php
$this->mock(GithubService::class)
    ->shouldReceive('getUser')
    ->andThrow(
        Http::failedRequest(['code' => 'not_found'], 404)
    );
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Http::response()`, URL-pattern fakes, response sequences, stray request prevention, recorded request inspection, assertions other than `assertSent()`, or request inspection methods not shown in the documented example.
