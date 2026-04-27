# Workers, Scheduler, And Upgrades

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x queue worker deployment, scheduler deployment, and narrow upgrade notes.

## Queue Workers During Deployment
The queue docs state queue workers are long-lived processes and will not notice code changes without being restarted.

The docs state the simplest deployment approach for applications using queue workers is to restart them during deployment using:

```shell
php artisan queue:restart
```

The docs state this command gracefully restarts workers after they finish their current job, ensuring no jobs are lost.

The docs recommend a process manager like Supervisor to automatically restart queue workers.

## Supervisor Worker Example
The queue docs show this Supervisor configuration example:

```ini
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/forge/app.com/artisan queue:work --sleep=3 --tries=3 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=forge
numprocs=8
redirect_stderr=true
stdout_logfile=/home/forge/app.com/worker.log
stopwaitsecs=3600
```

The docs state `stopwaitsecs` should be greater than the longest job's execution time.

Run a fresh lookup before changing the command, process counts, paths, user, or queue worker flags.

## Scheduler Cron
The scheduling docs show this cron entry to trigger Laravel's scheduler every minute on a production server:

```shell
* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```

The docs state `schedule:run` evaluates scheduled tasks and determines if they need to run based on the server's current time.

For local development, the docs show:

```shell
php artisan schedule:work
```

The docs state `schedule:work` starts the scheduler in the foreground for local development and eliminates the need for a system-level cron entry.

## Laravel 13 Upgrade Boundary
The upgrade docs show updating the global Laravel installer CLI tool:

```shell
composer global update laravel/installer
```

The upgrade docs state that upgrading to Laravel 13 requires updating core dependencies in `composer.json`, including the framework itself, Laravel Boost, Tinker, and testing frameworks like PHPUnit and Pest to their respective major versions.

The release notes state Laravel 13 prioritizes minimizing breaking changes to support a smooth upgrade process.

The upgrade docs state Laravel Boost is a first-party MCP server that can facilitate automated upgrades from Laravel 12 to Laravel 13 after being installed in a Laravel 12 application.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using concrete Laravel 13 dependency constraints, full upgrade steps, breaking changes, Laravel Boost installation commands, slash command names, Horizon deployment, Supervisor service-management commands, queue driver setup, cron editing instructions, schedule monitoring, or zero-downtime deployment workflows.
