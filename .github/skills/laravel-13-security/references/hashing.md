# Hashing

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x hashing.

## Purpose And Drivers
The docs state the `Hash` facade provides secure Bcrypt and Argon2 hashing for storing user passwords.

The docs state Bcrypt is used by default for registration and authentication when using Laravel application starter kits.

The docs state Laravel uses the `bcrypt` hashing driver by default.

The docs state supported hashing drivers include `bcrypt`, `argon`, and `argon2id`.

The docs state the application's hashing driver may be specified using the `HASH_DRIVER` environment variable.

The docs state the full `hashing` configuration file may be published using the `config:publish` Artisan command when customizing all hashing driver options.

## Hashing Passwords
The docs show hashing a password before storing it:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;

class PasswordController extends Controller
{
    public function update(Request $request): RedirectResponse
    {
        $request->user()->fill([
            'password' => Hash::make($request->newPassword)
        ])->save();

        return redirect('/profile');
    }
}
```

Confirmed import: `Illuminate\Support\Facades\Hash`.

## Verifying Passwords
The docs show comparing plain text against an existing hash:

```php
if (Hash::check('plain-text', $hashedPassword)) {
    // The passwords match...
}
```

## Rehashing Passwords
The docs show detecting whether current hash algorithm settings require a stored hash update:

```php
if (Hash::needsRehash($hashed)) {
    $hashed = Hash::make('plain-text');
}
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using per-driver option names, `Hash::driver()`, `isHashed`, custom hashers, algorithm verification behavior, password validation rules, starter-kit internals, or authentication flow behavior beyond the returned snippets.