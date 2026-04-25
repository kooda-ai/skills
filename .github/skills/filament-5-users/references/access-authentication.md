# Access and Authentication

Use this reference after a fresh Context7 lookup for the exact Filament 5 user access or authentication topic.

## Creating Panel Users
- Create a user account for accessing a Filament panel with:

```bash
php artisan make:filament-user
```

## Panel Access
- By default, all users can access Filament locally.
- In any environment other than local, Filament requires the User model to implement `Filament\Models\Contracts\FilamentUser`; otherwise users are unable to sign in.
- `canAccessPanel(Panel $panel): bool` determines whether a user can access a panel.

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser
{
    // ...

    public function canAccessPanel(Panel $panel): bool
    {
        return str_ends_with($this->email, '@yourdomain.com') && $this->hasVerifiedEmail();
    }
}
```

- For multiple panels, the docs show checking the panel ID:

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser
{
    // ...

    public function canAccessPanel(Panel $panel): bool
    {
        if ($panel->getId() === 'admin') {
            return str_ends_with($this->email, '@yourdomain.com') && $this->hasVerifiedEmail();
        }

        return true;
    }
}
```

## Authentication Features
- Enable panel authentication features with documented panel methods:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->login()
        ->registration()
        ->passwordReset()
        ->emailVerification()
        ->emailChangeVerification()
        ->profile();
}
```

- The docs state that authentication pages can be customized by creating custom Filament page classes and passing them to the relevant panel configuration method.
- Context7 confirmed the custom profile page example below; do not invent unconfirmed examples for other auth pages.

```php
<?php

namespace App\Filament\Pages\Auth;

use Filament\Auth\Pages\EditProfile as BaseEditProfile;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Schema;

class EditProfile extends BaseEditProfile
{
    public function form(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('username')
                    ->required()
                    ->maxLength(255),
                $this->getNameFormComponent(),
                $this->getEmailFormComponent(),
                $this->getPasswordFormComponent(),
                $this->getPasswordConfirmationFormComponent(),
            ]);
    }
}
```

```php
use App\Filament\Pages\Auth\EditProfile;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->profile(EditProfile::class);
}
```

- Make the profile page use the standard page layout with sidebar by calling `profile(isSimple: false)`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->profile(isSimple: false);
}
```

## Email Change Verification
- When `emailChangeVerification()` is enabled with `profile()`, users changing their email address must verify the new address before the change takes effect.
- The database email is updated only after verification.
- The new address receives a verification email, and the old address receives a confirmation email with a link to block the change.
- Context7 returned that the verification link is valid for 60 minutes.

## Auth Routes, Guard, Broker, and Password Inputs
- Customize authentication route slugs and prefixes with:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->loginRouteSlug('login')
        ->registrationRouteSlug('register')
        ->passwordResetRoutePrefix('password-reset')
        ->passwordResetRequestRouteSlug('request')
        ->passwordResetRouteSlug('reset')
        ->emailVerificationRoutePrefix('email-verification')
        ->emailVerificationPromptRouteSlug('prompt')
        ->emailVerificationRouteSlug('verify')
        ->emailChangeVerificationRoutePrefix('email-change-verification')
        ->emailChangeVerificationRouteSlug('verify');
}
```

- Set the authentication guard with:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->authGuard('web');
}
```

- Set the password broker with:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->authPasswordBroker('users');
}
```

- Disable revealable password inputs globally with:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->revealablePasswords(false);
}
```

- Customize a specific auth password field by overriding the component method:

```php
use Filament\Schemas\Components\Component;

protected function getPasswordFormComponent(): Component
{
    return parent::getPasswordFormComponent()
        ->revealable(false);
}
```

## Guest Access
- To allow guests to access a panel, the docs say to avoid components that require an authenticated user.
- Remove `Authenticate::class` from `authMiddleware()`.
- Remove authentication features such as `login()`.
- Remove widgets such as `AccountWidget` that display user data.

## Resource Authorization Boundary
- Panel access uses `FilamentUser` and `canAccessPanel()`.
- Resource CRUD authorization is handled by Resource authorization and Laravel model policies, such as `viewAny()`, `create()`, `update()`, and `delete()`.
- For Resource implementation details, load the Filament 5 Resources skill after confirming the Users touchpoint.
