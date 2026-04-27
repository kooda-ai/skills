# Database Access And Transactions

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x database access, raw SQL selection, raw expressions, and manual transactions.

## Raw Select Queries
The docs show a basic raw `SELECT` query using the `DB` facade:

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
        $users = DB::select('select * from users where active = ?', [1]);

        return view('user.index', ['users' => $users]);
    }
}
```

The docs state `DB::select(...)` takes the SQL query and parameter bindings as arguments, protects against SQL injection, and returns an array of `stdClass` objects.

## Manual Transactions
The docs show manual transaction control with the `DB` facade:

```php
use Illuminate\Support\Facades\DB;

DB::beginTransaction();
// ... operations
DB::commit();
// OR
DB::rollBack();
```

Confirmed transaction methods: `DB::beginTransaction()`, `DB::commit()`, and `DB::rollBack()`.

## Raw Expressions Boundary
The query builder reference includes raw expression methods such as `DB::raw(...)`, `selectRaw(...)`, `whereRaw(...)`, `havingRaw(...)`, `orderByRaw(...)`, and `groupByRaw(...)`. The docs say to use caution to prevent SQL injection vulnerabilities.

Prefer documented binding examples when raw methods accept bindings, such as:

```php
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
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using database configuration, SQLite defaults, multiple connections, read/write connections, `DB::connection(...)`, `DB::insert`, `DB::update`, `DB::delete`, `DB::statement`, transaction closure helpers, transaction retries, deadlock handling, query listeners, query monitoring, database inspection commands, or CLI database shells.
