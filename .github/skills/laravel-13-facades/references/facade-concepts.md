# Facade Concepts

Sources used: Current Laravel 13.x documentation page for facades.

## Introduction And Namespace
The docs describe facades as a static-looking interface to classes available in Laravel's service container.

The docs state Laravel facades are in the `Illuminate\Support\Facades` namespace.

The docs show a basic facade import and use pattern:

```php
use Illuminate\Support\Facades\Cache;
use Illuminate\Support\Facades\Route;

Route::get('/cache', function () {
    return Cache::get('key');
});
```

## Facades Vs Dependency Injection
The docs say one benefit of dependency injection is that implementations can be swapped during testing.

The docs explain that although facades look static, they can still be tested because facade calls proxy to objects resolved from the service container.

The docs show facade testing with `shouldReceive(...)`:

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

The docs also warn about class scope creep: because facades are easy to use, a class can quietly grow too large if it keeps accumulating facade calls.

## Facades Vs Helper Functions
The docs explain that helper functions often correspond to facade calls.

The docs show a `Response` facade call and the equivalent helper call:

```php
use Illuminate\Support\Facades\Response;

Route::get('/users', function () {
    return Response::json([
        // ...
    ]);
});

Route::get('/users', function () {
    return response()->json([
        // ...
    ]);
});
```

The docs also show a helper example using `cache('key')` and state there is no practical difference between the helper and the corresponding facade call.

## How Facades Work
The docs state that Laravel facades extend `Illuminate\Support\Facades\Facade`.

The docs explain that the base `Facade` class uses `__callStatic()` to defer the facade call to an object resolved from the container.

The docs show the `Cache` facade accessor pattern:

```php
class Cache extends Facade
{
    /**
     * Get the registered name of the component.
     */
    protected static function getFacadeAccessor(): string
    {
        return 'cache';
    }
}
```

The docs explain that when a static method is called on the facade, Laravel resolves the binding named by `getFacadeAccessor()` from the service container and executes the requested method on that object.

## Topics Requiring Fresh Lookup
Run a new documentation lookup before using custom facade classes, facade aliases outside the shown imports, helper behavior beyond the documented comparisons, or mocking patterns not shown on the Laravel 13 facades page.