# Redis Pub/Sub

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Redis publish / subscribe usage.

## Pub/Sub Purpose
The docs state Laravel provides a convenient interface to Redis `publish` and `subscribe` commands.

The docs state these commands let an application listen for messages on a channel, and messages may be published from another application or another programming language.

## Publishing Messages
The docs show publishing a JSON-encoded message to a Redis channel from a route:

```php
use Illuminate\Support\Facades\Redis;

Route::get('/publish', function () {
    // ...

    Redis::publish('test-channel', json_encode([
        'name' => 'Adam Wathan'
    ]));
});
```

Confirmed method and channel: `Redis::publish(...)` and `test-channel`.

Run a fresh lookup before writing the exact `Route` import for this example.

## Subscribing To Channels
The docs show placing `subscribe(...)` in an Artisan command because calling `subscribe` begins a long-running process:

```php
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\Redis;

class RedisSubscribe extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'redis:subscribe';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Subscribe to a Redis channel';

    /**
     * Execute the console command.
     */
    public function handle(): void
    {
        Redis::subscribe(['test-channel'], function (string $message) {
            echo $message;
        });
    }
}
```

Confirmed classes, methods, and values: `App\Console\Commands`, `Illuminate\Console\Command`, `Illuminate\Support\Facades\Redis`, `protected $signature = 'redis:subscribe'`, `Redis::subscribe(...)`, and `test-channel`.

## Wildcard Subscriptions
The docs show wildcard subscriptions with `psubscribe(...)`:

```php
Redis::psubscribe(['*'], function (string $message, string $channel) {
    echo $message;
});

Redis::psubscribe(['users.*'], function (string $message, string $channel) {
    echo $message;
});
```

Confirmed method and closure parameters: `Redis::psubscribe(...)`, `string $message`, and `string $channel`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using queue workers or process managers for subscribers, unsubscribe behavior, error handling, reconnect behavior, multiple channel payload conventions, broadcasting integration, Redis events, monitor features, or production supervision details for long-running subscribers.
