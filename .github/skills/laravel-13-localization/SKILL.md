---
name: laravel-13-localization
description: 'Use when: working with Laravel 13 localization, lang directory, php artisan lang:publish, lang_path(), APP_LOCALE, APP_FALLBACK_LOCALE, config/app.php locale, App::setLocale(), App::currentLocale(), App::isLocale(), translation strings, __(), short keys, JSON translation files, translation placeholders, Lang::stringable(), trans_choice(), pluralization ranges, Pluralizer::useLanguage(), Route::resourceVerbs(), package translations, loadTranslationsFrom(), loadJsonTranslationsFrom(), language overrides, and Laravel 13 localization code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 localization, translations, locale, pluralizer, resource verbs, package translations, or review task'
---

# Laravel 13 Localization

## Purpose
Use this skill to create, review, or explain Laravel 13 localization, translation strings, locale switching, pluralized translations, pluralizer language configuration, localized resource route verbs, and package translation overrides using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact localization topic.
2. Do not add locale config keys, environment variables, commands, language file paths, helper names, facade methods, placeholder behavior, pluralization syntax, package translation methods, route localization APIs, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented file paths, locale names, method names, command names, helper names, package namespaces, translation key syntax, and example values.
5. Do not infer behavior from older Laravel versions, Symfony translation docs, package source code, blog posts, locale standards beyond the returned ISO 15897 statement, browser language negotiation, or general Laravel/PHP memory.

## Reference Map
- Locale configuration, `APP_LOCALE`, `APP_FALLBACK_LOCALE`, `php artisan lang:publish`, `lang_path()`, `App::setLocale()`, `App::currentLocale()`, and `App::isLocale()`: [locale-configuration.md](./references/locale-configuration.md)
- Short-key language files, JSON translations, `__()`, replacement placeholders, automatic replacement capitalization, `Lang::stringable()`, and filename/key conflict boundary: [translation-strings.md](./references/translation-strings.md)
- `trans_choice()`, pluralization ranges, `:count` / custom placeholders, JSON pluralized strings, `Pluralizer::useLanguage()`, supported pluralizer languages, and Eloquent table-name boundary: [pluralization.md](./references/pluralization.md)
- Package translation loading, JSON package translations, package language file publishing, overriding package language files, and localized resource route verbs: [package-routing-localization.md](./references/package-routing-localization.md)

## Workflow
1. Identify the exact surface: default locale, fallback locale, language file publishing, language directory path, runtime locale switch, current locale inspection, PHP language file, JSON translation file, translation retrieval, placeholder replacement, object placeholder formatting, pluralized translation, pluralizer language, resource route verb localization, package translation loading, package translation publishing, package translation override, or code review.
2. Query Context7 for that exact Laravel 13 localization topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, paths, helpers, facades, methods, locale examples, imports, and translation formats.
5. For locale topics not in the references, such as locale negotiation middleware, persisted user locale, session/cookie locale storage, route locale parameters beyond the returned example, or exact config file contents beyond `locale` and fallback environment variables, rely on the fresh Context7 lookup.
6. For translation topics not in the references, such as validation attribute localization, custom validation values, nested keys beyond dot syntax, missing translation behavior beyond returned examples, Blade escaping details beyond `{{ __('...') }}`, or custom translator implementations, rely on the fresh Context7 lookup.
7. For pluralization topics not in the references, such as pluralization language internals, custom pluralization rules, exact Eloquent table-name side effects, or supported languages beyond the returned list, rely on the fresh Context7 lookup.
8. For package localization topics not in the references, such as publish groups/tags, service provider registration, vendor package discovery, JSON package override rules, or package translation testing, rely on the fresh Context7 lookup.
9. For reviews, flag only documented mismatches: unconfirmed locale key, unconfirmed language path, unsupported translation helper, wrong JSON/PHP language file structure, missing `lang:publish` where customization needs default files, unconfirmed placeholder behavior, unsupported pluralizer language, wrong package override path, or package behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The default language for a Laravel application is defined in `config/app.php` using the `locale` option and is typically controlled by `APP_LOCALE`.
- The fallback language may be defined via `APP_FALLBACK_LOCALE` so content can be displayed when a translation is missing in the primary language.
- `php artisan lang:publish` scaffolds the `lang` directory and publishes default language files.
- `lang_path()` returns the fully qualified path to the application's `lang` directory, and `lang_path('en/messages.php')` returns a path to a file within it.
- The docs show setting the locale for a single HTTP request with `App::setLocale($locale)` after validating the route locale.
- The docs show retrieving and checking the locale with `App::currentLocale()` and `App::isLocale('en')`.
- Translation strings may be stored as PHP files under language subdirectories, such as `lang/en/messages.php` and `lang/es/messages.php`.
- For language directories that differ by territory, the docs say to use ISO 15897 naming conventions, such as `en_GB`.
- PHP language files return keyed arrays, such as `'welcome' => 'Welcome to our application!'` in `lang/en/messages.php`.
- JSON translation files may use the default translation string as the key, such as `lang/es.json` containing `"I love programming.": "Me encanta programar."`.
- The docs warn that when using translation strings as keys, a key matching a translation filename may cause the translator to return the whole file content.
- The `__()` helper retrieves translation strings using short-key dot syntax or JSON translation keys.
- Blade may render translations with `{{ __('messages.welcome') }}` in the returned docs.
- Translation placeholders use a colon prefix, such as `:name`, and replacements are passed as the second argument to `__()`.
- The docs state replacement capitalization is automatic when placeholders are all caps or first-letter capitalized.
- Object placeholders use the object's `__toString()` method by default, and custom formatting can be registered with `Lang::stringable(...)` in a service provider `boot()` method.
- `trans_choice(...)` retrieves pluralized translation strings based on a count.
- Pluralized translation strings may use pipe-delimited forms, exact count forms such as `{0}`, range forms such as `[1,19]`, and placeholders such as `:value` or `:count`.
- The docs show JSON pluralized translation strings using a pipe-delimited JSON key and value.
- Laravel's pluralizer uses English by default and can be configured with `Pluralizer::useLanguage(...)`.
- Supported pluralizer languages returned by the docs are French, Norwegian Bokmal, Portuguese, Spanish, and Turkish.
- The docs state that if the pluralizer language is changed, Eloquent model table names should be explicitly defined to avoid unexpected behavior.
- Resource route create/edit URI verbs may be localized with `Route::resourceVerbs([...])` in `AppServiceProvider` `boot()`.
- Package translations can be loaded with `loadTranslationsFrom(...)` and referenced using `package::file.line` syntax.
- Package JSON translations can be loaded with `loadJsonTranslationsFrom(...)`.
- Package language files may be published to `$this->app->langPath('vendor/courier')` with `publishes(...)` in a service provider `boot()` method.
- Package translation overrides can be placed in `lang/vendor/{package}/{locale}`, such as `lang/vendor/hearthfire/en/messages.php`, and only overridden strings need to be defined.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 localization topic.
- Every command, path, helper, facade, method, config key, environment variable, locale example, placeholder behavior, pluralization syntax, package translation API, and route localization API is traceable to the lookup or references.
- Browser language detection, middleware patterns, package behavior, translator internals, and locale standards are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed localization features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
