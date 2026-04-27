# Locale Configuration

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x localization, helpers, validation language files, and initial configuration.

## Application Locale
The docs state the default language for a Laravel application is defined in `config/app.php` using the `locale` option.

The docs state this option is typically controlled by the `APP_LOCALE` environment variable.

The docs state a fallback language may be defined via `APP_FALLBACK_LOCALE`, ensuring the application can display content when a translation is missing in the primary language.

The broader configuration docs also recommend reviewing `config/app.php` options like `url` and `locale`.

## Publishing Language Files
The docs show publishing default language files and scaffolding the `lang` directory:

```shell
php artisan lang:publish
```

The docs state this command is necessary for customizing or creating your own language files.

The validation docs state Laravel stores default validation error messages in `lang/en/validation.php`. If this directory is missing, it can be generated with `php artisan lang:publish`, and the files may be modified or copied to other language directories to support localization.

## Language Directory Path
The helper docs show retrieving the fully qualified path to the application's `lang` directory:

```php
$path = lang_path();
```

The docs also show generating a path to a file within the `lang` directory:

```php
$path = lang_path('en/messages.php');
```

Confirmed helper: `lang_path(...)`.

## Runtime Locale Switching
The docs show setting the application locale for a single HTTP request with the `App` facade:

```php
use Illuminate\Support\Facades\App;

Route::get('/greeting/{locale}', function (string $locale) {
    if (! in_array($locale, ['en', 'es', 'fr'])) {
        abort(400);
    }

    App::setLocale($locale);

    // ...
});
```

Confirmed import and methods: `Illuminate\Support\Facades\App`, `App::setLocale(...)`, `in_array(...)`, and `abort(400)` in the returned example.

## Current Locale Inspection
The docs show retrieving and checking the current application locale:

```php
use Illuminate\Support\Facades\App;

$locale = App::currentLocale();

if (App::isLocale('en')) {
    // ...
}
```

Confirmed methods: `App::currentLocale()` and `App::isLocale(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using locale middleware, browser language negotiation, persisted locale storage in sessions or cookies, route groups for locales, exact `config/app.php` array examples beyond the returned option names, validation attribute/value localization, or language-file publishing details beyond `lang:publish`.
