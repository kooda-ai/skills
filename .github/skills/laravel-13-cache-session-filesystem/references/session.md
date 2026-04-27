# Session

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x session access and mutation.

## Retrieving Session Data From The Request
The docs show retrieving data from the HTTP session using an `Illuminate\Http\Request` instance:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\View\View;

class UserController extends Controller
{
    /**
     * Show the profile for the given user.
     */
    public function show(Request $request, string $id): View
    {
        $value = $request->session()->get('key');

        // ...

        $user = $this->users->find($id);

        return view('user.profile', ['user' => $user]);
    }
}
```

The docs show defaults for missing keys:

```php
$value = $request->session()->get('key', 'default');

$value = $request->session()->get('key', function () {
    return 'default';
});
```

Confirmed methods: `$request->session()` and `get(...)`.

## Global `session()` Helper
The docs show retrieving values and storing data with the global `session()` helper:

```php
Route::get('/home', function () {
    $value = session('key');
    $value = session('key', 'default');
    session(['key' => 'value']);
});
```

Confirmed helper behavior: `session('key')`, `session('key', 'default')`, and `session(['key' => 'value'])`.

## Storing And Modifying Session Data
The docs show:

```php
$request->session()->put('key', 'value');
$request->session()->push('user.teams', 'developers');
$value = $request->session()->pull('key', 'default');
```

Confirmed methods: `put(...)`, `push(...)`, and `pull(...)`.

## Flash Data
The docs show short-lived session data methods:

```php
$request->session()->flash('status', 'Task was successful!');
$request->session()->reflash();
$request->session()->keep(['username', 'email']);
$request->session()->now('status', 'Task was successful!');
```

Confirmed methods: `flash(...)`, `reflash()`, `keep(...)`, and `now(...)`.

## Deleting Session Data
The docs show removing specific keys and clearing all session data:

```php
$request->session()->forget('name');
$request->session()->forget(['name', 'status']);
$request->session()->flush();
```

Confirmed methods: `forget(...)` and `flush()`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `all`, `has`, `missing`, `exists`, `regenerate`, `invalidate`, CSRF/session security behavior, session blocking, driver configuration, custom session drivers, cookie behavior, session testing helpers, or session middleware behavior.
