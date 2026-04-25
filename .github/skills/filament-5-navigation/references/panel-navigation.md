# Panel Navigation

Use this reference only after a fresh Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Filament 5 panel navigation topic.

## Automatic Navigation
- The retrieved docs state that Filament automatically registers navigation items for resources, custom pages, and clusters.
- When working with cluster details, include only behavior confirmed by the current lookup.

## Custom Navigation Items
The retrieved docs confirm `navigationItems()` with `Filament\Navigation\NavigationItem` for adding custom navigation links.

```php
use Filament\Navigation\NavigationItem;
use Filament\Pages\Dashboard;
use Filament\Panel;
use Filament\Support\Icons\Heroicon;
use function Filament\Support\original_request;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->navigationItems([
            NavigationItem::make('Analytics')
                ->url('https://filament.pirsch.io', shouldOpenInNewTab: true)
                ->icon(Heroicon::OutlinedPresentationChartLine)
                ->group('Reports')
                ->sort(3),
            NavigationItem::make('dashboard')
                ->label(fn (): string => __('filament-panels::pages/dashboard.title'))
                ->url(fn (): string => Dashboard::getUrl())
                ->isActiveWhen(fn () => original_request()->routeIs('filament.admin.pages.dashboard')),
        ]);
}
```

Use only documented `NavigationItem` methods confirmed by the current lookup. The current retrieved snippets confirm `make()`, `url()`, `icon()`, `group()`, `sort()`, `label()`, and `isActiveWhen()`.

## Full Custom Navigation
The retrieved docs confirm `navigation()` with `Filament\Navigation\NavigationBuilder` for replacing the generated navigation structure with a custom structure.

```php
use App\Filament\Pages\Settings;
use App\Filament\Resources\Users\UserResource;
use Filament\Navigation\NavigationBuilder;
use Filament\Navigation\NavigationItem;
use Filament\Pages\Dashboard;
use Filament\Panel;
use Filament\Support\Icons\Heroicon;
use function Filament\Support\original_request;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->navigation(function (NavigationBuilder $builder): NavigationBuilder {
            return $builder->items([
                NavigationItem::make('Dashboard')
                    ->icon(Heroicon::OutlinedHome)
                    ->isActiveWhen(fn (): bool => original_request()->routeIs('filament.admin.pages.dashboard'))
                    ->url(fn (): string => Dashboard::getUrl()),
                ...UserResource::getNavigationItems(),
                ...Settings::getNavigationItems(),
            ]);
        });
}
```

- Use `getNavigationItems()` only for Resources or Pages when the current lookup confirms that surface.
- Do not invent route names for `routeIs()`; preserve route names returned by the current docs or the user's code.

## Custom Navigation Groups
The retrieved docs confirm `navigationGroups()` with `Filament\Navigation\NavigationGroup` objects for customizing navigation groups.

```php
use Filament\Navigation\NavigationGroup;
use Filament\Panel;
use Filament\Support\Icons\Heroicon;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->navigationGroups([
            NavigationGroup::make()
                 ->label('Shop')
                 ->icon(Heroicon::OutlinedShoppingCart),
            NavigationGroup::make()
                ->label('Blog')
                ->icon(Heroicon::OutlinedPencil),
            NavigationGroup::make()
                ->label(fn (): string => __('navigation.settings'))
                ->icon(Heroicon::OutlinedCog6Tooth)
                ->collapsed(),
        ]);
}
```

The retrieved docs also confirm `groups()` inside `navigation()` for custom grouped navigation.

```php
use App\Filament\Pages\HomePageSettings;
use App\Filament\Resources\Categories\CategoryResource;
use App\Filament\Resources\Pages\PageResource;
use Filament\Navigation\NavigationBuilder;
use Filament\Navigation\NavigationGroup;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->navigation(function (NavigationBuilder $builder): NavigationBuilder {
            return $builder->groups([
                NavigationGroup::make('Website')
                    ->items([
                        ...PageResource::getNavigationItems(),
                        ...CategoryResource::getNavigationItems(),
                        ...HomePageSettings::getNavigationItems(),
                    ]),
            ]);
        });
}
```

## Not Confirmed In Current Lookup
Do not add custom item visibility, authorization, badge polling, cluster implementation, menu item APIs, or generated route names unless a narrower Context7 lookup returns them.