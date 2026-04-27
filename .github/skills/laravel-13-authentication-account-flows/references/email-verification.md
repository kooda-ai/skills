# Email Verification

## User Model Contract
The verification docs show the user model implementing `MustVerifyEmail`:

```php
<?php

namespace App\Models;

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;

class User extends Authenticatable implements MustVerifyEmail
{
    use Notifiable;

    // ...
}
```

## Verification Notice Route
The verification docs show the route that tells the user to check their inbox:

```php
Route::get('/email/verify', function () {
    return view('auth.verify-email');
})->middleware('auth')->name('verification.notice');
```

## Verification Handler Route
The verification docs show the signed verification handler:

```php
use Illuminate\Foundation\Auth\EmailVerificationRequest;

Route::get('/email/verify/{id}/{hash}', function (EmailVerificationRequest $request) {
    $request->fulfill();

    return redirect('/home');
})->middleware(['auth', 'signed'])->name('verification.verify');
```

The docs state `fulfill()` marks the authenticated user as verified.

## Resend Verification Route
The verification docs show the resend endpoint:

```php
use Illuminate\Http\Request;

Route::post('/email/verification-notification', function (Request $request) {
    $request->user()->sendEmailVerificationNotification();

    return back()->with('message', 'Verification link sent!');
})->middleware(['auth', 'throttle:6,1'])->name('verification.send');
```

## Verified Middleware
The verification docs show restricting routes to verified users:

```php
Route::get('/profile', function () {
    // Only verified users may access this route...
})->middleware(['auth', 'verified']);
```

## Boundaries
- Run a fresh lookup before adding the exact `Verified` event import, verification-notification customization, custom email templates, middleware internals, or starter-kit verification UI details beyond the documented routes.
- Do not infer package-specific verification behavior from Breeze, Jetstream, or Fortify without package docs.
