# Maintenance Mode

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x maintenance mode.

## Maintenance Mode Behavior
The configuration docs state that when an application is in maintenance mode, a custom view is displayed for all requests into the application.

The docs state a maintenance mode check is included in the default middleware stack.

The docs state that if the application is in maintenance mode, a `Symfony\Component\HttpKernel\Exception\HttpException` instance is thrown with status code `503`.

## Redirecting Requests
The docs show enabling maintenance mode while redirecting incoming requests:

```shell
php artisan down --redirect=/
```

The docs state the `redirect` option can route users to a landing page or different domain while updates are happening.

## Disabling Maintenance Mode
The docs show disabling maintenance mode:

```shell
php artisan up
```

The docs state this returns normal application traffic.

## Bypassing Maintenance Mode
The docs state the `secret` option can specify a maintenance mode bypass token.

After placing the application in maintenance mode, navigating to the application URL matching this token issues a maintenance mode bypass cookie. The docs state that after the cookie is issued, the browser is redirected to `/` and can browse the application normally.

Run a fresh lookup before writing a concrete `php artisan down --secret=...` command example.

## Pre-Rendering The Maintenance View
The docs state users may encounter errors during deployment if dependencies are updating, because the framework must boot to determine maintenance status.

The docs state Laravel can pre-render a maintenance mode view that is returned at the beginning of the request cycle before application dependencies have loaded.

The docs state the `down` command's `render` option can pre-render a chosen template.

Run a fresh lookup before writing a concrete `php artisan down --render=...` command example.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using exact `--secret`, `--render`, `--retry`, `--refresh`, or `--status` command snippets, custom maintenance views, maintenance bypass cookie expiration, redirect behavior beyond the docs summary, or deployment workflows that combine maintenance mode with dependency updates.
