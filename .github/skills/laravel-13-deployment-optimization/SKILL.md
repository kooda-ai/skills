---
name: laravel-13-deployment-optimization
description: 'Use when: working with Laravel 13 deployment, production configuration, APP_DEBUG=false, web server document root, Nginx public directory config, bootstrap/cache permissions, storage permissions, php artisan optimize, optimize:clear, config:cache, config:clear, view:cache, view:clear, event:cache, event:clear, route:clear, maintenance mode, php artisan down, down --redirect, down --secret, down --render, php artisan up, queue:restart, Supervisor queue workers, scheduler cron, schedule:run, schedule:work, Laravel 13 upgrade boundaries, and deployment code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 deployment, optimization, maintenance mode, queue/scheduler deployment, upgrade, or review task'
---

# Laravel 13 Deployment And Optimization

## Purpose
Use this skill to create, review, or explain Laravel 13 deployment, production configuration, optimization commands, maintenance mode, queue/scheduler deployment concerns, and narrow upgrade boundaries using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final commands, server configuration, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact deployment, optimization, maintenance mode, queue worker deployment, scheduler deployment, or upgrade topic.
2. Do not add server requirements, server packages, web server config, document roots, permissions, environment variables, cache commands, queue worker commands, Supervisor options, cron entries, maintenance mode options, upgrade steps, dependency versions, or deployment workflow steps unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, paths, options, config snippets, environment variables, and process-manager values.
5. Do not infer behavior from older Laravel versions, Forge docs, Vapor docs, Envoyer docs, Linux administration guides, Nginx docs, Supervisor docs, Composer docs, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Production debug mode, web-directory safety, Nginx public-root example, writable directories, and storage link boundary: [server-configuration.md](./references/server-configuration.md)
- Production optimization commands, cache clearing, config/view/event/route cache boundaries, and package optimize hooks: [optimization.md](./references/optimization.md)
- Maintenance mode behavior, `down` and `up`, redirects, bypass secrets, pre-rendering, and fresh-lookup boundaries for additional flags: [maintenance-mode.md](./references/maintenance-mode.md)
- Queue worker deployment, Supervisor example, `queue:restart`, scheduler cron, `schedule:run`, `schedule:work`, and narrow Laravel 13 upgrade notes: [workers-scheduler-upgrades.md](./references/workers-scheduler-upgrades.md)

## Workflow
1. Identify the exact surface: production debug setting, web server public root, Nginx config, writable directory, storage link, optimization command, cache clear command, maintenance mode, queue worker deployment, Supervisor worker config, scheduler cron, local scheduler, Laravel 13 upgrade, or deployment review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, paths, options, environment variables, server config snippets, process-manager examples, cron entries, and upgrade statements.
5. For deployment topics not in the references, such as PHP extensions, Composer install flags, Node build steps, database migrations in deployment, file ownership commands, Apache config, TLS, proxies, Octane, Horizon, Forge, Vapor, Envoyer, Laravel Cloud, zero-downtime deployment, or rollback strategy, rely on the fresh Context7 lookup.
6. For optimization topics not in the references, such as `route:cache`, `event:cache`, route cache limitations, config cache caveats, package-specific optimize hooks, or clearing commands beyond documented snippets, rely on the fresh Context7 lookup.
7. For maintenance mode topics not in the references, such as exact `--secret`, `--render`, `--retry`, `--refresh`, or `--status` command examples, bypass-cookie details beyond the docs summary, or custom views, rely on the fresh Context7 lookup.
8. For upgrade topics, keep claims narrow. Use only the fresh Context7 upgrade result or [workers-scheduler-upgrades.md](./references/workers-scheduler-upgrades.md), and do not invent version constraints or breaking changes.
9. For reviews, flag only documented mismatches: `APP_DEBUG=true` in production, missing documented writable directories, serving from an unsafe web-directory setup, unsupported cache command, unconfirmed maintenance option, unconfirmed process-manager setting, wrong scheduler cron, or upgrade detail not confirmed by the current lookup.

## Confirmed Core Patterns
- In production, `APP_DEBUG` should always be `false` according to the deployment and configuration docs.
- The docs warn that serving an application from a subdirectory within the configured web directory is not recommended because it could expose sensitive application files.
- The documented Nginx example uses `root /srv/example.com/public;`, `index index.php;`, `try_files $uri $uri/ /index.php?$query_string;`, and an `index.php` PHP-FPM location.
- The web server process must have write permissions for the `bootstrap/cache` and `storage` directories according to the deployment docs.
- `php artisan storage:link` is documented for creating the public disk symbolic link.
- `php artisan optimize` is documented to cache configuration, events, routes, and views for production.
- `php artisan optimize:clear` is documented to clear those optimized caches when necessary.
- `php artisan config:cache` and `php artisan config:clear` are documented configuration cache commands.
- `php artisan view:cache` and `php artisan view:clear` are documented view cache commands.
- The events docs state `optimize` or `event:cache` caches a manifest of application listeners, and `event:clear` removes the cache.
- `php artisan route:clear` is documented for clearing the route cache.
- Maintenance mode displays a custom view for all requests, and the default middleware stack includes a maintenance mode check.
- In maintenance mode, the docs state a `Symfony\Component\HttpKernel\Exception\HttpException` with status code `503` is thrown.
- `php artisan down --redirect=/` and `php artisan up` are documented maintenance mode commands.
- The docs confirm a `secret` option for maintenance mode bypass and a `render` option for pre-rendering a maintenance view.
- Queue workers are long-lived processes and will not notice code changes without being restarted according to the queue deployment docs.
- `php artisan queue:restart` is documented to gracefully restart queue workers after their current job finishes.
- The queue docs recommend a process manager like Supervisor to automatically restart queue workers.
- The documented Supervisor example includes `command=php /home/forge/app.com/artisan queue:work --sleep=3 --tries=3 --max-time=3600`, `numprocs=8`, `stopwaitsecs=3600`, and related process settings.
- The documented scheduler cron entry is `* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1`.
- `php artisan schedule:work` is documented for running the scheduler in the foreground during local development.
- The upgrade docs confirm `composer global update laravel/installer` for updating the global Laravel installer CLI tool.
- The upgrade docs state Laravel 13 upgrades require updating core dependencies in `composer.json`, including the framework, Laravel Boost, Tinker, and testing frameworks like PHPUnit and Pest to their respective major versions.
- The release notes state Laravel 13 prioritizes minimizing breaking changes.
- The upgrade docs mention Laravel Boost as a first-party MCP server that can facilitate automated upgrades from Laravel 12 to Laravel 13.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 deployment, optimization, maintenance, queue/scheduler deployment, or upgrade topic.
- Every command, option, path, environment variable, web server directive, process-manager setting, cron entry, cache behavior, maintenance behavior, and upgrade statement is traceable to the lookup or references.
- OS, server package, Composer install, NPM build, permissions command, process manager, queue driver, scheduler, and upgrade details are not inferred when the current lookup did not confirm them.
- Unconfirmed deployment or upgrade features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
