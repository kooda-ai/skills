# Module Panel Registration

Use this reference after a fresh Context7 lookup for the exact Filament 5 module plugin, panel registration, or Livewire component topic.

## Module Plugin Class
- The docs state each module should define its own Filament plugin that registers its resources, pages, and widgets.
- The documented module plugin implements `Filament\Contracts\Plugin` and uses `Filament\Panel`.
- The documented plugin class has `getId(): string`, `public static function make(): static`, `register(Panel $panel): void`, and `boot(Panel $panel): void`.

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
- The docs show using `Panel::configureUsing()` in a module service provider.
- The docs show checking `$panel->getId()` to restrict a module plugin to a specific panel.
- The docs show `$panel->plugin(AlertsPlugin::make())` to attach the module plugin.

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

## Different Configuration Per Panel
- The docs show a `match ($panel->getId())` expression when different panels receive different plugin configuration.
- The docs show an `admin` panel receiving a configured plugin instance and a `staff` panel receiving the default plugin instance.

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

## Documented Plugin Option Shape
- The docs show a module plugin storing a boolean option in a protected property.
- The docs show a fluent setter returning `static` and a getter returning the option value.
- The docs show registering different plugin instances for different panels through `Panel::configureUsing()`.

```php
namespace Modules\Users;

use Filament\Contracts\Plugin;
use Filament\Panel;
use Modules\Users\Filament\Resources\UserResource;

class UsersPlugin implements Plugin
{
    protected bool $canManageRoles = false;

    public function getId(): string
    {
        return 'users';
    }

    public static function make(): static
    {
        return app(static::class);
    }

    public function canManageRoles(bool $condition = true): static
    {
        $this->canManageRoles = $condition;

        return $this;
    }

    public function hasRoleManagement(): bool
    {
        return $this->canManageRoles;
    }

    public function register(Panel $panel): void
    {
        $panel->resources([
            UserResource::class,
        ]);
    }

    public function boot(Panel $panel): void
    {
        //
    }
}
```

```php
Panel::configureUsing(function (Panel $panel): void {
    match ($panel->getId()) {
        'admin' => $panel->plugin(
            UsersPlugin::make()->canManageRoles(),
        ),
        'staff' => $panel->plugin(
            UsersPlugin::make(),
        ),
        default => null,
    };
});
```

## Livewire Components from Modules
- If a module contains custom Livewire components used by Filament, the docs show registering them in the plugin `boot()` method.

```php
use Livewire\Livewire;
use Modules\Alerts\Filament\Pages\AlertsDashboard;

public function boot(Panel $panel): void
{
    Livewire::component('alerts-dashboard', AlertsDashboard::class);
}
```