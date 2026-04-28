# Roles, Permissions, Admin, And Directives

## Roles And Permissions
- Wave ships with five documented roles: Admin, Registered, Basic, Premium, and Pro.
- The docs warn not to modify the Admin role because the codebase references it.
- Renaming the Registered role also requires changing `default_user_role` in `config/wave.php`.
- Documented role APIs include `Role::create(...)`, `syncRoles([])`, `assignRole(...)`, `User::role(...)`, `hasRole(...)`, and the `@role` Blade directive.
- Documented permission APIs include `Permission::create(...)`, `givePermissionTo(...)`, `revokePermissionTo(...)`, `hasPermissionTo(...)`, `hasAnyPermission([...])`, `@can`, and `can()`.

## Admin Panel
- The admin panel is documented at `/admin`.
- The docs list these managed areas: users, roles, permissions, plans, posts, media, pages, categories, changelogs, themes, and settings.
- The admin is built with FilamentPHP.

## Analytics
- Admin analytics uses the Filament Google Analytics plugin and Spatie Laravel Analytics.
- The analytics setup uses `ANALYTICS_PROPERTY_ID`.
- The docs also point to a credential file at `storage/app/analytics/servive-account-credentials.json`.

## Wave Blade Directives
- The documented directives are `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`.
- The docs say `@subscribed()` expects the full plan name.
- `@else` may be used with these directive conditions.
