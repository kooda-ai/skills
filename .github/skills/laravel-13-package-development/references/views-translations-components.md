# Package Views, Translations, And Components

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x package views, translations, and Blade components.

## Package Views
The docs show loading package views with a namespace from a service provider `boot()` method:

```php
public function boot(): void
{
    $this->loadViewsFrom(__DIR__.'/../resources/views', 'courier');
}
```

The docs show referencing the package view with `package::view` syntax:

```php
Route::get('/dashboard', function () {
    return view('courier::dashboard');
});
```

Confirmed method and namespace syntax: `loadViewsFrom(...)` and `courier::dashboard`.

Run a fresh lookup before writing exact imports for `Route` in this example.

## Publishing Views
The docs show making package views publishable:

```php
public function boot(): void
{
    $this->loadViewsFrom(__DIR__.'/../resources/views', 'courier');

    $this->publishes([
        __DIR__.'/../resources/views' => resource_path('views/vendor/courier'),
    ]);
}
```

Confirmed helper and path: `resource_path('views/vendor/courier')`.

## Package Translations
The docs show loading package language files:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadTranslationsFrom(__DIR__.'/../lang', 'courier');
}
```

The docs state translations may be accessed using `package::file.line` syntax, such as:

```php
trans('courier::messages.welcome')
```

The docs show registering package JSON translation files:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadJsonTranslationsFrom(__DIR__.'/../lang');
}
```

Confirmed methods: `loadTranslationsFrom(...)` and `loadJsonTranslationsFrom(...)`.

## Publishing Language Files
The docs show publishing package language files to the application's `lang/vendor` directory:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadTranslationsFrom(__DIR__.'/../lang', 'courier');

    $this->publishes([
        __DIR__.'/../lang' => $this->app->langPath('vendor/courier'),
    ]);
}
```

The localization docs state package translation overrides may be placed in `lang/vendor/{package}/{locale}`. The returned example places an English `messages.php` override for package `skyrim/hearthfire` at `lang/vendor/hearthfire/en/messages.php`.

## Blade Components
The docs show registering a package Blade component:

```php
public function boot(): void
{
    Blade::component('package-alert', AlertComponent::class);
}
```

```blade
<x-package-alert/>
```

The docs also show package component namespace registration:

```php
public function boot(): void
{
    Blade::componentNamespace('Nightshade\\Views\\Components', 'nightshade');
}
```

```blade
<x-nightshade::calendar />
<x-nightshade::color-picker />
```

The Blade docs confirm the facade import for component registration:

```php
use Illuminate\Support\Facades\Blade;
```

The docs show registering anonymous component paths:

```php
public function boot(): void
{
    Blade::anonymousComponentPath(__DIR__.'/../components');
    Blade::anonymousComponentPath(__DIR__.'/../components', 'dashboard');
}
```

```blade
<x-panel />
<x-dashboard::panel />
```

The package docs state package anonymous components must be located in a `components` directory inside the package's main view directory as defined by `loadViewsFrom(...)`, and an anonymous component named `alert` in the `courier` package may be rendered as `<x-courier::alert />`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using class-based component constructor APIs, component rendering internals, view composers, view namespaces beyond shown examples, publishing view tags, translation fallback behavior, package locale file layouts beyond shown paths, component autoloading edge cases, or package Livewire/Inertia view behavior.
