# Translation Strings

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x localization and translation strings.

## PHP Language Files With Short Keys
The docs state translation strings are typically stored in files within the `lang` directory, with subdirectories for each supported language.

The docs show this structure:

```text
/lang
    /en
        messages.php
    /es
        messages.php
```

The docs say language directories that differ by territory should use ISO 15897 naming conventions, such as `en_GB` for British English.

The docs show a PHP language file returning keyed strings:

```php
<?php

// lang/en/messages.php

return [
    'welcome' => 'Welcome to our application!',
];
```

## JSON Translation Files
The docs state applications with many translatable strings may use the default translation string itself as the key.

The docs show a Spanish JSON translation file in `lang/es.json`:

```json
{
    "I love programming.": "Me encanta programar."
}
```

The docs warn that when using translation strings as keys, a key matching a translation filename may cause the translator to return the entire file content instead of the intended translation.

## Retrieving Translation Strings
The docs show retrieving translations with the `__()` helper:

```php
echo __('messages.welcome');
echo __('I love programming.');
```

The docs show the Blade form:

```blade
{{ __('messages.welcome') }}
```

Confirmed helper: `__(...)`.

## Replacement Parameters
The docs show placeholders prefixed with a colon and replacements passed as the second argument to `__()`:

```php
// Definition
'welcome' => 'Welcome, :name',

// Usage
echo __('messages.welcome', ['name' => 'dayle']);
```

The docs state replacements are automatically capitalized if the placeholder is in all caps or only the first letter is capitalized.

## Object Replacement Formatting
The docs state that if an object is provided as a translation placeholder, the object's `__toString()` method is invoked by default.

The docs show registering custom object formatting with the `Lang` facade:

```php
use Illuminate\Support\Facades\Lang;
use Money\Money;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Lang::stringable(function (Money $money) {
        return $money->formatTo('en_GB');
    });
}
```

The docs state the `stringable` method should typically be invoked within the `boot` method of the application's `AppServiceProvider` class.

Confirmed import and method: `Illuminate\Support\Facades\Lang` and `Lang::stringable(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using custom missing translation behavior, nested key behavior beyond dot syntax, validation translation customization beyond the validation-language-file baseline, translation namespaces, Blade escaping details beyond the returned `{{ __('...') }}` example, custom translator bindings, or translation testing helpers.
