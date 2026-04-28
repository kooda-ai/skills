---
name: wave-installation-development
description: 'Use when: working with Wave installation, first-run setup, Herd install, manual install, SQLite defaults, admin login defaults, Wave stack, packages used by Wave, and documented starting points for adding functionality during development. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave install, first-run setup, stack, defaults, or development starting-point task'
---

# Wave Installation And Development

## Purpose
Use this skill to handle Wave setup, first-run defaults, under-the-hood stack questions, and the documented starting points for development using only details confirmed in the current Wave docs.

## Source Rule
1. Before giving final setup steps, commands, defaults, or development guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add install commands, prerequisites, database defaults, login defaults, stack details, package names, or development workflow claims unless they appear in the current Wave docs.
3. If Wave hands off advanced behavior to Laravel, Filament, DevDojo Auth, Folio, or Volt, say that clearly instead of filling gaps from memory.
4. Keep examples close to documented commands, file paths, routes, and config snippets.

## Reference Map
- Setup flows, defaults, stack, packages, and documented development entry points: [setup-and-starting-points.md](./references/setup-and-starting-points.md)

## Related Wave Skills
- Use `wave-customization-theming` for theme activation, theme structure, asset wiring, and visual customization.
- Use `wave-plugins-concepts` for plugins, Volt pages, Folio mapping, and the documented pattern for adding functionality.
- Use `wave-upgrading-guides` for manual upgrades, theme upgrade implications, and published guide lookups.

## Workflow
1. Identify whether the task is install, first login, database setup, stack explanation, or where-to-start development guidance.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only documented Wave setup flows: Herd automation or the manual installation path.
5. For development structure questions, prefer the documented Wave recommendation for adding functionality.
6. Omit anything not confirmed by the current Wave docs.

## Confirmed Core Patterns
- Wave is described as a SaaS starter kit/framework built on Laravel.
- The docs list Laravel, Livewire, Tailwind CSS, Alpine, and Vite as technologies used.
- The docs list FilamentPHP, DevDojo Auth, DevDojo Themes, the 404labfr impersonation package, Spatie Roles/Permissions, Laravel Folio, and Laravel Volt as packages used.
- The install docs describe an automated Herd flow: unzip, rename the folder, move it into a Herd sites directory, and visit `foldername.test`.
- The manual install docs show `cp .env.example .env`, `composer install`, `php artisan migrate`, and `php artisan db:seed`.
- Wave uses SQLite by default at `database/database.sqlite` and can be changed in `.env`.
- The default admin login in the docs is `admin@admin.com` with password `password`.
- The docs say Wave functionality can be added in familiar Laravel locations such as controllers, models, and services.
- The docs recommend single-file Volt pages in `resources/themes/{theme}/pages` when adding new functionality.
- The docs say complex logic may still be moved into services or controllers to keep Volt pages maintainable.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact setup or development topic.
- Every command, default credential, file path, package name, and development-structure claim is traceable to the current Wave docs.
- Laravel, Filament, Folio, or Volt details are not expanded beyond what the Wave docs confirm unless those docs are queried separately.
