# Setup And Starting Points

## Install Paths
- The docs describe two install flows: an automated Herd install and a manual installation flow.
- Herd flow: unzip the download, rename the folder, move it into a Herd sites directory, and visit `foldername.test`.
- Manual flow:

```bash
cp .env.example .env
composer install
php artisan migrate
php artisan db:seed
```

## Defaults
- Wave uses SQLite by default at `database/database.sqlite`.
- The docs say the database connection can be changed in `.env`.
- The default admin credentials are `admin@admin.com` and `password`.

## Stack And Packages
- Technologies listed in the docs: Laravel, Livewire, Tailwind CSS, Alpine, and Vite.
- Packages listed in the docs: FilamentPHP, DevDojo Auth, DevDojo Themes, the 404labfr impersonation package, Spatie Roles/Permissions, Laravel Folio, and Laravel Volt.

## Development Starting Point
- The docs say Wave logic can be added in familiar Laravel locations such as controllers, models, and services.
- The docs recommend single-file Volt pages in `resources/themes/{theme}/pages` as the preferred Wave pattern for new functionality.
- The docs say complex logic can still be moved into services or controllers when needed.
