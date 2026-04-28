---
name: wave-auth-users
description: 'Use when: working with Wave authentication, DevDojo Auth in Wave, auth setup pages, login, registration, email verification toggles, social auth toggles, password confirmation middleware in Wave docs, user profiles, custom profile fields, profile routes, and user impersonation. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave auth, profile, user settings, custom profile fields, or impersonation task'
---

# Wave Auth And Users

## Purpose
Use this skill for Wave authentication surfaces, profile management, custom profile fields, and user impersonation using only what the current Wave docs confirm.

## Source Rule
1. Before giving final auth, profile, or impersonation guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add auth routes, setup pages, middleware advice, profile paths, config paths, or impersonation behavior unless it appears in the current Wave docs.
3. When the Wave docs hand off advanced auth behavior to DevDojo Auth, say that clearly and query those docs only if the user asks for that deeper layer.
4. Keep examples close to documented routes, file paths, config files, and code snippets.

## Reference Map
- Auth setup surfaces, profiles, custom profile fields, and impersonation: [auth-profiles-and-impersonation.md](./references/auth-profiles-and-impersonation.md)

## Related Wave Skills
- Use `wave-access-control-admin` for roles, permissions, admin panel behavior, analytics, and Wave Blade directives.
- Use `wave-billing-subscriptions` for subscriber plans, provider setup, plan-role association, and billing gates documented by Wave.
- Use `wave-customization-theming` for auth appearance customization, logos, favicons, and theme-level UI changes.

## Workflow
1. Identify whether the task is auth customization, login/registration flow, subscriber gating, profile page behavior, custom profile fields, or impersonation.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use the documented Wave auth routes and setup pages first.
5. For profile customization, stay within `config/profiles.php` and the documented retrieval methods unless the docs confirm more.
6. Omit deeper auth-package behavior not confirmed by the Wave docs.

## Confirmed Core Patterns
- Wave authentication is built on DevDojo Auth.
- Auth customization is documented at `/auth/setup`.
- The docs list login, registration, verify email, password confirmation, password reset/request, and two-factor challenge as built-in auth pages.
- Login is documented at `/auth/login`.
- The docs say `subscribed` middleware may be used instead of adding both `auth` and `subscribed`.
- The auth docs show a `User` model `boot()` example that generates a username and assigns `config('wave.default_user_role', 'registered')` on creation.
- Email verification can be toggled from `/auth/setup/settings`.
- Social providers can be toggled from `/auth/setup/providers`.
- Public user profiles are documented at `/profile/{username}`.
- Profile pages use the app layout for authenticated users and the marketing layout for guests.
- The docs show disabling user profiles with `Route::redirect('profile/{username}', '/');` placed after `Wave::routes();`.
- Profile settings let users update avatar, name, email, and configured custom fields.
- Custom profile fields are configured in `config/profiles.php`.
- The docs show retrieving profile field data with `auth()->user()->profile('occupation')`.
- The docs say custom profile field types use the Filament Form Builder and may also use a plugin field by full namespace.
- User impersonation is managed from `/admin/users` with an Impersonate action and a Leave Impersonation action.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact auth or user topic.
- Every route, setup screen, config path, middleware statement, and code example is traceable to the current Wave docs.
- Advanced DevDojo Auth behavior is not inferred unless those docs are queried separately.
