---
name: wave-access-control-admin
description: 'Use when: working with Wave roles and permissions, default Wave roles, plan-to-role access control, admin panel routes and sections, admin analytics setup, admin-side Filament usage mentioned by Wave docs, and Wave Blade directives for admin/subscriber checks. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave roles, permissions, admin panel, analytics, or access-control task'
---

# Wave Access Control And Admin

## Purpose
Use this skill for Wave role and permission behavior, plan-linked access control, admin panel capabilities, analytics setup, and Wave-specific Blade directives.

## Source Rule
1. Before giving final access-control or admin guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add role names, permission APIs, admin routes, analytics setup, admin-managed areas, or Blade directives unless they appear in the current Wave docs.
3. If the task needs deeper Filament, Google Analytics, or package-level behavior, say that the Wave docs defer to those products.
4. Keep examples close to documented routes, file paths, directives, and code snippets.

## Reference Map
- Roles, permissions, admin surfaces, analytics setup, and Wave directives: [roles-permissions-admin-and-directives.md](./references/roles-permissions-admin-and-directives.md)

## Related Wave Skills
- Use `wave-auth-users` for login, registration, profile fields, impersonation, and auth setup pages.
- Use `wave-billing-subscriptions` for provider setup, webhooks, subscription plans, and plan-role linkage.
- Use `wave-blade-directives` when the task is specifically about the documented directive syntax or which Wave directive to use in a view.
- Use `wave-plugins-concepts` when the task moves from admin access control into Volt pages, plugin structure, or Filament-with-Volt implementation patterns.

## Workflow
1. Identify whether the task is roles, permissions, plan-linked access, admin panel behavior, analytics, or Wave directives.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Hand off to `wave-blade-directives` when the task is directive-specific rather than access-control-specific.
5. Use the documented Wave roles, admin areas, and directive names only.
6. Preserve the documented connection between plans and roles when discussing access control.
7. Omit package internals not confirmed by the Wave docs.

## Confirmed Core Patterns
- Wave ships with five documented roles: Admin, Registered, Basic, Premium, and Pro.
- The docs warn not to modify the Admin role because the codebase references it.
- Renaming the Registered role also requires changing `default_user_role` in `config/wave.php`.
- The docs show role creation with `Role::create(['name' => 'writer'])`.
- Documented role APIs include `syncRoles([])`, `assignRole('writer')`, `User::role('writer')->get()`, `hasRole('writer')`, and the `@role` Blade directive.
- The docs show permission creation with `Permission::create(['name' => 'edit articles'])`, user direct permissions with `givePermissionTo(...)`, role revocation with `revokePermissionTo(...)`, and permission checks with `hasPermissionTo(...)`, `hasAnyPermission([...])`, `@can`, and `can()`.
- The docs recommend keeping permissions organized and suggest assigning permissions to roles rather than directly to users when possible.
- The admin panel is documented at `/admin`.
- The docs list these admin-managed areas: users, roles, permissions, plans, posts, media, pages, categories, changelogs, themes, and settings.
- The admin is built with FilamentPHP.
- Admin analytics uses the Filament Google Analytics plugin and Spatie Laravel Analytics.
- The analytics setup uses `ANALYTICS_PROPERTY_ID` and a credential file at `storage/app/analytics/servive-account-credentials.json`.
- The Wave Blade directives page documents `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`, with `@else` support.
- The docs note that `@subscribed()` expects the full plan name.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact admin or access-control topic.
- Every role name, route, directive, package mention, analytics detail, and code example is traceable to the current Wave docs.
- Deeper Filament, package, or analytics behavior is not inferred beyond what the Wave docs confirm.
