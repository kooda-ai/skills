# Assets and Render Hooks

Use this reference after a fresh Context7 lookup for the exact Filament 5 asset or render-hook topic.

## FilamentAsset Facade
- All packages in the Filament ecosystem share an asset management system.
- The asset system lets official and third-party plugins register CSS and JavaScript files that can be consumed by Blade views.
- Use `Filament\Support\Facades\FilamentAsset` to register files.
- Registered files may come from anywhere in the filesystem and are copied into `/public` when `php artisan filament:assets` runs.
- Asset IDs are chosen by the developer and used as file names and references in Blade views.
- Use `FilamentAsset::register()` in the `boot()` method of a service provider.
- For plugin assets, pass the Composer package name as the `package` argument so assets are copied into their own public directory.

```php
use Filament\Support\Facades\FilamentAsset;

public function boot(): void
{
    FilamentAsset::register([
        // ...
    ]);
}
```

## CSS Assets
- Register CSS with `Filament\Support\Assets\Css`:

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('custom-stylesheet', __DIR__ . '/../../resources/css/custom.css'),
]);
```

- When `php artisan filament:assets` runs, the CSS file is copied into `/public` and loaded into all Blade views that use Filament.
- Register plugin CSS assets with `FilamentAsset::register([...], package: 'danharrin/filament-blog')`.
- The docs advise plugin authors not to build Tailwind CSS files into plugins in most cases; instead, provide raw CSS and instruct users to add the plugin vendor directory to their custom theme with an `@source` directive.
- Registered CSS files load in the `<head>` of every Filament page by default.
- For lazy CSS, use Alpine `x-load-css` with `FilamentAsset::getStyleHref('custom-stylesheet')`.
- Prevent automatic CSS loading with `Css::make(...)->loadedOnRequest()`.
- If the CSS belongs to a plugin, pass `package: 'danharrin/filament-blog'` to `getStyleHref()`.
- Register URL-based CSS with `Css::make('example-external-stylesheet', 'https://example.com/external.css')` or `Css::make('example-local-stylesheet', asset('css/local.css'))`.
- URL-based CSS is loaded on every page as normal but is not copied into `/public` by `php artisan filament:assets`.
- Register CSS variables with `FilamentAsset::registerCssVariables(['background-image' => asset('images/background.jpg')])`.
- Access registered CSS variables as `var(--background-image)`.

## JavaScript Assets
- Register JavaScript with `Filament\Support\Assets\Js`:

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Js::make('custom-script', __DIR__ . '/../../resources/js/custom.js'),
]);
```

- When `php artisan filament:assets` runs, the JavaScript file is copied into `/public` and loaded into all Blade views that use Filament.
- JavaScript files load at the bottom of every Filament page by default.
- For lazy JavaScript, use Alpine `x-load-js` with `FilamentAsset::getScriptSrc('custom-script')`.
- Prevent automatic JavaScript loading with `Js::make(...)->loadedOnRequest()`.
- If the JavaScript belongs to a plugin, pass `package: 'danharrin/filament-blog'` to `getScriptSrc()`.
- Register script data with `FilamentAsset::registerScriptData(['user' => ['name' => auth()->user()?->name]])`.
- Access registered script data at runtime with `window.filamentData.user.name`.
- Register URL-based JavaScript with `Js::make('example-external-script', 'https://example.com/external.js')` or `Js::make('example-local-script', asset('js/local.js'))`.
- The `php artisan filament:assets` command copies JavaScript files as-is and does not bundle or resolve npm imports.
- For JavaScript requiring bundling, compile with Vite first, then register the compiled output with `Js::make('timezone', Vite::asset('resources/js/timezone.js'))` using `Illuminate\Support\Facades\Vite`.
- Since `Vite::asset()` returns a URL, that asset is served from Vite build output and not copied by `php artisan filament:assets`.

## Asynchronous Alpine Components
- The docs recommend `esbuild` for bundled asynchronous Alpine components.
- Install esbuild with `npm install esbuild --save-dev`.
- Register a compiled Alpine component with `Filament\Support\Assets\AlpineComponent`:

