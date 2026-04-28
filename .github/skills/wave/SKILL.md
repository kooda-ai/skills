---
name: wave
description: 'Use when: working with Wave, DevDojo Wave, the DevDojo SaaS starter kit, themes, plugins, Volt pages, Folio routes, billing, subscription plans, roles and permissions, user profiles, impersonation, notifications, changelog, blog, pages, API, admin, customizations, adding Wave functionality, installation, or upgrading. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave topic, exact docs area, feature, route, config, page, or implementation task'
---

# Wave

## Purpose
Use this skill to create, review, or explain DevDojo Wave using only details confirmed in the current Wave documentation.

## Source Rule
1. Before giving final code, commands, routes, configuration, upgrade advice, or review findings, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add commands, file paths, routes, environment variables, middleware names, package behavior, admin flows, theme structure, plugin loading behavior, payment setup, API endpoints, or upgrade steps unless they appear in the current Wave documentation context or in the reference files below.
3. If the Wave docs explicitly defer to another product's docs, such as DevDojo Auth, Filament, Laravel Folio, Laravel Volt, Laravel, Stripe, or Paddle, say that clearly and only add those details after querying that product's current documentation if the user asks for them.
4. Keep examples close to documented snippets and preserve documented file paths, route paths, config keys, environment variables, method names, and command strings.
5. Do not infer behavior from Laravel, Livewire, Filament, older Wave versions, GitHub source, blog posts, or memory alone unless the current Wave docs confirm it.

## Reference Map
- Getting started, installation, stack, packages, and first-run defaults: [core-and-installation.md](./references/core-and-installation.md)
- Feature surfaces across authentication, profiles, billing, plans, roles, notifications, content, API, and admin: [features-and-admin.md](./references/features-and-admin.md)
- Themes, plugins, Volt pages, Blade directives, customizations, adding functionality, Filament with Volt, and upgrading: [extension-and-customization.md](./references/extension-and-customization.md)

## Related Split Skills
- Use `wave-installation-development` for installation, first-run setup, stack details, SQLite defaults, admin login defaults, and documented development starting points.
- Use `wave-customization-theming` for themes, theme activation, theme creation, theme structure, asset wiring, logos, favicons, colors, and auth appearance customization.
- Use `wave-auth-users` for authentication, auth setup pages, registration and login surfaces, profiles, custom profile fields, and impersonation.
- Use `wave-billing-subscriptions` for billing provider setup, Stripe, Paddle, webhooks, plans, plan-role association, and Price IDs.
- Use `wave-access-control-admin` for roles, permissions, plan-linked access control, admin panel behavior, analytics setup, and Wave Blade directives.
- Use `wave-content-api` for API keys, JWT token flows, register/login token endpoints, and API testing.
- Use `wave-notifications-content` for notifications, changelog, blog, content pages, and admin content-management surfaces.
- Use `wave-plugins-concepts` for plugins, adding functionality, and Filament-with-Volt patterns.
- Use `wave-volt-pages` for Volt pages, Folio route mapping, and the documented theme-page implementation pattern.
- Use `wave-blade-directives` for Wave-specific Blade directives such as `@admin`, `@subscriber`, and `@subscribed(...)`.
- Use `wave-upgrading-guides` for manual upgrades, theme-upgrade implications, guide lookup, support resources, and the documented Filament-with-Volt guide.

## Workflow
1. Identify the Wave surface: getting started, installation, customizations, your functionality, upgrading, authentication, user profiles, impersonation, billing, subscription plans, roles and permissions, notifications, changelog, blog, pages, API, admin, themes, plugins, Blade directives, Volt pages, or Filament with Volt.
2. Run a narrow Context7 query for `/websites/devdojo_wave` before producing code or review findings.
3. Prefer the closest split skill above when the request fits one of those narrower surfaces; otherwise continue with this umbrella skill.
4. Load the closest reference file from the map above.
5. For package-backed features, keep the answer inside the Wave boundary first. If the docs hand off advanced behavior to DevDojo Auth, Filament, Laravel, Stripe, or Paddle, mark that handoff explicitly instead of filling gaps from memory.
6. For theme and plugin work, verify every documented folder, file name, route mapping, namespace, and activation step before suggesting changes.
7. For billing, API, or auth work, verify the exact env vars, routes, endpoints, credentials, middleware, and setup pages against the current lookup.
8. For implementation guidance, prefer the documented Wave patterns: theme pages, single-file Volt pages, and documented Filament form/table usage inside theme pages.
9. Finish by checking that every version-specific claim is traceable to the current Wave docs context or the reference files, and omit anything not confirmed.

## Confirmed Core Patterns
- Wave presents itself as a SaaS starter kit/framework built on Laravel.
- The docs list Wave feature areas including authentication, user profiles, user impersonations, billing, subscription plans, roles and permissions, notifications, changelog, blog, pages, API, admin, themes, and plug-ins.
- The docs list the stack and packages under the hood as Laravel, Livewire, Tailwind CSS, Alpine, Vite, FilamentPHP, DevDojo Auth, DevDojo Themes, the 404labfr impersonation package, Spatie Roles/Permissions, Laravel Folio, and Laravel Volt.
- The install docs describe both an automated Herd flow and a manual installation flow with `cp .env.example .env`, `composer install`, `php artisan migrate`, and `php artisan db:seed`.
- The install docs say Wave defaults to SQLite at `database/database.sqlite` and can be changed in `.env`.
- The install docs document a default admin login of `admin@admin.com` and `password`.
- The auth docs say Wave uses DevDojo Auth and exposes customization at `/auth/setup`.
- The theme docs say active views live in `resources/themes/{theme}`, the active theme is available through the `theme::` namespace, theme pages are route-mapped through the theme `pages` directory, and theme assets are selected through `theme.json` and `vite.config.js`.
- The plug-in docs say plugins live in `resources/plugins`, installed plugin names are tracked in `resources/plugins/installed.json`, and plugin classes follow a `register()` then `boot()` lifecycle similar to Laravel service providers.
- The Wave docs recommend adding custom functionality with single-file Volt pages inside `resources/themes/{theme}/pages`, while moving complex logic into services or controllers when needed.
- The upgrading docs currently describe a manual upgrade path and note that theme upgrades may require manual file movement when new features add views.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact Wave topic.
- Every route, path, command, env var, setup screen, endpoint, plugin/theme detail, and upgrade statement is traceable to the current lookup or the reference files.
- Advanced Auth, Filament, Laravel, Stripe, or Paddle behavior is not invented from memory when Wave docs delegate to those products.
- Unconfirmed details are omitted or followed by a narrower lookup.
