# Testing Patterns

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x HTTP tests, console tests, facade testing, exception reporting tests, model factories in tests, and time-sensitive tests.

## Basic HTTP Request Tests
The docs show a basic HTTP test in Pest:

```php
<?php

test('basic request', function () {
    $response = $this->get('/');

    $response->assertStatus(200);
});
```

The docs show the same pattern in PHPUnit:

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;

class ExampleTest extends TestCase
{
    /**
     * A basic test example.
     */
    public function test_a_basic_request(): void
    {
        $response = $this->get('/');

        $response->assertStatus(200);
    }
}
```

Confirmed helpers and classes: `$this->get('/')`, `$response->assertStatus(200)`, `Tests\Feature`, and `Tests\TestCase`.

## Session And Authentication In HTTP Tests
The docs show:

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

Confirmed helpers: `User::factory()->create()`, `actingAs($user)`, `withSession(['banned' => false])`, and `get('/')`.

## Console Command Tests
The docs show console tests in Pest and PHPUnit:

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

Confirmed helpers: `$this->artisan(...)`, `expectsQuestion(...)`, `expectsOutput(...)`, `doesntExpectOutput(...)`, and `assertExitCode(...)`.

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

Confirmed helpers and classes: `Illuminate\Support\Facades\Cache`, `Cache::shouldReceive('get')`, `with('key')`, `andReturn('value')`, `$this->get('/cache')`, and `assertSee('value')`.

## Exception Reporting Tests
The docs show `Exceptions::fake()` and `Exceptions::assertReported(...)`:

```php
<?php

use App\Exceptions\InvalidOrderException;
use Illuminate\Support\Facades\Exceptions;

test('exception is thrown', function () {
    Exceptions::fake();

    $response = $this->get('/order/1');

    Exceptions::assertReported(InvalidOrderException::class);

    Exceptions::assertReported(function (InvalidOrderException $e) {
        return $e->getMessage() === 'The order was invalid.';
    });
});
```

```php
<?php

namespace Tests\Feature;

use App\Exceptions\InvalidOrderException;
use Illuminate\Support\Facades\Exceptions;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    /**
     * A basic test example.
     */
    public function test_exception_is_thrown(): void
    {
        Exceptions::fake();

        $response = $this->get('/');

        Exceptions::assertReported(InvalidOrderException::class);

        Exceptions::assertReported(function (InvalidOrderException $e) {
            return $e->getMessage() === 'The order was invalid.';
        });
    }
}
```

Confirmed helpers and classes: `App\Exceptions\InvalidOrderException`, `Illuminate\Support\Facades\Exceptions`, `Exceptions::fake()`, `Exceptions::assertReported(...)`, `$this->get(...)`, and `Tests\TestCase`.

## Time-Sensitive Tests
The docs show a Pest time travel example:

```php
use App\Models\Thread;

test('forum threads lock after one week of inactivity', function () {
    $thread = Thread::factory()->create();

    $this->travel(1)->week();

    expect($thread->isLockedByInactivity())->toBeTrue();
});
```

Confirmed helpers and classes: `App\Models\Thread`, `Thread::factory()->create()`, `$this->travel(1)->week()`, and `expect(...)->toBeTrue()`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using JSON assertions, redirect assertions, validation assertions, database refresh traits, database assertions, file uploads, storage fakes, queue fakes, event fakes, mail fakes, notification fakes, bus fakes, HTTP client fakes, browser tests, parallel testing, coverage, or test generation commands.
