# Query Builder

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x query builder retrieval, filtering, raw expressions, inserts, updates, deletes, aggregates, limits, and offsets.

## Introduction
The docs describe Laravel's database query builder as a fluent interface for creating and running database queries. It can perform most database operations and works with all supported database systems.

The docs state Laravel's query builder uses PDO parameter binding to protect the application against SQL injection attacks for query bindings, and that strings passed as query bindings do not need to be cleaned or sanitized.

## Retrieving Rows
The docs show using `DB::table(...)->get()`:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Support\Facades\DB;
use Illuminate\View\View;

class UserController extends Controller
{
    /**
     * Show a list of all of the application's users.
     */
    public function index(): View
    {
        $users = DB::table('users')->get();

        return view('user.index', ['users' => $users]);
    }
}
```

The docs say the `table` method on the `DB` facade begins a query and returns a fluent query builder instance for the given table. The `get` method retrieves results, and each result is an instance of PHP's `stdClass` object whose column values can be accessed as object properties.

## Basic Where Clauses
The docs show chained `where` calls:

```php
$users = DB::table('users')
    ->where('votes', '=', 100)
    ->where('age', '>', 35)
    ->get();
```

The docs show shorthand equality:

```php
$users = DB::table('users')->where('votes', 100)->get();
```

The docs show associative array conditions:

```php
$users = DB::table('users')->where([
    'first_name' => 'Jane',
    'last_name' => 'Doe',
])->get();
```

The docs show comparison and pattern operators:

```php
$users = DB::table('users')
    ->where('votes', '>=', 100)
    ->get();

$users = DB::table('users')
    ->where('votes', '<>', 100)
    ->get();

$users = DB::table('users')
    ->where('name', 'like', 'T%')
    ->get();
```

The docs show an array of condition arrays:

```php
$users = DB::table('users')->where([
    ['status', '=', '1'],
    ['subscribed', '<>', '1'],
])->get();
```

## Logical Grouping
The docs show grouping where clauses with a closure. The closure receives a query builder instance:

```php
$users = DB::table('users')
    ->where('name', '=', 'John')
    ->where(function (Builder $query) {
        $query->where('votes', '>', 100)
            ->orWhere('title', '=', 'Admin');
    })
    ->get();
```

The docs specifically call out grouping as useful with `orWhere` to prevent unexpected query behavior. Run a narrower lookup before adding the exact import for `Builder` in `DB::table()` examples, since the current result did not include it in this snippet.

## Subquery Where Clauses
The docs show subquery where clauses using closures:

```php
use App\Models\User;
use Illuminate\Database\Query\Builder;

$users = User::where(function (Builder $query) {
    $query->select('type')
        ->from('membership')
        ->whereColumn('membership.user_id', 'users.id')
        ->orderByDesc('membership.start_date')
        ->limit(1);
}, 'Pro')->get();

use App\Models\Income;

$incomes = Income::where('amount', '<', function (Builder $query) {
    $query->selectRaw('avg(i.amount)')->from('incomes as i');
})->get();
```

Confirmed methods from this snippet include `select(...)`, `from(...)`, `whereColumn(...)`, `orderByDesc(...)`, `limit(...)`, and `selectRaw(...)`.

## Raw Expressions
The docs show `DB::raw(...)` and raw query builder methods. The docs say to use caution to prevent SQL injection vulnerabilities:

```php
$users = DB::table('users')
    ->select(DB::raw('count(*) as user_count, status'))
    ->where('status', '<>', 1)
    ->groupBy('status')
    ->get();

$orders = DB::table('orders')
    ->selectRaw('price * ? as price_with_tax', [1.0825])
    ->get();

$orders = DB::table('orders')
    ->whereRaw('price > IF(state = "TX", ?, 100)', [200])
    ->get();

$orders = DB::table('orders')
    ->select('department', DB::raw('SUM(price) as total_sales'))
    ->groupBy('department')
    ->havingRaw('SUM(price) > ?', [2500])
    ->get();

$orders = DB::table('orders')
    ->orderByRaw('updated_at - created_at DESC')
    ->get();

$orders = DB::table('orders')
    ->select('city', 'state')
    ->groupByRaw('city, state')
    ->get();
```

Confirmed raw methods: `DB::raw(...)`, `selectRaw(...)`, `whereRaw(...)`, `havingRaw(...)`, `orderByRaw(...)`, and `groupByRaw(...)`.

## Inserts
The docs show single and multiple record inserts:

```php
DB::table('users')->insert([
    'email' => 'kayla@example.com',
    'votes' => 0
]);
```

```php
DB::table('users')->insert([
    ['email' => 'picard@example.com', 'votes' => 0],
    ['email' => 'janeway@example.com', 'votes' => 0],
]);
```

The docs show `insertOrIgnore(...)`:

```php
DB::table('users')->insertOrIgnore([
    ['id' => 1, 'email' => 'sisko@example.com'],
    ['id' => 2, 'email' => 'archer@example.com'],
]);
```

The docs show `insertUsing(...)`:

```php
DB::table('pruned_users')->insertUsing([
    'id', 'name', 'email', 'email_verified_at'
], DB::table('users')->select(
    'id', 'name', 'email', 'email_verified_at'
)->where('updated_at', '<=', now()->minus(months: 1)));
```

The docs show `insertGetId(...)`:

```php
$id = DB::table('users')->insertGetId(
    ['email' => 'john@example.com', 'votes' => 0]
);
```

## Updates And Deletes
The docs show `update(...)`, returning the number of affected rows:

```php
$affected = DB::table('users')
    ->where('id', 1)
    ->update(['votes' => 1]);
```

The docs show `delete(...)`, returning the number of affected rows:

```php
$deleted = DB::table('users')->delete();
```

```php
$deleted = DB::table('users')->where('votes', '>', 100)->delete();
```

## Aggregates, Limit, And Offset
The docs show aggregate methods:

```php
use Illuminate\Support\Facades\DB;

$count = DB::table('users')->count();
$maxPrice = DB::table('orders')->max('price');

// With constraints
$avgPrice = DB::table('orders')->where('finalized', 1)->avg('price');
```

Confirmed aggregate methods from the docs: `count()`, `max(...)`, `min(...)`, `avg(...)`, and `sum(...)`. The current returned snippet shows `count()`, `max(...)`, and `avg(...)` concretely.

The docs show `offset(...)` and `limit(...)`:

```php
<?php

// Skip the first 10 users and return the next 5
$users = DB::table('users')
            ->offset(10)
            ->limit(5)
            ->get();
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `first`, `value`, `find`, `pluck`, `select` details, joins, unions, ordering helpers such as `orderBy` / `latest` / `oldest`, random ordering, chunking, lazy collections, cursors, JSON where clauses, full-text where clauses, locking, `exists`, `doesntExist`, `updateOrInsert`, `upsert`, `increment`, `decrement`, pagination, or query builder macros.
