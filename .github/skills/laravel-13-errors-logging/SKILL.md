---
name: laravel-13-errors-logging
description: 'Use when: working with Laravel 13 errors, exception handling, bootstrap/app.php withExceptions(), Illuminate\Foundation\Configuration\Exceptions, exception reporting, report callbacks, report() helper, exception render methods, render callbacks, custom HTTP error pages, abort(404), resources/views/errors, 4xx.blade.php, 5xx.blade.php, logging, Log facade, Log::emergency(), alert(), critical(), error(), warning(), notice(), info(), debug(), Log::channel(), config/logging.php, stack channel, log channel drivers, and Laravel 13 error/logging code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 exception handling, error pages, logging, Log facade, or review task'
---

# Laravel 13 Errors And Logging

## Purpose
Use this skill to create, review, or explain Laravel 13 exception handling, HTTP error responses, custom error pages, and logging code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact errors, exception handling, HTTP error page, or logging topic.
2. Do not add exception configuration APIs, callbacks, imports, exception classes, rendering behavior, reporting behavior, log channels, channel drivers, log levels, config keys, file paths, Artisan commands, helpers, facades, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, helper names, facade names, file paths, status codes, and view names.
5. Do not infer behavior from older Laravel versions, Symfony docs, Monolog docs, PSR docs, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- `withExceptions()`, exception reporting callbacks, exception class `report()` and `render()` methods, log levels, and ignored-exception boundaries: [exception-handling.md](./references/exception-handling.md)
- `Log` facade levels, `Log::channel()`, `config/logging.php`, default `stack` channel, log levels, and available channel drivers: [logging.md](./references/logging.md)
- `abort(404)`, custom HTTP error pages, fallback `4xx` / `5xx` pages, `$exception` variable, and publish boundary: [http-error-pages.md](./references/http-error-pages.md)

## Workflow
1. Identify the exact surface: exception reporting, exception rendering, custom exception class methods, log levels for exceptions, ignored framework exceptions, manual reporting, HTTP abort responses, custom error pages, fallback error pages, log message writing, specific log channels, logging configuration, channel drivers, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented APIs, helpers, facades, paths, callbacks, method names, view names, status codes, commands, and channel driver names.
5. For exception topics not in the references, such as exact imports for malformed Context7 snippets, `dontReport()`, `ShouldntReport`, `dontReportDuplicates()`, throttling, exception context, `shouldRenderJsonWhen()`, custom JSON rendering, validation exception behavior, or render callbacks configured in `bootstrap/app.php`, rely on a fresh Context7 lookup.
6. For logging topics not in the references, such as context arrays, stack creation APIs, on-demand channels, custom Monolog handlers, deprecations channels, emergency logger behavior, log retention, cloud logging, or concrete channel config arrays, rely on a fresh Context7 lookup.
7. For error page topics not in the references, such as the exact `vendor:publish` arguments, internal dedicated page behavior beyond `404`, `500`, and `503`, custom 503 maintenance pages, or exception variables beyond `$exception`, rely on a fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed exception configuration API, unsupported helper, wrong documented error view path, unconfirmed log level, unsupported channel driver, unconfirmed logging config path, malformed imports from generated snippets, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- New Laravel projects have error and exception handling already configured according to the docs.
- Exception handling can be managed with `withExceptions()` in `bootstrap/app.php`.
- The `$exceptions` object provided to the `withExceptions` closure is an instance of `Illuminate\Foundation\Configuration\Exceptions` according to the docs.
- The docs show `$exceptions->report(function (InvalidOrderException $e) { ... });` for custom reporting logic.
- The docs show `->stop()` on a report callback and returning `false` from a report callback to stop default logging propagation.
- Exception classes can define `report()` and `render(...)` methods.
- The docs show a custom exception `render(Request $request): Response` returning `response(/* ... */)`.
- The docs show `render(Request $request): Response|bool` returning `false` to fall back to default behavior.
- The docs show `report(): bool` returning `true` or `false` depending on custom reporting behavior.
- The docs show mapping exception classes to custom PSR-3 log levels with `$exceptions->level(...)`.
- The docs show `$exceptions->stopIgnoring(HttpException::class)` to re-enable reporting for exception types Laravel ignores by default, such as HTTP exceptions.
- The `report($e)` helper is documented for logging exceptions without interrupting the request lifecycle.
- `abort(404)` is documented for generating an HTTP 404 response from anywhere in the application.
- Custom HTTP error pages are stored in `resources/views/errors` and are named to match the HTTP status code, such as `404.blade.php`.
- The docs state the HTTP exception raised by `abort` is passed to the error view as `$exception`.
- The docs confirm fallback error pages named `4xx.blade.php` and `5xx.blade.php` in `resources/views/errors`.
- The docs state fallback pages do not override Laravel's internal dedicated pages for `404`, `500`, and `503`; define individual pages to customize those responses.
- `Illuminate\Support\Facades\Log` is documented for writing log messages.
- The docs confirm log methods `emergency()`, `alert()`, `critical()`, `error()`, `warning()`, `notice()`, `info()`, and `debug()`.
- Laravel uses Monolog to power logging services according to the docs.
- The docs state log levels are RFC 5424 levels in descending severity: `emergency`, `alert`, `critical`, `error`, `warning`, `notice`, `info`, and `debug`.
- Logging configuration lives in `config/logging.php`.
- Laravel uses the `stack` channel by default for logging messages according to the docs.
- The `stack` channel aggregates multiple log channels into a single channel.
- `Log::channel('slack')->info('Something happened!')` is documented for logging to a specific channel.
- The docs list available channel drivers: `custom`, `daily`, `errorlog`, `monolog`, `papertrail`, `single`, `slack`, `stack`, and `syslog`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 exception, HTTP error, error page, or logging topic.
- Every API, helper, method, facade, callback, class name, status code, view path, config file, log level, channel name, driver name, and command is traceable to the lookup or references.
- Symfony, Monolog, PSR, and package-specific behavior is not inferred when the Laravel 13 docs did not confirm it.
- Unconfirmed error handling or logging features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
