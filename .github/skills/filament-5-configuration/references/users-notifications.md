# Users, Authentication, and Notifications Configuration

Use this reference after a fresh Context7 lookup for the exact Filament 5 users, authentication, or notification configuration topic.

## Panel Access
- By default, all `App\Models\User` records can access Filament locally.
- To allow access in non-local environments, implement `Filament\Models\Contracts\FilamentUser` on the User model.
- `canAccessPanel(Panel $panel): bool` returns whether the user may access that panel.

```php
use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser
{
    public function canAccessPanel(Panel $panel): bool
    {
        return str_ends_with($this->email, '@yourdomain.com') && $this->hasVerifiedEmail();
    }
}
```

- Because `canAccessPanel()` receives the current panel, the docs show checking `$panel->getId() === 'admin'` for panel-specific access logic.
- Resource access is handled through Resource authorization, not the panel access contract.

## User Name and Avatars
- By default, Filament uses the `name` attribute of the user.
- Customize the displayed user name by implementing `Filament\Models\Contracts\HasName` and `getFilamentName(): string`.
- Out of the box, Filament uses `ui-avatars.com` to generate avatars from the user's name.
- If the user model has an `avatar_url` attribute, that is used instead.
- Customize the current user's avatar URL by implementing `Filament\Models\Contracts\HasAvatar` and `getFilamentAvatarUrl(): ?string`.
- If `getFilamentAvatarUrl()` returns `null`, Filament falls back to `ui-avatars.com`.
- Register a custom avatar provider with `defaultAvatarProvider(BoringAvatarsProvider::class)`.
- A custom provider implements `Filament\AvatarProviders\Contracts\AvatarProvider`; its `get()` method accepts a user model instance and returns an avatar URL.

## Authentication Features
- Enable authentication features in panel configuration:

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

- Authentication methods can receive custom Filament page classes.
- The docs show customizing the profile page with `profile(EditProfile::class)` where `EditProfile` extends `Filament\Auth\Pages\EditProfile`.
- Other documented base page classes are `Filament\Auth\Pages\Login`, `Filament\Auth\Pages\Register`, `Filament\Auth\Pages\EmailVerification\EmailVerificationPrompt`, `Filament\Auth\Pages\PasswordReset\RequestPasswordReset`, and `Filament\Auth\Pages\PasswordReset\ResetPassword`.
- A custom profile page can override `form(Schema $schema): Schema` using `Filament\Schemas\Schema`.
- Authentication page components can call documented helpers such as `getNameFormComponent()`, `getEmailFormComponent()`, `getPasswordFormComponent()`, and `getPasswordConfirmationFormComponent()`.
- To customize one authentication field without redefining a whole form, extend a component method and return `parent::getPasswordFormComponent()->revealable(false)`.
- If using `profile()` with `emailChangeVerification()`, users must verify the new email before they can log in with it; the database email is not updated until the verification link is clicked.
- The email-change verification link is valid for 60 minutes, and the old email address receives a blocking link.
- Make the profile page use the standard page layout with sidebar by calling `profile(isSimple: false)`.

## Auth Routes, Guard, Broker, and Password Inputs
- Customize authentication route slugs with:

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

- Set the authentication guard with `authGuard('web')`.
- Set the password broker with `authPasswordBroker('users')`.
- Disable revealable password inputs globally with `revealablePasswords(false)`.
- The docs also confirm disabling a single password field with `revealable(false)` when extending a base auth page class.

## Guest Access
- By default, Filament expects authenticated users only.
- To allow guests, the docs say to avoid components that expect a signed-in user, such as profiles and avatars.
- Remove the default `Authenticate::class` from the `authMiddleware()` array.
- Remove `login()` and other authentication features from the panel.
- Remove the default `AccountWidget` from `widgets()` because it reads the current user's data.
- For guest read access in policies, the docs say Laravel model policy `viewAny()` and `view()` methods can use an optional `?User $user` parameter and return `true`, or those methods can be removed from the policy entirely.

## Database Notifications
- Before using database notifications, add Laravel's notifications table with `php artisan make:notifications-table`.
- For PostgreSQL, the docs say the `data` column in the migration should use `json()`: `$table->json('data')`.
- For UUID user models, the docs say the `notifiable` column should use `uuidMorphs()`: `$table->uuidMorphs('notifiable')`.
- Enable database notifications in a panel with `databaseNotifications()`.
- By default, the database notifications trigger is positioned in the topbar. If the topbar is disabled, it is added to the sidebar.
- Always move the trigger to the sidebar with `databaseNotifications(position: DatabaseNotificationsPosition::Sidebar)` using `Filament\Enums\DatabaseNotificationsPosition`.
- Without additional setup, new database notifications are only received when the page first loads.
- Poll for new database notifications with `databaseNotificationsPolling('30s')` after `databaseNotifications()`.
- The docs state Livewire polls every 30 seconds by default.
- Disable database notification polling with `databaseNotificationsPolling(null)`.
- Open the database notifications modal from anywhere by dispatching an `open-modal` browser event with `{ id: 'database-notifications' }`.

## Broadcast Notifications and Websockets
- Filament sends flash notifications via the Laravel session by default.
- Broadcast notifications use Laravel Echo and require Echo plus a server-side websockets integration such as Pusher.
- To set up websockets in a panel, the docs say to read Laravel broadcasting docs, install and configure server-side websockets, publish Filament config with `php artisan vendor:publish --tag=filament-config`, edit `config/filament.php` and uncomment `broadcasting.echo`, ensure the relevant `VITE_*` entries exist in `.env`, then clear route and config caches with `php artisan route:clear` and `php artisan config:clear`.
- If Echo credentials are set in `config/filament.php`, Laravel Echo automatically connects for every panel by default.
- Disable automatic Echo connection in a panel with `broadcasting(false)`.