# Panel Runtime Configuration

Use this reference after a fresh Context7 lookup for the exact Filament 5 Configuration topic.

## Installation and Providers
- Filament requires PHP 8.2+, Laravel v11.28+, and Tailwind CSS v4.1+.
- Panel Builder installation commands are `composer require filament/filament:"^5.0"` and `php artisan filament:install --panels`.
- Windows PowerShell may require `composer require filament/filament:"~5.0"` because it ignores `^` characters in version constraints.
- Installation creates and registers `app/Providers/Filament/AdminPanelProvider.php`.
- If the panel cannot be accessed, the docs say to check that the service provider is registered in `bootstrap/providers.php`.
- Create a user account with `php artisan make:filament-user`.
- Publish shared Filament package configuration with `php artisan vendor:publish --tag=filament-config`; this creates `config/filament.php`, where the docs mention options such as the default filesystem disk, file generation flags, and UI defaults.
- The default panel lives at `/admin`; resources, custom pages, and dashboard widgets are registered to that panel unless other panels are configured.
- Create another panel with `php artisan make:filament-panel app`; the docs state it creates `app/Providers/Filament/AppPanelProvider.php`, is accessible at `/app`, and may need provider registration in `bootstrap/providers.php` or `config/app.php` depending on Laravel structure.

## Panel Provider Shape
```php
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

## URL, Domain, Width, and Sub-Navigation
- Change the panel path with `path('app')`.
- Use `path('')` to make the app accessible without a prefix; the docs warn that existing `''` or `'/'` routes in `routes/web.php` take precedence.
- Scope the panel to a domain with `domain('admin.example.com')`.
- Change maximum page content width with `maxContentWidth(Width::Full)` using `Filament\Support\Enums\Width`.
- Documented width options are `ExtraSmall`, `Small`, `Medium`, `Large`, `ExtraLarge`, `TwoExtraLarge`, `ThreeExtraLarge`, `FourExtraLarge`, `FiveExtraLarge`, `SixExtraLarge`, `SevenExtraLarge`, `Full`, `MinContent`, `MaxContent`, `FitContent`, `Prose`, `ScreenSmall`, `ScreenMedium`, `ScreenLarge`, `ScreenExtraLarge`, and `ScreenTwoExtraLarge`; the default is `SevenExtraLarge`.
- Change simple-page max width with `simplePageMaxContentWidth(Width::Small)`; the default is `Large`.
- Set the panel-wide sub-navigation position with `subNavigationPosition(SubNavigationPosition::End)` using `Filament\Pages\Enums\SubNavigationPosition`.
- Documented sub-navigation values are `SubNavigationPosition::Start`, `SubNavigationPosition::End`, and `SubNavigationPosition::Top`.

## Lifecycle, SPA, and Unsaved Changes
- `bootUsing(function (Panel $panel) { ... })` runs on every request within that panel.
- In multi-panel apps, only the current panel's `bootUsing()` runs.
- The docs say the `bootUsing()` function runs from middleware after all service providers have been booted.
- Enable SPA mode with `spa()`; it uses Livewire's `wire:navigate`.
- In SPA mode, same-domain URLs are navigated with `wire:navigate` by default.
- Disable SPA navigation for exact URLs with `spaUrlExceptions(fn (): array => [url('/admin'), PostResource::getUrl()])`.
- If using `getUrl()` during configuration, the docs use a callback because panel configuration is too early in the lifecycle for the panel to already be registered.
- Disable SPA navigation for URL patterns with `spaUrlExceptions(['*/admin/posts/*'])`; `*` is a wildcard character.
- Enable SPA prefetching with `spa(hasPrefetching: true)`, which adds Livewire `wire:navigate.hover` behavior.
- The docs warn that prefetching heavy pages can increase bandwidth usage and server load.
- Enable unsaved changes alerts with `unsavedChangesAlerts()`.
- The docs state unsaved changes alerts apply on Resource Create/Edit pages and open action modals.

## Database Transactions
- By default, Filament does not wrap operations in database transactions.
- Enable transactions for all operations with `databaseTransactions()`.
- Opt an action out with `CreateAction::make()->databaseTransaction(false)`.
- Opt an action in with `CreateAction::make()->databaseTransaction()`.
- For Create/Edit resource pages, set `protected ?bool $hasDatabaseTransactions = true;` or `false` on the page class.

## Panel Assets and Render Hooks
- Register assets only for pages within a specific panel with `assets()`:

```php
use Filament\Panel;
use Filament\Support\Assets\Css;
use Filament\Support\Assets\Js;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->assets([
            Css::make('custom-stylesheet', resource_path('css/custom.css')),
            Js::make('custom-script', resource_path('js/custom.js')),
        ]);
}
```

- Before these assets can be used, run `php artisan filament:assets`.
- Register panel-specific Blade render hooks with `renderHook()`:

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

## Middleware and Runtime Switches
- Apply extra middleware to all routes with `middleware([...])`.
- Apply middleware to all authenticated routes with `authMiddleware([...])`.
- By default, `middleware()` and `authMiddleware()` run on first page load but not subsequent Livewire AJAX requests.
- Make those middleware persistent by passing `isPersistent: true` as the second argument.
- Disable automatic Echo connection in a panel with `broadcasting(false)`.
- Enable strict authorization with `strictAuthorization()`; the docs state Filament otherwise grants access when a policy or policy method does not exist.

## Error Notifications
- When Laravel debug mode is disabled, Filament replaces Livewire full-screen error modals with flash notifications.
- Disable that behavior with `errorNotifications(false)`.
- Customize the default error notification text with `registerErrorNotification(title: 'An error occurred', body: 'Please try again later.')`.
- Register notification text for a status code with `registerErrorNotification(..., statusCode: 404)`.
- Hide a notification for a status code with `hiddenErrorNotification(403)`.
- Disable Filament's error notification handling for a status code with `disabledErrorNotification(503)`.
- On pages, use `protected ?bool $hasErrorNotifications = true;`, `protected ?bool $hasErrorNotifications = false;`, `hasErrorNotifications(): bool`, or `setUpErrorNotifications()` with page-level `registerErrorNotification()`, `hiddenErrorNotification()`, and `disabledErrorNotification()`.

## Plugins and Distributed Panels
- Plugin classes implement `Filament\Contracts\Plugin`.
- A plugin class has documented `getId(): string`, `register(Panel $panel): void`, and `boot(Panel $panel): void` methods.
- `getId()` returns a unique plugin identifier.
- `register()` can use panel configuration options such as resources, pages, themes, and render hooks.
- `boot()` runs only when the panel that the plugin is registered to is in use; it is executed by middleware.
- Add a plugin to a panel with `plugin(new BlogPlugin())`.
- A documented fluent plugin pattern adds `public static function make(): static { return app(static::class); }` and registers with `plugin(BlogPlugin::make())`.
- For per-panel plugin options, the docs suggest a setter and getter for each option, with the setter storing a property and returning `static` for fluent chaining.
- Access a plugin by ID with `filament('blog')->hasAuthorResource()`.
- A documented type-friendly retrieval pattern adds `public static function get(): static { return filament(app(static::class)->getId()); }` and calls `BlogPlugin::get()->hasAuthorResource()`.
- A package can distribute a whole panel by providing a `PanelProvider` service provider and registering it in Composer `extra.laravel.providers`.