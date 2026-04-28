# Auth, Profiles, And Impersonation

## Authentication Surfaces
- Wave authentication is built on DevDojo Auth.
- Auth customization is documented at `/auth/setup`.
- The built-in auth surfaces listed in the docs are login, registration, verify email, password confirmation, password reset/request, and two-factor challenge.
- Login is documented at `/auth/login`.
- Social providers are toggled from `/auth/setup/providers`.
- Email verification is toggled from `/auth/setup/settings`.

## Registration And Access
- The docs say `subscribed` middleware may be used instead of adding both `auth` and `subscribed`.
- The auth docs show a `User` model `boot()` example that generates a username and assigns `config('wave.default_user_role', 'registered')` on creation.

## Profiles
- Public profiles are documented at `/profile/{username}`.
- Profile pages use the app layout for authenticated users and the marketing layout for guests.
- The docs show disabling profiles with `Route::redirect('profile/{username}', '/');` placed after `Wave::routes();`.
- Profile settings let users update avatar, name, email, and custom profile fields.
- Custom profile fields are configured in `config/profiles.php`.
- Field values can be read with `auth()->user()->profile('occupation')`.

## Impersonation
- User impersonation is managed from `/admin/users`.
- The docs show an Impersonate action and a Leave Impersonation action in the user menu.
