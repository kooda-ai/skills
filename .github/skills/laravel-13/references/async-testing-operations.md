# Async, Testing, And Operations

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x scheduling, queued Artisan commands, console tests, HTTP tests, and facade testing.

## Scheduling Artisan Commands
The docs show scheduled Artisan commands using the `Schedule` facade:

```php
use App\Console\Commands\SendEmailsCommand;
use Illuminate\Support\Facades\Schedule;

Schedule::command('emails:send Taylor --force')->daily();

Schedule::command(SendEmailsCommand::class, ['Taylor', '--force'])->daily();
```

Confirmed methods and classes from this snippet:

- `App\Console\Commands\SendEmailsCommand`
- `Illuminate\Support\Facades\Schedule`
- `Schedule::command(...)`
- `daily()`
- Command strings and class references are both shown.

Run a narrower Context7 lookup before adding scheduling locations, frequency options beyond `daily()`, constraints, overlapping rules, background tasks, maintenance mode behavior, scheduler deployment, or cron entries.

## Queued Artisan Commands
The docs show queued Artisan commands with the `Artisan` facade:

```php
use Illuminate\Support\Facades\Artisan;

Artisan::queue('mail:send', [
    'user' => $user, '--queue' => 'default'
]);
```

```php
Artisan::queue('mail:send', [
    'user' => 1, '--queue' => 'default'
])->onConnection('redis')->onQueue('commands');
```

Confirmed methods and values from these snippets:

- `Illuminate\Support\Facades\Artisan`
- `Artisan::queue(...)`
- `onConnection('redis')`
- `onQueue('commands')`
- The documented examples include command arguments in an array.

Run a narrower Context7 lookup before adding job classes, queue workers, queue connections, failed jobs, batches, chains, Horizon, retries, timeouts, supervisor configuration, or production queue guidance.

## Console Tests
The docs show console command tests in both Pest and PHPUnit:

```php
test('console command', function () {
    $this->artisan('question')
        ->expectsQuestion('What is your name?', 'Taylor Otwell')
        ->expectsQuestion('Which language do you prefer?', 'PHP')
        ->expectsOutput('Your name is Taylor Otwell and you prefer PHP.')
        ->doesntExpectOutput('Your name is Taylor Otwell and you prefer Ruby.')
        ->assertExitCode(0);
});
```

```php
public function test_console_command(): void
{
    $this->artisan('question')
        ->expectsQuestion('What is your name?', 'Taylor Otwell')
        ->expectsQuestion('Which language do you prefer?', 'PHP')
        ->expectsOutput('Your name is Taylor Otwell and you prefer PHP.')
        ->doesntExpectOutput('Your name is Taylor Otwell and you prefer Ruby.')
        ->assertExitCode(0);
}
```

Confirmed test helpers from these snippets:

- `$this->artisan(...)`
- `expectsQuestion(...)`
- `expectsOutput(...)`
- `doesntExpectOutput(...)`
- `assertExitCode(...)`

## HTTP Tests
The docs show session and authentication setup in HTTP tests:

```php
test('an action that requires authentication', function () {
    $user = User::factory()->create();

    $response = $this->actingAs($user)
        ->withSession(['banned' => false])
        ->get('/');
});
```

```php
public function test_an_action_that_requires_authentication(): void
{
    $user = User::factory()->create();

    $response = $this->actingAs($user)
        ->withSession(['banned' => false])
        ->get('/');
}
```

Confirmed test helpers from these snippets:

- `actingAs($user)`
- `withSession(['banned' => false])`
- `get('/')`
- `User::factory()->create()`

Run a narrower Context7 lookup before adding response assertions, JSON tests, session assertions, redirects, exception handling, middleware handling, database assertions, or file upload tests.

## Facade Testing
The docs show facade mocking with `Cache::shouldReceive()`:

```php
use Illuminate\Support\Facades\Cache;

test('basic example', function () {
    Cache::shouldReceive('get')
        ->with('key')
        ->andReturn('value');

    $response = $this->get('/cache');

    $response->assertSee('value');
});
```

```php
use Illuminate\Support\Facades\Cache;

public function test_basic_example(): void
{
    Cache::shouldReceive('get')
        ->with('key')
        ->andReturn('value');

    $response = $this->get('/cache');

    $response->assertSee('value');
}
```

Confirmed helpers and classes from these snippets:

- `Illuminate\Support\Facades\Cache`
- `Cache::shouldReceive('get')`
- `with('key')`
- `andReturn('value')`
- `$this->get('/cache')`
- `assertSee('value')`

## Topics Requiring Fresh Lookup
The Context7 snapshot used for this reference did not confirm concrete APIs for cache usage outside facade testing, session usage outside HTTP tests, jobs, events, listeners, broadcasting, notifications, mail, filesystem storage, HTTP client, deployment, optimization commands, maintenance mode, production queue setup, or Laravel 13 upgrade steps. Query Context7 for the exact topic before adding those details.
