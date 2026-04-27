# Collections

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x collections.

## Introduction
The docs state `Illuminate\Support\Collection` provides a fluent, convenient wrapper for working with arrays of data.

The docs state the `collect` helper creates a new collection instance from an array:

```php
$collection = collect([1, 2, 3]);
```

The docs state collections allow chaining methods to perform fluent mapping and reducing of the underlying array.

The docs state collections are generally immutable, meaning every `Collection` method returns an entirely new `Collection` instance.

The docs state collections can also be created using the `make` and `fromJson` methods.

The docs state Eloquent query results are always returned as `Collection` instances.

## Pluck
The docs state `pluck(...)` retrieves all values for a given key.

The docs show retrieving values:

```php
$collection = collect([
    ['product_id' => 'prod-100', 'name' => 'Desk'],
    ['product_id' => 'prod-200', 'name' => 'Chair'],
]);

$plucked = $collection->pluck('name');

$plucked->all();

// ['Desk', 'Chair']
```

The docs show keying results by another key:

```php
$plucked = $collection->pluck('name', 'product_id');

$plucked->all();

// ['prod-100' => 'Desk', 'prod-200' => 'Chair']
```

The docs state nested values can be retrieved using dot notation, as in `pluck('speakers.first_day')`.

The docs state if duplicate keys exist, the last matching item is inserted into the plucked collection.

## GroupBy
The docs state `groupBy(...)` groups collection items by a specified key or callback function.

The docs show grouping by key:

```php
$collection = collect([
    ['account_id' => 'account-x10', 'product' => 'Chair'],
    ['account_id' => 'account-x10', 'product' => 'Bookcase'],
    ['account_id' => 'account-x11', 'product' => 'Desk'],
]);

$grouped = $collection->groupBy('account_id');
```

The docs show grouping with a callback:

```php
$grouped = $collection->groupBy(function (array $item, int $key) {
    return substr($item['account_id'], -3);
});
```

The docs show multiple grouping criteria with `preserveKeys: true`:

```php
$result = $data->groupBy(['skill', function (array $item) {
    return $item['roles'];
}], preserveKeys: true);
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using collection methods not listed here, including `map`, `filter`, `reject`, `reduce`, `sortBy`, `values`, `each`, `contains`, `partition`, `pipe`, `when`, `unless`, macros, higher-order messages, collection serialization, or exact method return types beyond the snippets returned for this slice.
