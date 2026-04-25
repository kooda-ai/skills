# Context7 Query Prompts

Use these query shapes to refresh the source context before answering Filament 5 Users questions.

## Core Users
```text
Filament 5 Users documentation: user model setup, creating users, panel access, FilamentUser contract, canAccessPanel, panel-specific access, authentication features, custom auth pages/routes, profile, avatars, auth guard/password broker, user menu, guest access. Return documented APIs, commands, namespaces, and examples only.
```

## Authentication
```text
Filament 5 Users authentication documentation: login(), registration(), passwordReset(), emailVerification(), emailChangeVerification(), profile(), auth route slug customization, custom auth page classes, disabling revealable passwords, authGuard(), authPasswordBroker(), guest access. Return documented methods and snippets only.
```

## Identity and Menus
```text
Filament 5 users documentation: user names in UI, HasName contract, getFilamentName(), HasAvatar, getFilamentAvatarUrl(), custom avatar provider, defaultAvatarProvider(), userMenuItems(), profile menu item, UserMenuPosition. Return exact code snippets and documented methods only.
```

## Multi-Factor Authentication
```text
Filament 5 users multi-factor authentication documentation: AppAuthentication, EmailAuthentication, recovery codes, required database columns, User model interfaces/traits, MustVerifyEmail, profile setup UI, multiFactorAuthentication(), recoverable(), isRequired. Return exact documented APIs, classes, snippets, and commands only.
```

## Tenancy Users
```text
Filament 5 users tenancy documentation: tenant model setup, HasTenants, getTenants, canAccessTenant, HasDefaultTenant, current tenant, tenant registration page, tenant profile page, tenant menu items, tenant identity, tenant routes/domains, billing, resource scoping, validation, tenant middleware, security notes. Return documented methods, interfaces, snippets, namespaces only.
```
