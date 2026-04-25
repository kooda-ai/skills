---
name: filament-5-users
description: 'Use when: working with Filament 5 Users, User model access, make:filament-user, FilamentUser, canAccessPanel(), login(), registration(), passwordReset(), emailVerification(), emailChangeVerification(), profile(), auth route slugs, authGuard(), authPasswordBroker(), revealable passwords, guest access, HasName, HasAvatar, default avatar providers, userMenuItems(), multi-factor authentication, HasTenants, canAccessTenant(), tenant registration/profile/menu/billing, and tenancy security. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Users/authentication/access/identity/MFA/tenancy task, PanelProvider code, User model code, or code to review'
---

# Filament 5 Users

## Purpose
Use this skill to create, review, or explain Filament 5 user access, authentication, identity, profile, multi-factor authentication, and tenant-user behavior using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Users topic.
2. Do not add behavior, APIs, namespaces, commands, route names, middleware behavior, security guarantees, authentication behavior, tenancy behavior, or conventions unless they appear in the retrieved documentation.
3. If a requested Users topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Users tasks into reference-backed sections instead of guessing or mixing unrelated Filament areas.
5. Keep examples close to documented snippets and preserve documented method names, class names, namespaces, parameter names, and command names.

## Reference Map
- Panel access, creating users, authentication features, auth routes, guard/broker, revealable passwords, custom profile forms, email-change verification, guest access, and resource authorization boundaries: [access-authentication.md](./references/access-authentication.md)
- User names, avatars, avatar providers, profile/user menu items, and user menu position: [identity-user-menu.md](./references/identity-user-menu.md)
- Multi-factor authentication, app authentication, recovery codes, email authentication, profile UI, and required MFA: [multi-factor-authentication.md](./references/multi-factor-authentication.md)
- Tenant users, tenant access, tenant registration/profile pages, tenant menu, tenant routing/domains, billing, resource scoping, and tenancy security checks: [tenancy-users.md](./references/tenancy-users.md)

## Workflow
1. Identify the Users surface: panel access, account creation, auth feature enablement, auth page customization, profile fields, identity display, avatars, user menu, multi-factor authentication, guest access, tenant access, tenant pages/menu/billing, or tenancy security.
2. Run a narrow Context7 query for the exact Users subtopic before producing code.
3. Load the relevant reference file from the map above.
4. For panel access, use only documented `php artisan make:filament-user`, `Filament\Models\Contracts\FilamentUser`, `Filament\Panel`, `canAccessPanel(Panel $panel): bool`, and `$panel->getId()` patterns confirmed by the lookup.
5. For authentication features, use only documented panel methods confirmed for the task, such as `login()`, `registration()`, `passwordReset()`, `emailVerification()`, `emailChangeVerification()`, `profile()`, route slug/prefix methods, `authGuard()`, `authPasswordBroker()`, and `revealablePasswords(false)`.
6. For custom authentication/profile pages, only use base classes, helper methods, and form components confirmed by the current lookup. If Context7 confirms only the profile example, do not invent examples for login, registration, or reset pages.
7. For identity and menu tasks, use only documented contracts and panel methods: `HasName`, `getFilamentName()`, `HasAvatar`, `getFilamentAvatarUrl()`, `defaultAvatarProvider()`, `userMenuItems()`, `userMenu()`, and `UserMenuPosition` when confirmed.
8. For multi-factor authentication, include the required database columns, User model interfaces/traits, panel provider methods, and profile-page dependency only when confirmed by the lookup.
9. For tenancy, state the security framing first, then use only documented `tenant()`, `HasTenants`, `getTenants()`, `canAccessTenant()`, `HasDefaultTenant`, tenant registration/profile/menu/billing methods, route/domain methods, resource scoping properties, validation methods, and tenant middleware confirmed by Context7.
10. For Resource CRUD authorization, UserResource schemas/tables, or form component internals, use this skill only for the Users touchpoint and load the Filament 5 Resources, Forms, Tables, Actions, or Configuration skill for the detailed implementation.
11. Finish by checking that every command, method, class, interface, trait, import, property, parameter, route slug, and security statement is traceable to the current Context7 result and loaded reference file.

## Confirmed Core Patterns
- `php artisan make:filament-user` creates a user account for accessing a Filament panel.
- In non-local environments, a User model must implement `FilamentUser` and `canAccessPanel(Panel $panel): bool` to allow panel sign-in.
- `canAccessPanel()` can inspect `$panel->getId()` for panel-specific access logic.
- Panel authentication features are enabled with `login()`, `registration()`, `passwordReset()`, `emailVerification()`, `emailChangeVerification()`, and `profile()`.
- Auth route slugs and prefixes are customized with documented `*RouteSlug()` and `*RoutePrefix()` panel methods.
- `authGuard('web')` sets the panel authentication guard, and `authPasswordBroker('users')` sets the password broker.
- `revealablePasswords(false)` disables revealable password inputs globally in panel authentication forms.
- Custom profile pages can extend `Filament\Auth\Pages\EditProfile`, override `form(Schema $schema): Schema`, and be registered with `profile(EditProfile::class)`.
- User display names use the `name` attribute by default; `HasName` and `getFilamentName()` customize the displayed name.
- User avatars use `ui-avatars.com` by default; `HasAvatar`, `getFilamentAvatarUrl()`, and `defaultAvatarProvider()` customize avatars.
- User menu customization uses `userMenuItems()` with `Filament\Actions\Action`; the `profile` key customizes the profile link.
- Multi-factor authentication is configured with `multiFactorAuthentication([...])`; users manage MFA settings from the profile page when `profile()` is enabled.
- Tenancy is configured with `tenant(Team::class)` and user tenant membership is defined through `HasTenants`, `getTenants(Panel $panel): Collection`, and `canAccessTenant(Model $tenant): bool`.
- Tenant registration/profile pages extend `RegisterTenant` and `EditTenantProfile`; `tenantRegistration()` is confirmed for registration, and tenant profile registration must be re-queried before use.
- Tenant-aware resources are automatically scoped in a tenancy-enabled panel, but the docs warn that custom queries, actions, pages, validation, and code outside the tenancy-enabled panel need explicit care.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each command, class, interface, trait, method, property, parameter, route behavior, and security note is traceable to retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Laravel habits, package source code, or memory.
- If the user asks for a Users topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, parameters, imports, and route strings intact.
