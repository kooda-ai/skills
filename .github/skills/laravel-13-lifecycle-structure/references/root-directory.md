# Root Directory

Sources used: Current Laravel 13.x documentation page for directory structure.

## Structure Boundary
The docs state the default Laravel application structure is intended as a great starting point for large and small applications, and Laravel imposes almost no restrictions on where classes are located as long as Composer can autoload them.

## Root Directories
The docs describe the following root directories:

- `app`: contains the core code of the application, and almost all application classes live here.
- `bootstrap`: contains `app.php`, which bootstraps the framework, and a `cache` directory for generated performance files such as route and services caches.
- `config`: contains all application configuration files.
- `database`: contains migrations, model factories, and seeds, and may also hold an SQLite database.
- `public`: contains `index.php`, the entry point for all requests, and public assets such as images, JavaScript, and CSS.
- `resources`: contains views and raw uncompiled assets such as CSS or JavaScript.
- `routes`: contains route definitions. By default, Laravel includes `web.php` and `console.php`.
- `storage`: contains logs, compiled Blade templates, file sessions, file caches, and other framework-generated files; the docs also describe `storage/app/public` for user-generated public files.
- `tests`: contains automated tests; the docs mention Pest and PHPUnit examples and `php artisan test`.
- `vendor`: contains Composer dependencies.

## Routes Directory Details
The docs state `routes/web.php` holds routes placed in the `web` middleware group.

The docs state `routes/console.php` is where closure-based console commands may be defined and that tasks may also be scheduled in this file.

The docs also state optional additional route files may be installed:

- `api.php` via `install:api`
- `channels.php` via `install:broadcasting`

The docs describe `api.php` as stateless and intended for token-authenticated requests, and `channels.php` as the registration point for broadcasting channels.

## Storage Directory Details
The docs state `storage` is divided into `app`, `framework`, and `logs`.

The docs say `storage/app/public` may store user-generated files that should be publicly accessible, and that `php artisan storage:link` creates the `public/storage` symbolic link to that directory.

## Test Commands
The docs state tests may be run with `/vendor/bin/pest`, `/vendor/bin/phpunit`, or `php artisan test`.

## Topics Requiring Fresh Lookup
Run a new documentation lookup before describing every file in the root tree, API route bootstrap behavior beyond the structure page, deployment filesystem layouts, package-installed directories, or directories not explicitly covered in the Laravel 13 structure docs.