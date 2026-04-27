# Pluralization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x localization, translation pluralization, and pluralizer language configuration.

## Pluralized Translation Strings
The docs show pipe-delimited pluralized translation strings:

```php
'apples' => 'There is one apple|There are many apples';
```

The docs show exact-count and range forms:

```php
'apples' => '{0} There are none|[1,19] There are some|[20,*] There are many';
```

The docs show retrieving pluralized strings with `trans_choice(...)`:

```php
echo trans_choice('messages.apples', 10);
```

The docs show placeholders in pluralized strings:

```php
'minutes_ago' => '{1} :value minute ago|[2,*] :value minutes ago';
echo trans_choice('time.minutes_ago', 5, ['value' => 5]);

'apples' => '{0} There are none|{1} There is one|[2,*] There are :count';
```

Confirmed helper and placeholder examples: `trans_choice(...)`, `:value`, and `:count`.

## JSON Pluralized Translations
The docs show JSON pluralized translation strings:

```json
{
    "There is one apple|There are many apples": "Hay una manzana|Hay muchas manzanas"
}
```

## Pluralizer Language
The docs state Laravel includes a pluralizer utility that converts singular strings to plural and is commonly used by Eloquent ORM.

The docs state the pluralizer uses English by default.

The docs state supported pluralizer languages include French, Norwegian Bokmal, Portuguese, Spanish, and Turkish.

The docs show configuring the pluralizer language in a service provider `boot()` method:

```php
use Illuminate\Support\Pluralizer;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Pluralizer::useLanguage('spanish');

    // ...
}
```

Confirmed import and method: `Illuminate\Support\Pluralizer` and `Pluralizer::useLanguage(...)`.

The docs state that if this setting is changed, it is best practice to explicitly define Eloquent model table names to avoid unexpected behavior.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using languages beyond the returned list, custom pluralization rules, pluralizer internals, exact Eloquent table-name side effects, pluralization behavior for non-Eloquent strings outside the returned docs, or translation pluralization edge cases beyond exact counts, ranges, and pipe-delimited examples.
