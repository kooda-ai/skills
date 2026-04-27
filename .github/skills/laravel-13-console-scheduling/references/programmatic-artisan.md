# Programmatic Artisan

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x programmatic Artisan command execution.

## Calling Commands From Routes Or Controllers
The docs show using the `Artisan` facade from a route:

```php
use Illuminate\Support\Facades\Artisan;
use Illuminate\Support\Facades\Route;

Route::post('/user/{user}/mail', function (string $user) {
    $exitCode = Artisan::call('mail:send', [
        'user' => $user, '--queue' => 'default'
    ]);
});
```

Confirmed imports: `Illuminate\Support\Facades\Artisan` and `Illuminate\Support\Facades\Route`.

The docs state `Artisan::call()` accepts the command's signature or class name as the first argument and an array of parameters as the second argument. The route example stores the returned exit code.

## Passing Arguments And Options
The docs show a string command:

```php
Artisan::call('mail:send 1 --queue=default');
```

The docs show array values for options:

```php
Artisan::call('mail:send', [
    '--id' => [5, 13]
]);
```

The docs show boolean values for flags:

```php
$exitCode = Artisan::call('migrate:refresh', [
    '--force' => true,
]);
```

## Calling Commands From Other Commands
The docs show calling another command from a command's `handle()` method:

```php
public function handle(): void
{
    $this->call('mail:send', [
        'user' => 1, '--queue' => 'default'
    ]);

    $this->callSilently('mail:send', [
        'user' => 1, '--queue' => 'default'
    ]);
}
```

Confirmed methods: `$this->call(...)` and `$this->callSilently(...)`.

## Queued Artisan Commands
The docs show dispatching Artisan commands to the queue system:

```php
use Illuminate\Support\Facades\Artisan;

Artisan::queue('mail:send', [
    'user' => $user, '--queue' => 'default'
]);
```

The docs show setting a connection and queue name on the queued command:

```php
Artisan::queue('mail:send', [
    'user' => 1, '--queue' => 'default'
])->onConnection('redis')->onQueue('commands');
```

Confirmed methods: `Artisan::queue(...)`, `onConnection('redis')`, and `onQueue('commands')`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Artisan::output()`, `Artisan::callSilently()` from the facade, command class names in `Artisan::call()`, queue worker configuration, queue retry behavior, failed jobs, Horizon, command batches, command chains, or production queue guidance.
