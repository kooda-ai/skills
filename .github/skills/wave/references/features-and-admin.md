# Features And Admin

## Authentication
- Wave docs say authentication is built on DevDojo Auth.
- The auth customization screen is documented at `/auth/setup`.
- Documented auth pages include `/auth/login` plus login, registration, verify email, password confirmation, password reset/request, and two-factor challenge flows.
- The docs say subscriber-only access can use the `subscribed` middleware instead of adding both `auth` and `subscribed`.
- The docs show a documented `App\Models\User` boot example that generates a username and assigns `config('wave.default_user_role', 'registered')` after user creation.
- The auth docs say email verification can be enabled from `/auth/setup/settings` and social providers are toggled at `/auth/setup/providers`.

## User Profiles And Impersonation
- Public user profiles are documented at `/profile/{username}`.
- The docs say profile pages use the app layout for authenticated users and the marketing layout for guests.
- The docs show disabling profiles with `Route::redirect('profile/{username}', '/');` placed after `Wave::routes();`.
- Profile settings let users edit avatar, name, email, and configured custom profile fields.
- Custom profile fields are documented in `config/profiles.php`.
- The docs say custom profile data is stored in the `profile_key_value` table and can be read with `auth()->user()->profile('occupation')` style access.
- The profile docs say field types come from the Filament Form Builder and may also use a plugin field by full namespace.
- User impersonation is documented from `/admin/users` with an Impersonate action and a Leave Impersonation action in the user menu.

## Billing And Subscription Plans
- The billing docs say `BILLING_PROVIDER` in `.env` selects `stripe` or `paddle`, with config stored in `config/wave.php`.
- Stripe setup in the docs uses `STRIPE_PUBLISHABLE_KEY`, `STRIPE_SECRET_KEY`, and `STRIPE_WEBHOOK_SECRET`.
- The Stripe webhook endpoint is documented as `/webhook/stripe`.
- The billing docs warn that successful checkout without a working webhook can leave the account unupgraded.
- The docs show local Stripe webhook testing with `stripe listen --forward-to https://wave.test/webhook/stripe`.
- Paddle setup in the docs includes `PADDLE_ENV`, `PADDLE_VENDOR_ID`, `PADDLE_API_KEY`, and `PADDLE_CLIENT_SIDE_TOKEN`.
- The Paddle webhook endpoint is documented as `webhook/paddle`, and the handled events include `subscription.cancelled`, `subscription.created`, `subscription.updated`, and `transaction.payment_failed`.
- The Paddle payment link is documented as `http://yourdomain.com/settings/subscription`.
- Subscription plans are managed in admin and linked to roles.
- The docs say default plans are Basic, Premium, and Pro.
- The subscription plan docs say it is best to keep plan names and role names lowercase.
- The docs show Stripe Price IDs coming from the Stripe product catalog and Paddle price IDs from the Paddle catalog.

## Roles And Permissions
- The roles docs say Wave ships with five roles: Admin, Registered, Basic, Premium, and Pro.
- The docs warn not to modify the Admin role because the codebase references it.
- The docs say renaming the Registered role also requires updating `default_user_role` in `config/wave.php`.
- The docs show role creation with `Spatie\Permission\Models\Role::create(['name' => 'writer'])`.
- Documented role APIs include `syncRoles([])`, `assignRole('writer')`, `User::role('writer')->get()`, `hasRole('writer')`, and the `@role` Blade directive.
- The permission docs show `Spatie\Permission\Models\Permission::create(['name' => 'edit articles'])`, `givePermissionTo('edit articles')`, `revokePermissionTo(...)`, `hasPermissionTo(...)`, `hasAnyPermission([...])`, `@can`, and `can()`.
- The docs recommend keeping permission assignments organized and suggest assigning permissions to roles rather than directly to users when possible.

## Notifications, Changelog, Blog, And Pages
- Wave notifications are documented as being built on Laravel notifications with a Wave UI on top.
- The docs show `php artisan make:notification TestNotification`, changing `via()` to `['database']`, and returning `icon`, `body`, `link`, and `user` data from `toArray()`.
- Notifications are viewed at `/notifications`, and unread count is documented as `auth()->user()->unreadNotifications->count()`.
- Changelog entries are managed at `/admin/changelog`, and the docs say changelog popups are shown across the application until clicked or dismissed.
- The blog is documented at `/blog`.
- The docs point to `resources/themes/{theme_folder}/blog/index.blade.php` for the blog list and `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php` for a post view.
- Posts are managed at `/admin/posts`, and only posts with status `PUBLISHED` appear on the front end.
- Categories are managed at `/admin/categories`.
- Content pages are managed from `/admin/pages` and become routes such as `/hello-world` based on slug.
- The docs say admin-created pages fit simple content pages, while theme `pages` files fit custom layouts, logic, or styling.

## API And Admin
- The docs say API keys are created at `/settings/api`.
- The API docs show token endpoints at `/api/token?key=API_KEY_HERE`, `/api/login?email=admin@admin.com&password=password`, `/api/refresh`, and `/api/register?name=John Doe&username=jdoe&email=jdoe@gmail.com&password=pass`.
- The docs describe the built-in API as a stateless JWT API and say Sanctum may be used alongside it.
- The docs suggest using the `wave-3-api-endpoints.json` export from the documented GitHub repository for Insomnia testing.
- The admin interface is documented at `/admin`.
- The docs list these admin-managed areas: users, roles, permissions, plans, posts, media, pages, categories, changelogs, themes, and settings.
- Admin analytics uses the Filament Google Analytics plugin and Spatie Laravel Analytics.
- The analytics setup in the docs uses `ANALYTICS_PROPERTY_ID` and a credential file at `storage/app/analytics/servive-account-credentials.json`.
- The admin docs show using Filament table and form builders inside theme pages, including `resources/themes/{theme}/pages/settings/api.blade.php` as a documented example.

## Use This Reference For
- Feature-level Wave questions.
- Routing user requests to the correct documented Wave surface.
- Verifying exact Wave routes, setup screens, and feature-specific config or endpoint names.