```php
use Filament\Support\Assets\AlpineComponent;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    AlpineComponent::make('test-component', __DIR__ . '/../../resources/js/dist/components/test-component.js'),
]);
```

- Load the component in a view with `x-load`, `x-load-src="{{ \Filament\Support\Facades\FilamentAsset::getAlpineComponentSrc('test-component') }}"`, and `x-data="testComponent(...)"`.
- The `x-load` attributes come from the Async Alpine package, and the docs state any features of that package can be used.

## Registering Render Hooks
- Render hooks render Blade content at various points in Filament framework views.
- The docs say render hooks are useful for plugins and for users because publishing Filament views is not recommended due to increased breaking-change risk.
- Register render hooks with `Filament\Support\Facades\FilamentView::registerRenderHook()` from a service provider or middleware.
- The first argument is the hook name and the second is a callback returning rendered content.

```php
use Filament\Support\Facades\FilamentView;
use Filament\View\PanelsRenderHook;
use Illuminate\Support\Facades\Blade;

FilamentView::registerRenderHook(
    PanelsRenderHook::BODY_START,
    fn (): string => Blade::render('@livewire(\'livewire-ui-modal\')'),
);
```

- A render hook may return a view, such as `fn (): View => view('impersonation-banner')`.
- Panel configuration can register panel-specific render hooks with `$panel->renderHook(...)`; see [panel-runtime.md](./panel-runtime.md).

## Scoping and Data
- Some render hooks can be scoped to a specific page, Livewire component, relation manager, table widget, or all pages in a resource.
- Pass a class string or array of class strings with the `scopes` argument to `registerRenderHook()`.
- The docs show retrieving active scopes by adding `array $scopes` to the render-hook callback.
- Render hooks can receive data from the point where the hook is rendered.
- Access hook data by injecting `array $data` in the callback.
- Example: `TablesRenderHook::FILTER_INDICATORS` receives `filterIndicators` data as `array<Filament\Tables\Filters\Indicator>`.

## Rendering Custom Hooks
- Plugin developers may expose render hooks by outputting `FilamentView::renderHook()` in Blade.
- Pass scopes to `renderHook()` with the `scopes` argument.
- Pass data to `renderHook()` with the `data` argument.

## Hook Families Confirmed in Docs
- Panel Builder hooks use `Filament\View\PanelsRenderHook`.
- Table Builder hooks use `Filament\Tables\View\TablesRenderHook`.
- Actions hooks use `Filament\Actions\View\ActionsRenderHook`.
- Widgets hooks use `Filament\Widgets\View\WidgetsRenderHook`.
- Confirmed Panel Builder hook examples include `BODY_START`, `BODY_END`, `HEAD_START`, `HEAD_END`, `CONTENT_BEFORE`, `CONTENT_AFTER`, `PAGE_START`, `PAGE_END`, `SIDEBAR_NAV_START`, `SIDEBAR_NAV_END`, `TOPBAR_START`, `TOPBAR_END`, `USER_MENU_BEFORE`, `USER_MENU_AFTER`, `TENANT_MENU_BEFORE`, and `TENANT_MENU_AFTER`.
- Confirmed Table Builder hook examples include `FILTER_INDICATORS`, `HEADER_CELL`, `HEADER_BEFORE`, `HEADER_AFTER`, `TOOLBAR_START`, `TOOLBAR_END`, `TOOLBAR_BEFORE`, `TOOLBAR_AFTER`, `TOOLBAR_SEARCH_BEFORE`, and `TOOLBAR_SEARCH_AFTER`.
- Confirmed Actions hook examples include `MODAL_CUSTOM_CONTENT_BEFORE`, `MODAL_CUSTOM_CONTENT_AFTER`, `MODAL_CUSTOM_CONTENT_FOOTER_BEFORE`, `MODAL_CUSTOM_CONTENT_FOOTER_AFTER`, `MODAL_SCHEMA_BEFORE`, and `MODAL_SCHEMA_AFTER`.
- Confirmed Widgets hook examples include `TABLE_WIDGET_START` and `TABLE_WIDGET_END`.