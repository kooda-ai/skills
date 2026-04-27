# Exception Handling

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x error and exception handling.

## Exception Configuration
The docs state that when starting a new Laravel project, error and exception handling is already configured.

The docs state exception handling can be managed with the `withExceptions` method in `bootstrap/app.php`.

The docs state the `$exceptions` object provided to the `withExceptions` closure is an instance of `Illuminate\Foundation\Configuration\Exceptions`.

## Custom Reporting In Bootstrap
The docs show custom reporting logic for a specific exception type:

```php
use App\Exceptions\InvalidOrderException;

->withExceptions(function (Exceptions $exceptions): void {
    $exceptions->report(function (InvalidOrderException $e) {
        // ...
    });
});
```

The docs show stopping default logging propagation with `stop()` or by returning `false`:

```php
use App\Exceptions\InvalidOrderException;

->withExceptions(function (Exceptions $exceptions): void {
    $exceptions->report(function (InvalidOrderException $e) {
        // ...
    })->stop();

    $exceptions->report(function (InvalidOrderException $e) {
        return false;
    });
});
```

Run a fresh lookup before adding the exact import for the `Exceptions` type in this snippet.

## Report And Render Methods On Exceptions
The docs show exception classes with `report()` and `render(...)` methods:

```php
<?php

namespace App\Exceptions;

use Exception;
use Illuminate\Http\Request;
use Illuminate\Http\Response;

class InvalidOrderException extends Exception
{
    /**
     * Report the exception.
     */
    public function report(): void
    {
        // ...
    }

    /**
     * Render the exception as an HTTP response.
     */
    public function render(Request $request): Response
    {
        return response(/* ... */);
    }
}
```

The docs show returning `false` from `render(...)` to fall back to default behavior:

```php
/**
 * Render the exception as an HTTP response.
 */
public function render(Request $request): Response|bool
{
    if (/* Determine if the exception needs custom rendering */) {

        return response(/* ... */);
    }

    return false;
}
```

The docs show returning `true` or `false` from `report()` depending on whether custom reporting should apply:

```php
/**
 * Report the exception.
 */
public function report(): bool
{
    if (/* Determine if the exception needs custom reporting */) {

        // ...

        return true;
    }

    return false;
}
```

## Exception Log Levels
The docs show mapping exception classes to custom PSR-3 log levels with `$exceptions->level(...)`:

```php
->withExceptions(function (Exceptions $exceptions): void {
    $exceptions->level(PDOException::class, LogLevel::CRITICAL);
})
```

The returned Context7 snippet had malformed namespace formatting for the `LogLevel` import. Run a fresh lookup before writing the exact imports for this example.

## Reporting Ignored Framework Exceptions
The docs show using `stopIgnoring(...)` to re-enable reporting for exception types Laravel ignores by default, such as HTTP exceptions:

```php
->withExceptions(function (Exceptions $exceptions): void {
    $exceptions->stopIgnoring(HttpException::class);
})
```

The returned Context7 snippet had malformed namespace formatting for the `HttpException` import. Run a fresh lookup before writing the exact import for this example.

## Manual Reporting
The docs show the `report` helper logging an exception without interrupting the request lifecycle:

```php
public function isValid(string $value): bool
{
    try {
        // Validate the value...
    } catch (Throwable $e) {
        report($e);

        return false;
    }
}
```

Run a fresh lookup before writing the exact import for `Throwable`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `dontReport()`, `ShouldntReport`, `dontReportDuplicates()`, exception throttling, exception context, `shouldRenderJsonWhen()`, render callbacks in `bootstrap/app.php`, JSON exception rendering, validation exception behavior, exact imports for malformed snippets, or exception handling APIs not listed here.
