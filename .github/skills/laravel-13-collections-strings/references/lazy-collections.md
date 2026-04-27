# Lazy Collections

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x lazy collections, Eloquent cursors, and query builder lazy streaming.

## LazyCollection From A Generator
The docs state `LazyCollection` leverages PHP generators to process large datasets efficiently and minimize memory usage.

The docs show creating a lazy collection from a generator:

```php
use App\Models\LogEntry;
use Illuminate\Support\LazyCollection;

LazyCollection::make(function () {
    $handle = fopen('log.txt', 'r');

    while (($line = fgets($handle)) !== false) {
        yield $line;
    }

    fclose($handle);
})->chunk(4)->map(function (array $lines) {
    return LogEntry::fromLines($lines);
})->each(function (LogEntry $logEntry) {
    // Process the log entry...
});
```

Confirmed import: `Illuminate\Support\LazyCollection`.

## Eloquent Cursor LazyCollection
The docs show using Eloquent `cursor()` with lazy filtering:

```php
use App\Models\User;

$users = User::cursor()->filter(function (User $user) {
    return $user->id > 500;
});

foreach ($users as $user) {
    echo $user->id;
}
```

The docs state `cursor()` returns a `LazyCollection` and loads only one model at a time instead of loading all models into memory.

The docs state collection methods like `filter` can be applied to a `LazyCollection` obtained from `cursor()` while maintaining low memory usage per model.

## Converting Collections To Lazy Collections
The docs show `lazy()` returning a `LazyCollection` instance:

```php
$lazyCollection = collect([1, 2, 3, 4])->lazy();
```

The docs show chaining `lazy()` with collection-style filters and `count()`:

```php
$count = $hugeCollection
    ->lazy()
    ->where('country', 'FR')
    ->where('balance', '>', '100')
    ->count();
```

## Query Builder Lazy Streams
The query builder docs state `lazy()` and `lazyById()` return a `LazyCollection` and allow large datasets to be iterated as a single stream.

The docs show streaming query builder results:

```php
use Illuminate\Support\Facades\DB;

DB::table('users')->orderBy('id')->lazy()->each(function (object $user) {
    // Process user
});
```

The docs show `lazyById()` when modifying records during iteration:

```php
DB::table('users')->where('active', false)
    ->lazyById()->each(function (object $user) {
        DB::table('users')->where('id', $user->id)->update(['active' => true]);
    });
```

The docs state `lazyById()` should be used when modifying records to ensure consistent iteration.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using lazy collection methods not listed here, `chunkWhile`, cursor pagination interactions, generator cleanup behavior beyond the returned file example, database cursor limitations, Eloquent relationship behavior while streaming, or memory guarantees beyond the returned documentation statements.
