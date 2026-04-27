# Scheduling

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x task scheduling.

## Defining Scheduled Tasks
The docs state scheduled tasks are typically defined within `routes/console.php`. They also state tasks can be configured using the `withSchedule` method in `bootstrap/app.php` for better organization.

The docs show scheduled Artisan commands using the `Schedule` facade:

```php
use App\Console\Commands\SendEmailsCommand;
use Illuminate\Support\Facades\Schedule;

Schedule::command('emails:send Taylor --force')->daily();

Schedule::command(SendEmailsCommand::class, ['Taylor', '--force'])->daily();
```

Confirmed imports and methods: `Illuminate\Support\Facades\Schedule`, `Schedule::command(...)`, and `daily()`.

## Closure Scheduling And Frequencies
The docs show scheduling a closure:

```php
use Illuminate\Support\Facades\Schedule;

// Run once per week on Monday at 1 PM...
Schedule::call(function () {
    // ...
})->weekly()->mondays()->at('13:00');

// Run hourly from 8 AM to 5 PM on weekdays...
Schedule::command('foo')
    ->weekdays()
    ->hourly()
    ->timezone('America/Chicago')
    ->between('8:00', '17:00');
```

The docs also mention frequency methods including `cron('* * * * *')`, `everySecond()`, `everyMinute()`, `hourly()`, `daily()`, `weekly()`, `monthly()`, `quarterly()`, `yearly()`, `hourlyAt(17)`, `dailyAt('13:00')`, and `weeklyOn(1, '8:00')`.

## Listing And Running The Scheduler
The docs show viewing scheduled tasks and their next execution times:

```shell
php artisan schedule:list
```

The docs state the `schedule:run` command evaluates all scheduled tasks and determines if they need to run based on the server's current time.

The documented cron entry for production servers is:

```shell
* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```

For local development, the docs show starting the scheduler in the foreground:

```shell
php artisan schedule:work
```

## Preventing Overlaps
The docs show `withoutOverlapping()` to prevent a scheduled task from running if the previous instance is still active:

```php
use Illuminate\Support\Facades\Schedule;

// Prevent overlap
Schedule::command('emails:send')->withoutOverlapping();

// Prevent overlap with custom lock expiration (in minutes)
Schedule::command('emails:send')->withoutOverlapping(10);
```

The docs state this uses the application cache to manage locks, with an optional parameter for lock expiration time.

## Maintenance Mode
The docs show forcing a task to run even when the application is in maintenance mode:

```php
Schedule::command('emails:send')->evenInMaintenanceMode();
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Schedule::job()`, invokable object scheduling, sub-minute task details, `schedule:interrupt`, `onOneServer()`, `runInBackground()`, groups, hooks, URL pinging, environment constraints, additional timezone behavior, schedule mutex clearing, maintenance mode behavior beyond `evenInMaintenanceMode()`, or deployment guidance beyond the documented cron entry.
