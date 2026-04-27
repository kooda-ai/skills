---
name: laravel-13-installation-starter-kits
description: 'Use when: working with Laravel 13 installation, creating applications, Laravel installer, composer global require laravel/installer, laravel new example-app, cd example-app, npm install, npm run build, composer run dev, http://localhost:8000, starter kits, authentication scaffolding, Inertia, React, Svelte, Vue starter kits, Tailwind CSS, Vite, fresh application structure, bootstrap/app.php, storage directory, Providers directory, AppServiceProvider, Laravel Sail install boundary, and Laravel 13 setup code reviews. Use laravel-13-lifecycle-structure for full documented directory structure and request lifecycle topics. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 installation, starter kit, fresh app structure, local dev, or setup review task'
---

# Laravel 13 Installation And Starter Kits

## Purpose
Use this skill to create, review, or explain Laravel 13 installation, fresh application setup, starter kits, local startup commands, and confirmed fresh-app structure details using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact installation, starter kit, local development, Sail, or directory structure topic.
2. Do not add installation requirements, installer prompts, commands, starter kit names, generated files, frontend stacks, authentication behavior, directories, paths, server URLs, package commands, or setup steps unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, paths, URLs, directory names, package names, starter kit names, and wording.
5. Do not infer behavior from older Laravel versions, Laravel package docs outside the resolved source, blog posts, Docker guides, starter-kit source code, community examples, or general Laravel memory.

## Reference Map
- Laravel installer setup, `laravel new`, local app startup, and the documented Sail install boundary: [installation.md](./references/installation.md)
- Starter kit authentication scaffolding, fresh-application boundary, and documented frontend stacks: [starter-kits.md](./references/starter-kits.md)
- Confirmed fresh application structure details for `bootstrap`, route bootstrap, `storage`, and `Providers`: [fresh-application-structure.md](./references/fresh-application-structure.md)

## Workflow
1. Identify the exact surface: installer installation, new application creation, local development startup, starter kit selection, authentication scaffolding, frontend starter stack, fresh app directory structure, Sail installation, or setup review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, paths, directories, starter kit names, package names, server URLs, and setup examples.
5. For installation topics not in the references, such as PHP version requirements, Composer requirements, Node requirements, Laravel Herd, operating-system setup, database selection prompts, test framework selection prompts, Docker/Sail usage beyond installation, or deployment setup, rely on the fresh Context7 lookup.
6. For starter kit topics not in the references, such as exact starter kit command flags, generated routes/controllers/views, Livewire-specific kits, authentication customization, or package internals, rely on the fresh Context7 lookup.
7. Route full documented directory structure topics to `laravel-13-lifecycle-structure`; keep this slice focused on fresh-app structure boundaries relevant to installation and starter kits.
8. For reviews, flag only documented mismatches: unconfirmed setup command, wrong installer command, unsupported starter kit claim, unconfirmed generated file, unconfirmed frontend stack, wrong documented path, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `composer global require laravel/installer` is documented as an installer setup method when PHP and Composer are already present.
- `laravel new example-app` and `laravel new my-app` are documented new application commands.
- The Laravel installer prompts for framework and starter kit preferences according to the docs.
- The docs show local startup after application creation with `cd example-app`, `npm install && npm run build`, and `composer run dev`.
- The docs state the app is accessible at `http://localhost:8000` after the documented local development command sequence.
- Laravel starter kits offer backend and frontend authentication scaffolding for new applications.
- The authentication docs state installing a starter kit in a fresh application and running database migrations gives access to registration and login functionality.
- The docs describe starter kits as an educational resource for custom authentication flows.
- The frontend docs state Laravel starter kits include pre-configured setups for Inertia, React, Svelte, or Vue.
- The frontend docs state these kits scaffold backend and frontend authentication flows and integrate Tailwind CSS and Vite.
- The frontend docs describe starter kits as the recommended way to jump-start development.
- `composer require laravel/sail --dev` is documented as installing Laravel Sail as a development dependency.
- The default route bootstrap snippet uses `bootstrap/app.php`, `Application::configure(basePath: dirname(__DIR__))`, `withRouting(...)`, `routes/web.php`, `routes/console.php`, and health route `/up`.
- The `bootstrap` directory contains `app.php` and a cache folder for framework-generated files such as route and service caches according to the docs.
- The `storage` directory contains logs, compiled Blade templates, file-based sessions, file caches, and framework-generated files according to the docs.
- The docs state `storage/app/public` is used for user-generated files that must be publicly accessible and requires `php artisan storage:link`.
- The `Providers` directory contains service providers, and a fresh Laravel application already contains `AppServiceProvider` according to the docs.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 installation, starter kit, local development, Sail, or structure topic.
- Every setup command, package command, path, directory, URL, starter kit name, frontend stack, auth-scaffolding statement, and structure claim is traceable to the lookup or references.
- Operating system, Docker, Herd, Sail usage, Node, Composer, PHP, database, test framework, and generated-code details are not inferred when the current lookup did not confirm them.
- Unconfirmed setup or fresh-app structure details are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
