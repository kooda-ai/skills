# Starter Kits, Login, and Logout

## Starter-Kit Authentication Scaffolding
- The Laravel 13 authentication docs say application starter kits offer a rapid way to scaffold an entire authentication system.
- The starter-kit docs state these kits include the routes, controllers, and views required for user registration and authentication.
- The docs state that after installing a starter kit in a fresh application and running database migrations, registration and login functionality are immediately available.
- The starter-kit docs state these kits use Laravel Fortify for authentication logic.
- The docs describe starter kits as both a fast starting point and a practical reference for custom authentication flows.

## Manual Login Attempt
The authentication docs show a controller method for handling an authentication attempt:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Http\RedirectResponse;
use Illuminate\Support\Facades\Auth;

class LoginController extends Controller
{
    /**
     * Handle an authentication attempt.
     */
    public function authenticate(Request $request): RedirectResponse
    {
        $credentials = $request->validate([
            'email' => ['required', 'email'],
            'password' => ['required'],
        ]);

        if (Auth::attempt($credentials)) {
            $request->session()->regenerate();

            return redirect()->intended('dashboard');
        }

        return back()->withErrors([
            'email' => 'The provided credentials do not match our records.',
        ])->onlyInput('email');
    }
}
```

Confirmed methods and helpers: `Auth::attempt(...)`, `$request->session()->regenerate()`, `redirect()->intended('dashboard')`, `back()->withErrors(...)`, and `onlyInput('email')`.

## Logout Flow
The authentication docs show a logout method that removes authentication state and rotates session state:

```php
use Illuminate\Http\Request;
use Illuminate\Http\RedirectResponse;
use Illuminate\Support\Facades\Auth;

public function logout(Request $request): RedirectResponse
{
    Auth::logout();
    $request->session()->invalidate();
    $request->session()->regenerateToken();

    return redirect('/');
}
```

The docs recommend invalidating the session and regenerating the CSRF token in addition to calling `Auth::logout()`.

## Boundaries
- Do not invent starter-kit installation flags, generated file inventories, Fortify callback APIs, session guard configuration, or Breeze/Jetstream internals unless a fresh lookup confirms them.
- Keep generic `Auth` facade helpers such as `login()`, `loginUsingId()`, `user()`, and `id()` in the broader auth slice when the task is not specifically about account flows.
