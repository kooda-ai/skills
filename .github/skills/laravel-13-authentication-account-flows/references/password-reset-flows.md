# Password Reset Flows

## Reset-Link Request Form
The password-reset docs show the guest-only route that displays the reset-link request form:

```php
Route::get('/forgot-password', function () {
    return view('auth.forgot-password');
})->middleware('guest')->name('password.request');
```

## Reset-Link Submission Boundary
- The current Laravel 13 docs context confirms that handling the forgot-password form submission validates the user's email address and uses the `Password` facade's `sendResetLink(...)` method.
- The docs state `sendResetLink(...)` returns a status slug that may be translated using Laravel localization helpers and password language lines.
- The current Context7 result did not return the exact route code block for the POST handler, so run a fresh lookup before writing the exact `Route::post('/forgot-password', ...)` snippet.

## Reset Form Route
The password-reset docs show the guest-only route that displays the reset form after the user clicks the emailed link:

```php
Route::get('/reset-password/{token}', function (string $token) {
    return view('auth.reset-password', ['token' => $token]);
})->middleware('guest')->name('password.reset');
```

## Reset Submission Route
The password-reset docs show the route that validates input and updates the password:

```php
use App\Models\User;
use Illuminate\Auth\Events\PasswordReset;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\Password;
use Illuminate\Support\Str;

Route::post('/reset-password', function (Request $request) {
    $request->validate([
        'token' => 'required',
        'email' => 'required|email',
        'password' => 'required|min:8|confirmed',
    ]);

    $status = Password::reset(
        $request->only('email', 'password', 'password_confirmation', 'token'),
        function (User $user, string $password) {
            $user->forceFill([
                'password' => Hash::make($password)
            ])->setRememberToken(Str::random(60));

            $user->save();

            event(new PasswordReset($user));
        }
    );

    return $status === Password::PasswordReset
        ? redirect()->route('login')->with('status', __($status))
        : back()->withErrors(['email' => [__($status)]]);
})->middleware('guest')->name('password.update');
```

Confirmed methods and classes: `Password::reset(...)`, `Hash::make(...)`, `setRememberToken(...)`, `event(new PasswordReset(...))`, `redirect()->route('login')`, `with('status', __($status))`, and `back()->withErrors(...)`.

## Boundaries
- Do not invent the exact forgot-password POST route block, custom brokers, password-broker configuration, notification customization, or password-reset view internals unless a fresh lookup confirms them.
- Do not infer reset-table or cache-driver configuration from this account-flow slice unless the task is specifically about password broker configuration.
