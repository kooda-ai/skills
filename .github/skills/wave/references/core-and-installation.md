# Core And Installation

## Product Scope
- Wave is described as a SaaS starter kit/framework built on Laravel.
- The getting-started docs point to these Wave feature areas: authentication, user profiles, user impersonations, billing, subscription plans, roles and permissions, user notifications, changelog, blog, pages, API, admin, themes, and plug-ins.

## Under The Hood
- The docs list these technologies: Laravel, Livewire, Tailwind CSS, Alpine, and Vite.
- The docs also list these packages used by Wave: FilamentPHP, DevDojo Auth, DevDojo Themes, the 404labfr impersonation package, Spatie Roles/Permissions, Laravel Folio, and Laravel Volt.

## Installation
### Automated Installation With Herd
- The install docs say to unzip the download, rename the folder, move it into a Herd site directory, and visit `foldername.test` to start the automated installer.

### Manual Installation
- The manual install flow in the docs is:

```bash
cp .env.example .env
composer install
php artisan migrate
php artisan db:seed
```

## Database Defaults
- The docs say Wave uses SQLite by default at `database/database.sqlite`.
- The docs show that the database connection can be changed in `.env`.
- The install page includes a MySQL `.env` example using:

```env
CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database-name
DB_USERNAME=root
DB_PASSWORD=''
```

## First Login
- The install docs say the default admin credentials are `admin@admin.com` and `password`.
- The docs say those values can later be changed from the settings section in the user menu.

## Demo And Navigation
- The getting-started docs link to a public Wave demo.
- The published documentation entry points confirmed in the docs fetch are `getting-started`, `install`, `customizations`, `your-functionality`, `upgrading`, feature pages, concept pages such as `blade-directives` and `volt`, and the guides index.

## Use This Reference For
- Explaining what Wave includes out of the box.
- Verifying install steps, defaults, and first-run expectations.
- Routing a question into the right Wave docs area before deeper work.
