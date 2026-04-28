# Plugins, Volt, And Functionality Patterns

## Plugins
- Plugins are stored in `resources/plugins`.
- Installed plugin names are tracked in `resources/plugins/installed.json`.
- Plugins are activated from `/admin/plugins`.
- The docs describe a main plugin class such as `resources/plugins/example/ExamplePlugin.php`.
- The plugin `boot()` method is documented for loading views, migrations, routes, and Livewire components.
- The plugin `register()` method is documented for binding services and registering utilities before boot logic runs.
- The documented loading order is: read `installed.json`, instantiate plugin classes, call `register()` on all, then call `boot()` on each.

## Volt And Folio
- Theme `pages` directories are mapped to routes using Laravel Folio.
- The docs show route mapping examples such as `pages/index.blade.php` to `/`, `pages/about.blade.php` to `/about`, and `pages/blog/[post].blade.php` to `/blog/{post}`.
- The docs say those page files can contain single-file Volt components.

## Blade Directives And Functionality Pattern
- Wave documents `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`.
- The `your-functionality` docs recommend single-file Volt pages in `resources/themes/{theme}/pages` for new functionality.
- The docs say complex logic can still move into services or controllers.

## Filament With Volt
- The Filament-with-Volt guide demonstrates using Filament table and form builders directly inside Wave theme Volt pages.
- The guide shows rendering a table with `{{ $this->table }}` and a form with `{{ $this->form }}` in a Volt page.
