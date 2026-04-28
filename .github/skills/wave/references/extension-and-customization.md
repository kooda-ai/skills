# Extension And Customization

## Themes
- Themes are installed under `resources/themes/{theme}` and activated from `/admin/themes`.
- The docs say downloaded theme folders should be renamed to the actual theme name before being placed in `resources/themes`.
- After activation, the docs say `npm run dev` may need to be restarted.
- The active theme is available through the `theme::` namespace, for example `return view('theme::home');`.
- Theme pages are documented under `resources/themes/{theme}/pages` and are route-mapped.
- The theme docs list common provided pages including homepage, dashboard, pricing, profile, settings pages, subscription welcome, notifications, blog pages, and changelog pages.
- Theme assets are documented at `resources/themes/{theme}/assets/css/app.css` and `resources/themes/{theme}/assets/js/app.js`.
- The docs say `npm run dev` handles HMR and `npm run build` creates production assets.
- The active theme is tracked in the root `theme.json`, and the docs show `vite.config.js` reading that file to choose the current theme assets.
- The docs say a minimal custom theme needs a lowercase folder, a `theme.json`, and a `theme.jpg`.
- The theme structure docs describe `assets`, `components`, `pages`, and `partials` plus layout files for authenticated and guest users.
- The docs show `@filamentStyles` and `@livewireStyles` before `@vite(...)` in theme layouts.
- The docs show theme partial inclusion with `@include('theme::partials.alert')`.

## Plug-ins
- Plug-ins are documented in `resources/plugins`.
- Installed plugin names are tracked in `resources/plugins/installed.json`.
- Plugins are activated from `/admin/plugins`.
- The docs describe a main plugin class such as `resources/plugins/example/ExamplePlugin.php`.
- The docs say the plugin `boot()` method is for loading views, migrations, routes, and Livewire components.
- The docs say the plugin `register()` method is for binding services and registering utilities before boot logic runs.
- The plugin docs say the system autoloads classes from the plugin `src` folder with PSR-4 style behavior.
- The documented plugin loading order is: read `installed.json`, instantiate each plugin class, call `register()` on all, then call `boot()` on each.

## Volt Pages And Blade Directives
- The docs say theme `pages` directories are mapped to routes using Laravel Folio.
- The Volt docs show route mapping examples such as `pages/index.blade.php` to `/`, `pages/about.blade.php` to `/about`, and `pages/blog/[post].blade.php` to `/blog/{post}`.
- The docs say these page files can contain single-file Volt components.
- The documented Blade directives include `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`, with `@else` support.
- The docs note that `@subscribed()` expects the full plan name.

## Adding Your Own Functionality
- The `your-functionality` docs say custom logic may be added in familiar Laravel locations such as controllers, models, and services.
- The same docs recommend single-file Volt pages in `resources/themes/{theme}/pages` as the preferred Wave pattern for new functionality.
- The docs say more complex logic can still be moved into services or controllers to keep Volt pages maintainable.
- The documented example adds a `projects` feature through a migration, model, a user relationship, and Volt pages under `resources/themes/{theme}/pages/projects`.
- The docs also point to using FilamentPHP beyond the admin, especially the form and table builders.

## Filament With Volt
- The Wave guide demonstrates using Filament tables and forms directly inside theme Volt pages.
- The guide shows a Volt page implementing `HasForms` and `HasTable`, with `InteractsWithForms` and `InteractsWithTable`.
- Documented Filament table usage includes searchable and sortable `TextColumn` columns and rendering the table with `{{ $this->table }}`.
- Documented Filament form usage includes `TextInput`, `Textarea`, `DatePicker`, `statePath('data')`, reading state with `$this->form->getState()`, and sending a Filament notification after create.
- The guide also shows combining create, view, edit, and delete actions on one page with slide-over actions and a modal.

## Customizations
- The customizations docs say logos live in `resources/views/components/logo.blade.php` and `resources/views/components/logo-icon.blade.php`.
- The docs say logo markup should preserve `{{ $attributes->merge([...]) }}` so classes continue to pass through component usage.
- The docs say favicon files are `public/wave/favicon.png`, `public/wave/favicon-dark.png`, and optionally `/public/favicon.ico`.
- The primary Wave color is documented as `primary_color` in `config/wave.php`.
- Authentication view customization is documented through `/auth/setup` and delegated further to DevDojo Auth docs.

## Upgrading
- The upgrading docs say Wave currently uses a manual upgrade path.
- The documented upgrade step is to replace the root `wave` folder and the `app/Filament` folder with the latest copies, then run `composer dump-autoload` and `php artisan cache:clear`.
- The docs say admin customizations may need to be ported manually.
- The docs say theme upgrades are usually not required unless a new feature introduces corresponding views that you want to bring over.

## Use This Reference For
- Theme, plugin, Volt, and Blade-directive work.
- Documented Wave extension patterns.
- Customization and upgrade guidance that should stay inside the Wave docs boundary.
