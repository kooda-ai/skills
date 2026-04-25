# Render Hook Patterns

Use this reference after a fresh Context7 lookup for the exact Filament 5 render-hook topic.

## What Render Hooks Are For
- Render hooks allow Blade content to be rendered at specific points within Filament framework views.
- The docs describe them as useful for plugins that inject HTML into the framework.
- The docs also describe them as useful for users because Filament does not recommend publishing framework views due to increased breaking-change risk.

## Registering Global Hooks
- Register hooks with `Filament\Support\Facades\FilamentView::registerRenderHook()`.
- Call `registerRenderHook()` from a service provider or middleware.
- The first argument is the hook name.
- The second argument is a callback that returns the rendered content.

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Support\Facades\Blade;

FilamentView::registerRenderHook(
    PanelsRenderHook::BODY_START,
    fn (): string => Blade::render('@livewire(\'livewire-ui-modal\')'),
);
```

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    PanelsRenderHook::BODY_START,
    fn (): View => view('impersonation-banner'),
);
```

## Registering Panel Hooks
- Panel configuration can register panel-specific render hooks with `renderHook()`.
- The documented panel example integrates Blade content into a panel at a specific point.

```php
use Filament\Panel;
use Filament\View\PanelsRenderHook;
use Illuminate\Support\Facades\Blade;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->renderHook(
            PanelsRenderHook::BODY_START,
            fn (): string => Blade::render('@livewire(\'livewire-ui-modal\')'),
        );
}
```

## Choosing a Hook Family
- Panel Builder hooks use `Filament\View\PanelsRenderHook`.
- Table Builder hooks use `Filament\Tables\View\TablesRenderHook`.
- Actions hooks use `Filament\Actions\View\ActionsRenderHook`.
- Widgets hooks use `Filament\Widgets\View\WidgetsRenderHook`.

## Scoping Hooks
- Some hooks can be scoped so they are only output on a specific page or Livewire component.
- Pass a class string with the `scopes` argument to `registerRenderHook()`.
- Pass an array of class strings with `scopes` to register a hook for multiple scopes.
- Some Panel Builder hooks allow scoping to all pages in a resource by passing the resource class.
- Active scopes can be retrieved inside the callback with an `array $scopes` parameter.

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    PanelsRenderHook::PAGE_START,
    fn (): View => view('warning-banner'),
    scopes: \App\Filament\Resources\Users\Pages\EditUser::class,
);
```

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    PanelsRenderHook::PAGE_START,
    fn (): View => view('warning-banner'),
    scopes: [
        \App\Filament\Resources\Users\Pages\CreateUser::class,
        \App\Filament\Resources\Users\Pages\EditUser::class,
    ],
);
```

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    PanelsRenderHook::PAGE_START,
    fn (): View => view('warning-banner'),
    scopes: \App\Filament\Resources\Users\UserResource::class,
);
```

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    PanelsRenderHook::PAGE_START,
    fn (array $scopes): View => view('warning-banner', ['scopes' => $scopes]),
    scopes: \App\Filament\Resources\Users\UserResource::class,
);
```

## Passing Data to Hooks
- Render hooks can receive data from the place where the hook is rendered.
- Access hook data by adding an `array $data` parameter to the callback.
- The documented `TablesRenderHook::FILTER_INDICATORS` example receives `filterIndicators` data.

```php
use Filament\Support\Facades\FilamentView;
use Filament\Tables\View\TablesRenderHook;
use Illuminate\Contracts\View\View;

FilamentView::registerRenderHook(
    TablesRenderHook::FILTER_INDICATORS,
    fn (array $data): View => view('filter-indicators', ['indicators' => $data['filterIndicators']]),
);
```

## Rendering Custom Hooks
- Plugin developers can expose render hooks to users by outputting `FilamentView::renderHook()` in Blade.
- Hooks rendered with `renderHook()` do not need to be registered separately.
- Pass scope information with the `scopes:` argument.
- Pass data with the `data:` argument.

```blade
{{ \Filament\Support\Facades\FilamentView::renderHook(\Filament\View\PanelsRenderHook::PAGE_START) }}
```

```blade
{{ \Filament\Support\Facades\FilamentView::renderHook(\Filament\View\PanelsRenderHook::PAGE_START, scopes: $this->getRenderHookScopes()) }}
```

```blade
{{ \Filament\Support\Facades\FilamentView::renderHook(\Filament\View\PanelsRenderHook::PAGE_START, scopes: [static::class, \App\Filament\Resources\Users\UserResource::class]) }}
```

```blade
{{ \Filament\Support\Facades\FilamentView::renderHook(\Filament\Tables\View\TablesRenderHook::FILTER_INDICATORS, data: ['filterIndicators' => $filterIndicators]) }}
```

## Decision Flow
1. If the content should be added only inside one configured panel, consider the documented `Panel::renderHook()` shortcut.
2. If the content should be registered from an application service provider, middleware, or plugin service provider, use `FilamentView::registerRenderHook()`.
3. If the hook belongs to a Filament panel page, navigation, auth, layout, content area, scripts, styles, or resource page area, choose `PanelsRenderHook`.
4. If the hook belongs to a table header, toolbar, filter indicators, column manager, grouping selector, reorder trigger, search, selection indicator, or header cell, choose `TablesRenderHook`.
5. If the hook belongs to action modal custom content or modal schema placement, choose `ActionsRenderHook`.
6. If the hook belongs to a table widget wrapper, choose `WidgetsRenderHook`.
7. If the hook is exposed by plugin Blade, use `FilamentView::renderHook()` and pass documented scopes or data at the render point.