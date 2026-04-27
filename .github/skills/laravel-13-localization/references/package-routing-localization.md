# Package And Routing Localization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x localization, packages, and controllers.

## Loading Package Translations
The package docs show loading package language files from a service provider `boot()` method:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadTranslationsFrom(__DIR__.'/../lang', 'courier');
}
```

The docs state translation lines are referenced using `package::file.line` syntax, such as:

```php
trans('courier::messages.welcome')
```

Confirmed method and syntax: `loadTranslationsFrom(...)` and `package::file.line`.

## Loading Package JSON Translations
The package docs show loading JSON translation files for a package:

```php
/**
 * Bootstrap any package services.
 */
public function boot(): void
{
    $this->loadJsonTranslationsFrom(__DIR__.'/../lang');
}
```

Confirmed method: `loadJsonTranslationsFrom(...)`.

## Publishing Package Language Files
The package docs show publishing package language files to the application's `lang/vendor` directory:

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

Confirmed methods: `loadTranslationsFrom(...)`, `publishes(...)`, and `$this->app->langPath(...)`.

The docs state this allows users to override translations via the `vendor:publish` Artisan command.

Run a fresh lookup before writing exact publish tags or command arguments.

## Overriding Package Language Files
The localization docs state package translation files may be overridden by placing files in `lang/vendor/{package}/{locale}`.

The docs give this example for overriding English `messages.php` translation strings for package `skyrim/hearthfire`:

```text
lang/vendor/hearthfire/en/messages.php
```

The docs state only the translation strings to override should be defined in that file. Any strings not overridden are still loaded from the package's original language files.

## Localized Resource Route Verbs
The controllers docs show customizing resource route verbs for the `create` and `edit` actions in `AppServiceProvider`:

```php
/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Route::resourceVerbs([
        'create' => 'crear',
        'edit' => 'editar',
    ]);
}
```

The docs state resource URIs default to English verbs and pluralization rules, and `Route::resourceVerbs(...)` customizes the `create` and `edit` verbs.

Run a fresh lookup before writing the exact `Route` import for this snippet.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using package publish tags, package provider registration details, package translation testing, JSON translation overrides, package translation fallback behavior, localized resource route examples beyond `create` and `edit`, route localization middleware, or route model binding interactions with localized URIs.
