# Modular Plugins and Distributed Panels

Use this reference after a fresh Context7 lookup for the exact Filament 5 modular architecture or distributed panel topic.

## Modular Architecture Context
- The docs describe modular architecture for large-scale Filament applications that use Domain-Driven Design principles.
- A domain can be structured as a separate Composer package, typically located in an `app-modules/` directory.
- The docs list module contents as models and business logic, Filament resources, pages, widgets, a service provider, routes, views, configurations, and tests.
- The docs show installing InterNACHI/Modular with:

```bash
composer require internachi/modular
```

- The docs show creating a module with:

```bash
php artisan make:module alerts
```

- The docs show each module requiring `filament/filament` and defining its service provider in Composer metadata.

```json
{
    "name": "my-app/alerts",
    "type": "library",
    "require": {
        "filament/filament": "^5.0"
    },
    "autoload": {
        "psr-4": {
            "Modules\\Alerts\\": "src/"
        }
    },
    "extra": {
        "laravel": {
            "providers": [
                "Modules\\Alerts\\Providers\\AlertsServiceProvider"
            ]
        }
    }
}
```

## Module Plugin Class
- The docs state each module should define its own Filament plugin that registers its resources, pages, and widgets.

```php
namespace Modules\Alerts;

use Filament\Contracts\Plugin;
use Filament\Panel;

class AlertsPlugin implements Plugin
{
    public function getId(): string
    {
        return 'alerts';
    }

    public static function make(): static
    {
        return app(static::class);
    }

    public function register(Panel $panel): void
    {
        $panel
            ->discoverResources(
                in: __DIR__ . '/Filament/Resources',
                for: 'Modules\\Alerts\\Filament\\Resources',
            )
            ->discoverPages(
                in: __DIR__ . '/Filament/Pages',
                for: 'Modules\\Alerts\\Filament\\Pages',
            )
            ->discoverWidgets(
                in: __DIR__ . '/Filament/Widgets',
                for: 'Modules\\Alerts\\Filament\\Widgets',
            );
    }

    public function boot(Panel $panel): void
    {
        //
    }
}
```

## Conditional Panel Registration
- The docs state that in multi-panel apps such as `admin`, `app`, and `portal`, modules often need to register plugins only for specific panels.
- Use `Panel::configureUsing()` in the module service provider to conditionally register plugins.

```php
namespace Modules\Alerts\Providers;

use Filament\Panel;
use Illuminate\Support\ServiceProvider;
use Modules\Alerts\AlertsPlugin;

class AlertsServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        Panel::configureUsing(function (Panel $panel): void {
            if ($panel->getId() !== 'admin') {
                return;
            }

            $panel->plugin(AlertsPlugin::make());
        });
    }
}
```

- For multiple panels or different plugin configuration per panel, the docs show a `match` statement that calls `$panel->plugin()` directly.

```php
namespace Modules\Alerts\Providers;

use Filament\Panel;
use Illuminate\Support\ServiceProvider;
use Modules\Alerts\AlertsPlugin;

class AlertsServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        Panel::configureUsing(function (Panel $panel): void {
            match ($panel->getId()) {
                'admin' => $panel->plugin(
                    AlertsPlugin::make()->enableAdminFeatures(),
                ),
                'staff' => $panel->plugin(
                    AlertsPlugin::make(),
                ),
                default => null,
            };
        });
    }
}
```

- The docs state this lets each plugin instance be configured differently based on the panel, while unmatched panels do not receive the plugin.
- The docs state `Panel::configureUsing()` allows modules to configure themselves without requiring changes to panel provider files.

## Sharing Resources Between Panels
- The docs show sharing a resource between panels by registering the same resource from a plugin and enabling capabilities with per-panel plugin configuration.
- A documented example stores a `canManageRoles` boolean, exposes `canManageRoles(bool $condition = true): static`, reads it with `hasRoleManagement(): bool`, registers `UserResource::class`, and registers different plugin instances per panel through `Panel::configureUsing()`.

## Registering Livewire Components from Modules
- If a module contains custom Livewire components used by Filament, such as custom pages or widgets, the docs show registering them in the plugin `boot()` method.

```php
use Livewire\Livewire;
use Modules\Alerts\Filament\Pages\AlertsDashboard;

public function boot(Panel $panel): void
{
    Livewire::component('alerts-dashboard', AlertsDashboard::class);
}
```

## Distributing a Full Panel
- The docs state a Laravel package can distribute an entire panel.
- The panel configuration class extends `Filament\PanelProvider`, which is a standard Laravel service provider.

```php
<?php

namespace DanHarrin\FilamentBlog;

use Filament\Panel;
use Filament\PanelProvider;

class BlogPanelProvider extends PanelProvider
{
    public function panel(Panel $panel): Panel
    {
        return $panel
            ->id('blog')
            ->path('blog')
            ->resources([
                // ...
            ])
            ->pages([
                // ...
            ])
            ->widgets([
                // ...
            ])
            ->middleware([
                // ...
            ])
            ->authMiddleware([
                // ...
            ]);
    }
}
```

- The docs state this provider should be registered in the package Composer metadata.

```json
"extra": {
    "laravel": {
        "providers": [
            "DanHarrin\\FilamentBlog\\BlogPanelProvider"
        ]
    }
}
```