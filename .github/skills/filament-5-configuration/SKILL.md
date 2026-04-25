---
name: filament-5-configuration
description: 'Use when: working with Filament 5 Configuration, PanelProvider, AdminPanelProvider, panel(Panel $panel), make:filament-panel, filament:install --panels, vendor:publish --tag=filament-config, path(), domain(), middleware(), authMiddleware(), colors(), font(), viteTheme(), navigation, authentication, notifications, tenancy, assets, render hooks, SPA mode, transactions, broadcasting, and panel plugins. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Panel configuration task, AdminPanelProvider code, auth/styling/navigation/tenancy setup, or configuration to review'
---

# Filament 5 Configuration

## Purpose
Use this skill to create, review, or explain Filament 5 panel configuration using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Configuration topic.
2. Do not add behavior, APIs, options, namespaces, commands, middleware behavior, plugin behavior, auth behavior, tenancy behavior, styling options, navigation options, asset behavior, render hooks, or conventions unless they appear in the retrieved documentation.
3. If a requested Configuration topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Configuration tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, command names, enum names, and class names.

## Reference Map
- Panel setup, routes, lifecycle, middleware, SPA mode, transactions, broadcasting, strict authorization, error notifications, panel assets, panel render hooks, and plugins: [panel-runtime.md](./references/panel-runtime.md)
- Styling, themes, navigation, sidebars, topbar, breadcrumbs, navigation groups, and custom navigation items: [styling-navigation.md](./references/styling-navigation.md)
- Users, panel access, authentication features, auth routes, guards, profile pages, avatars, guest access, and notifications: [users-notifications.md](./references/users-notifications.md)
- Multi-tenancy, tenant registration/profile pages, tenant menu, tenant relationships, route/domain options, tenant middleware, billing, and tenancy security: [tenancy.md](./references/tenancy.md)
- Asset registration and render-hook details outside the panel-provider shortcuts: [assets-render-hooks.md](./references/assets-render-hooks.md)

## Workflow
1. Identify the configuration surface: installation/config publishing, panel provider setup, URL/domain, styling, navigation, authentication, notifications, tenancy, assets, render hooks, middleware, runtime behavior, plugins, or review of an existing provider.
2. Run a narrow Context7 query for the exact configuration topic before producing code.
3. Load the relevant reference file from the map above.
4. For panel-provider code, use only documented `Panel` methods confirmed for the task, such as `path()`, `domain()`, `maxContentWidth()`, `simplePageMaxContentWidth()`, `subNavigationPosition()`, `bootUsing()`, `spa()`, `spaUrlExceptions()`, `unsavedChangesAlerts()`, `databaseTransactions()`, `assets()`, `middleware()`, `authMiddleware()`, `broadcasting(false)`, `strictAuthorization()`, `errorNotifications(false)`, `registerErrorNotification()`, `hiddenErrorNotification()`, `disabledErrorNotification()`, `renderHook()`, and `plugin()`.
5. For styling and theme tasks, use only documented configuration methods confirmed for the task, such as `colors()`, `font()`, `viteTheme()`, `darkMode(false)`, `defaultThemeMode()`, `brandName()`, `brandLogo()`, `darkModeBrandLogo()`, `brandLogoHeight()`, and `favicon()`.
6. For navigation tasks, distinguish panel-level configuration from Resource/Page static navigation properties. Use the Filament 5 Resources skill for Resource-specific implementation details after confirming the configuration touchpoint.
7. For authentication tasks, keep panel-level methods separate from User model contracts. Use only documented `login()`, `registration()`, `passwordReset()`, `emailVerification()`, `emailChangeVerification()`, `profile()`, route slug methods, `authGuard()`, `authPasswordBroker()`, `revealablePasswords(false)`, and documented contracts when confirmed.
8. For notifications, load the Filament 5 Notifications skill for notification composition, and use this skill for panel-level enablement such as `databaseNotifications()`, `databaseNotificationsPolling()`, broadcasting setup, and `broadcasting(false)`.
9. For tenancy, include the security warnings and relationship requirements from the tenancy docs before providing implementation guidance. Load the Filament 5 Resources, Forms, or Actions skill when the task moves into resource scoping, validation, forms, or action menu customization details.
10. For plugin work, use only documented `Filament\Contracts\Plugin`, `getId()`, `register(Panel $panel)`, `boot(Panel $panel)`, `plugin()`, `make()`, and per-panel getter/setter patterns confirmed by the lookup.
11. Finish by checking that every command, method, enum, class, import, parameter name, route behavior, and code example in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Panel Builder installation uses `composer require filament/filament:"^5.0"` and `php artisan filament:install --panels`; PowerShell may require `composer require filament/filament:"~5.0"`.
- Installation creates and registers `app/Providers/Filament/AdminPanelProvider.php`; the docs say to check `bootstrap/providers.php` if the panel cannot be accessed.
- `php artisan make:filament-user` creates a user account for signing in.
- `php artisan vendor:publish --tag=filament-config` creates `config/filament.php` for defaults shared across Filament packages.
- A new panel is created with `php artisan make:filament-panel app`, creating `app/Providers/Filament/AppPanelProvider.php`, normally accessible at `/app` unless the path is customized.
- Panel configuration is expressed in a class extending `Filament\PanelProvider` with `public function panel(Panel $panel): Panel` returning the configured panel.
- Panel plugins implement `Filament\Contracts\Plugin` with `getId()`, `register(Panel $panel)`, and `boot(Panel $panel)`; users add one with `->plugin(new BlogPlugin())` or a documented `BlogPlugin::make()` pattern.
- Middleware configured with `middleware()`, `authMiddleware()`, and `tenantMiddleware()` runs on the first page load by default; the docs confirm passing `isPersistent: true` to run on every Livewire AJAX request for those methods.
- SPA mode uses Livewire `wire:navigate`; `spa(hasPrefetching: true)` enables prefetching, and `spaUrlExceptions()` accepts exact URLs, a deferred callback, or wildcard patterns.
- Database transactions are disabled by default; `databaseTransactions()` enables them panel-wide, `databaseTransaction(false)` opts actions out, and `$hasDatabaseTransactions` controls Create/Edit resource pages.
- Filament tenancy is security-sensitive; the docs state Filament provides tools but no guarantees, and the application is responsible for ensuring tenant data is secure.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each command, method, enum, class, import, parameter, contract, middleware behavior, and route behavior is traceable to retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Laravel habits, Livewire habits, package source code, or memory.
- If the user asks for a Configuration topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, parameter names, enum names, command flags, and route strings intact.