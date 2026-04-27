# Cache

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x cache access.

## Retrieving Cache Values
The docs show retrieving a cache value with the `Cache` facade:

```php
$value = Cache::get('key');

$value = Cache::get('key', 'default');
```

The docs state `Cache::get('key')` returns `null` if the key does not exist. The second argument provides a default value returned when the requested key does not exist.

## Cache Facade In Controllers
The docs show importing and using `Cache` in a controller:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Support\Facades\Cache;

class UserController extends Controller
{
    /**
     * Show a list of all users of the application.
     */
    public function index(): array
    {
        $value = Cache::get('key');

        return [
            // ...
        ];
    }
}
```

## Cache Facade In Routes
The docs show `Cache` and `Route` facades together:

```php
use Illuminate\Support\Facades\Cache;
use Illuminate\Support\Facades\Route;

Route::get('/cache', function () {
    return Cache::get('key');
});
```

Confirmed imports: `Illuminate\Support\Facades\Cache` and `Illuminate\Support\Facades\Route`.

## Incrementing And Decrementing
The docs show cache integer adjustment methods:

```php
Cache::add('key', 0, now()->plus(hours: 4));
Cache::increment('key');
Cache::increment('key', $amount);
Cache::decrement('key');
Cache::decrement('key', $amount);
```

Confirmed methods: `add(...)`, `increment(...)`, and `decrement(...)`.

## Permanent Cache Items
The docs show storing a cache item without an expiration time:

```php
Cache::forever('key', 'value');
```

The docs state items stored with `forever` must be manually removed using the `forget` method.

Run a narrower lookup before writing a concrete `Cache::forget(...)` example.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Cache::put`, `has`, `missing`, `pull`, `remember`, `rememberForever`, `flexible`, `store`, cache tags, locks, memoization, cache events, pruning, driver configuration, cache testing helpers, or exact expiration behavior beyond the returned examples.
