# Password Confirmation

## Confirmation Form Route
The authentication docs show the route that displays the confirmation form:

```php
Route::get('/confirm-password', function () {
    return view('auth.confirm-password');
})->middleware('auth')->name('password.confirm');
```

## Confirmation Submission Route
The authentication docs show the route that verifies the submitted password:

```php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;

Route::post('/confirm-password', function (Request $request) {
    if (! Hash::check($request->password, $request->user()->password)) {
        return back()->withErrors([
            'password' => ['The provided password does not match our records.']
        ]);
    }

    $request->session()->passwordConfirmed();

    return redirect()->intended();
})->middleware(['auth', 'throttle:6,1']);
```

Confirmed methods and helpers: `Hash::check(...)`, `$request->session()->passwordConfirmed()`, `back()->withErrors(...)`, and `redirect()->intended()`.

## Protecting Sensitive Routes
The authentication docs show protecting routes with the `password.confirm` middleware alias:

```php
Route::get('/settings', function () {
    // ...
})->middleware(['password.confirm']);

Route::post('/settings', function () {
    // ...
})->middleware(['password.confirm']);
```

The docs state the middleware stores the intended destination in the session, redirects the user to the `password.confirm` named route when confirmation is required, and returns the user to the intended location after success.

## Boundaries
- Run a fresh lookup before using the exact `config/auth.php` `password_timeout` statement, custom timeout values, middleware internals, or password-confirmation view details beyond the returned routes.
- Do not infer starter-kit implementation details for confirmation screens from the framework route examples alone.
