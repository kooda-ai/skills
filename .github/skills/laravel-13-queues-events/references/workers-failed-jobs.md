# Workers And Failed Jobs

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x failed jobs, queue workers, and Supervisor worker configuration.

## Failed Job Listing And Retry
The docs state `queue:failed` lists all failed jobs, including their ID, connection, queue, and failure time.

The docs confirm these commands:

```shell
php artisan queue:failed
```

```shell
php artisan queue:retry ce7bb17c-cdd8-41f0-a8ec-7b4fef4e5ece
```

```shell
php artisan queue:retry ce7bb17c-cdd8-41f0-a8ec-7b4fef4e5ece 91401d2c-0784-4f43-824c-34f94a33c24d
```

```shell
php artisan queue:retry --queue=name
```

```shell
php artisan queue:retry all
```

The docs state `queue:retry` can re-run specific failed jobs, multiple jobs, all jobs for a queue, or all failed jobs.

## Queue Worker Backoff Option
The docs show setting the delay in seconds before retrying a failed job with `--backoff` on `queue:work`:

```shell
php artisan queue:work redis --tries=3 --backoff=3
```

Confirmed command elements: `queue:work`, `redis`, `--tries=3`, and `--backoff=3`.

## Supervisor Worker Configuration
The docs show an example Supervisor config for queue workers:

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

The docs say to adjust `command` and `numprocs` as needed and ensure `stopwaitsecs` is greater than the longest job execution time.

## Horizon Boundary
The current Context7 result included a Laravel Horizon timeout snippet with an `environments` array and a supervisor `timeout` value. Do not turn that into general Horizon guidance without a fresh Horizon-specific Context7 lookup.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `queue:listen`, worker daemon lifecycle, worker restart commands, priority queues, timeouts beyond shown snippets, memory limits, max jobs, max time beyond shown Supervisor command, sleep behavior beyond shown command, failed-job table setup, `queue:forget`, `queue:flush`, job pruning, queue monitoring, Supervisor installation, systemd, Horizon configuration, batches, or chains.
