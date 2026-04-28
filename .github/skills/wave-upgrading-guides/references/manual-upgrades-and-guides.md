# Manual Upgrades And Guides

## Upgrading
- The current docs describe a manual upgrade path.
- The documented upgrade flow is to replace the root `wave` folder and the `app/Filament` folder with the latest copies.
- The docs then show running:

```bash
composer dump-autoload
php artisan cache:clear
```

- The docs say admin customizations may need to be ported manually.
- Theme upgrades are usually not required unless a new feature introduces corresponding views that you want to bring over.

## Guides And Support
- The guides index currently lists `Using Filament With Volt` as the current guide confirmed in the fetched docs.
- The guides page also mentions planned guides for adding the table builder to a page, adding the form builder to a page, and adding the billing component to any page.
- The guides page links to Wave documentation, DevDojo Questions, and DevDojo help/support.

## Filament With Volt Guide
- The guide demonstrates using a Filament table, a Filament form, and a combined table-plus-form Volt page inside Wave theme pages.
- Keep guide-based answers inside what the guide explicitly shows unless the user asks for deeper product docs.
