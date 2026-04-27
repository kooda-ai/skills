# Rate Limiting

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x routing rate limiters and rate-limited actions.

## Named Route Rate Limiters
The docs show registering a named rate limiter in the `boot` method of `AppServiceProvider`:

```php
use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\RateLimiter;

public function boot(): void
{
    RateLimiter::for('api', function (Request $request) {
        return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
    });
}
```

Confirmed imports: `Illuminate\Cache\RateLimiting\Limit`, `Illuminate\Http\Request`, and `Illuminate\Support\Facades\RateLimiter`.

The docs state named limiters can control request frequency and that Laravel automatically returns a `429` HTTP status code when a request exceeds these limits.

## Applying Route Limiters
The docs show applying a named limiter with the `throttle` middleware:

```php
Route::middleware(['throttle:uploads'])->group(function () {
    Route::post('/audio', function () {
        // ...
    });

    Route::post('/video', function () {
        // ...
    });
});
```

## Custom Responses
The docs show customizing a rate-limit response with `Limit::response(...)`:

```php
RateLimiter::for('global', function (Request $request) {
    return Limit::perMinute(1000)->response(function (Request $request, array $headers) {
        return response('Custom response...', 429, $headers);
    });
});
```

## Response-Based Rate Limiting
The docs show counting only specific responses toward the limit using `after(...)`:

```php
use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\RateLimiter;
use Symfony\Component\HttpFoundation\Response;

RateLimiter::for('resource-not-found', function (Request $request) {
    return Limit::perMinute(10)
        ->by($request->user()?->id ?: $request->ip())
        ->after(function (Response $response) {
            // Only count 404 responses toward the rate limit to prevent enumeration...
            return $response->status() === 404;
        });
});
```

Confirmed additional import: `Symfony\Component\HttpFoundation\Response`.

## Rate-Limited Actions
The docs show executing a callback if the limit is not exceeded:

```php
use Illuminate\Support\Facades\RateLimiter;

$executed = RateLimiter::attempt(
    'send-message:'.$user->id,
    $perMinute = 5,
    function() {
        // Send message...
    }
);

if (! $executed) {
    return 'Too many messages sent!';
}
```

The docs show a custom decay rate:

```php
$executed = RateLimiter::attempt(
    'send-message:'.$user->id,
    $perTwoMinutes = 5,
    function() {
        // Send message...
    },
    $decayRate = 120,
);
```

## Manual Attempts
The docs show checking and incrementing attempts manually:

```php
use Illuminate\Support\Facades\RateLimiter;

if (RateLimiter::tooManyAttempts('send-message:'.$user->id, $perMinute = 5)) {
    return 'Too many attempts!';
}

RateLimiter::increment('send-message:'.$user->id);
```

The docs show checking remaining attempts:

```php
if (RateLimiter::remaining('send-message:'.$user->id, $perMinute = 5)) {
    RateLimiter::increment('send-message:'.$user->id);

    // Send message...
}
```

The docs show incrementing by an explicit amount:

```php
RateLimiter::increment('send-message:'.$user->id, amount: 5);
```

The docs show retrieving the remaining wait time:

```php
if (RateLimiter::tooManyAttempts('send-message:'.$user->id, $perMinute = 5)) {
    $seconds = RateLimiter::availableIn('send-message:'.$user->id);

    return 'You may try again in '.$seconds.' seconds.';
}

RateLimiter::increment('send-message:'.$user->id);
```

The docs show clearing attempts:

```php
use App\Models\Message;
use Illuminate\Support\Facades\RateLimiter;

/**
 * Mark the message as read.
 */
public function read(Message $message): Message
{
    $message->markAsRead();

    RateLimiter::clear('send-message:'.$message->user_id);

    return $message;
}
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Limit::none`, multiple limits, Redis throttle setup, named middleware aliases, custom headers beyond the returned `array $headers` callback, queue job rate limiting, event throttling, login throttling, or rate limiter testing helpers.