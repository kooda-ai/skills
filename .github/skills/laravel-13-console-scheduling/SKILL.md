---
name: laravel-13-console-scheduling
description: 'Use when: working with Laravel 13 Artisan console commands, php artisan make:command, app/Console/Commands, command classes, Illuminate\Console\Command, Signature and Description attributes, protected $signature, handle(), command arguments, command options, argument(), arguments(), option(), options(), console output helpers, ask(), secret(), confirm(), Artisan::command(), routes/console.php, Artisan::call(), callSilently(), Artisan::queue(), onConnection(), onQueue(), task scheduling, Schedule facade, Schedule::command(), Schedule::call(), schedule:list, schedule:run, schedule:work, cron entries, withoutOverlapping(), evenInMaintenanceMode(), and Laravel 13 console/scheduler code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 Artisan command, programmatic command call, task scheduler, or review task'
---

# Laravel 13 Console And Scheduling

## Purpose
Use this skill to create, review, or explain Laravel 13 Artisan console commands, programmatic Artisan calls, queued Artisan commands, and scheduled tasks using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Artisan command, programmatic command, queued command, or scheduler topic.
2. Do not add command paths, namespaces, attributes, properties, input helpers, output helpers, scheduling methods, frequency methods, scheduler commands, cron entries, queue methods, facades, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, class names, method names, attribute names, arguments, options, cron entries, and imports.
5. Do not infer behavior from older Laravel versions, Symfony Console docs, queue driver docs, cron guides, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Command generation, class-based commands, closure commands, command input, prompts, and output helpers: [commands.md](./references/commands.md)
- `Artisan::call()`, command arguments/options, command-to-command calls, `callSilently()`, queued commands, `onConnection()`, and `onQueue()`: [programmatic-artisan.md](./references/programmatic-artisan.md)
- `Schedule` facade, scheduled commands, closure scheduling, frequency examples, scheduler commands, cron entry, overlap prevention, and maintenance mode boundary: [scheduling.md](./references/scheduling.md)

## Workflow
1. Identify the exact surface: command generation, command class structure, command signature, command input, console prompts, console output, closure command, programmatic command execution, queued command, scheduled task definition, scheduler frequency, scheduler runtime command, cron setup, overlap prevention, maintenance-mode scheduling, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented facades, commands, attributes, properties, methods, imports, paths, frequency methods, and examples.
5. For console topics not in the references, such as command isolation, signal handling, progress bars, choices, auto-completion, stub customization, command registration details, or testing commands, rely on the fresh Context7 lookup.
6. For scheduler topics not in the references, such as sub-minute task details, `schedule:interrupt`, `onOneServer()`, `runInBackground()`, environment constraints, timezones beyond the documented example, hooks, pinging URLs, groups, schedule cache commands, or cache lock clearing, rely on the fresh Context7 lookup.
7. For reviews, flag only documented mismatches: wrong command path, wrong namespace, unsupported attribute/property, unconfirmed input/output helper, unsupported scheduling method, wrong scheduler command, unconfirmed cron entry, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `php artisan make:command SendEmails` is documented for generating a new Artisan command.
- `php artisan make:command YourCommandName` creates the necessary file within the `app/Console/Commands` directory according to the docs.
- The docs state `make:command` creates a new command class in `app/Console/Commands`, and that directory is created the first time the command is run if it does not exist.
- Class-based commands can live in the `App\Console\Commands` namespace and extend `Illuminate\Console\Command`.
- The docs confirm `Illuminate\Console\Attributes\Signature` and `Illuminate\Console\Attributes\Description` attributes on a command class.
- The docs also confirm the older `protected $signature = 'mail:send {user}';` property pattern.
- The docs confirm `handle()` as the method that executes a console command and show dependency injection in `handle(DripEmailer $drip)`.
- The docs confirm `argument()`, `arguments()`, `option()`, and `options()` for retrieving command input.
- The docs confirm console output helpers `info()`, `error()`, `line()`, `newLine()`, and `table()`.
- The docs confirm prompt helpers `ask()`, `secret()`, and `confirm()`.
- Closure-based commands can be defined with `Artisan::command('mail:send {user}', function (string $user) { ... });` in `routes/console.php` according to the docs.
- `Illuminate\Support\Facades\Artisan` is documented for programmatic command execution.
- `Artisan::call(...)` accepts command parameters as arrays or strings in the documented examples and returns an exit code in the route example.
- Commands can call other commands with `$this->call(...)` and `$this->callSilently(...)`.
- `Artisan::queue(...)` is documented for dispatching Artisan commands to the queue system, including `onConnection('redis')` and `onQueue('commands')` in the returned chain.
- `Illuminate\Support\Facades\Schedule` is documented for task scheduling.
- Scheduled tasks are typically defined in `routes/console.php`, and the docs also mention `withSchedule` in `bootstrap/app.php` for better organization.
- The docs confirm `Schedule::command('emails:send Taylor --force')->daily()` and `Schedule::command(SendEmailsCommand::class, ['Taylor', '--force'])->daily()`.
- The docs confirm `Schedule::call(function () { ... })->weekly()->mondays()->at('13:00')`.
- The docs confirm frequency examples including `weekly()`, `mondays()`, `at('13:00')`, `weekdays()`, `hourly()`, `timezone('America/Chicago')`, `between('8:00', '17:00')`, `everySecond()`, `everyMinute()`, `daily()`, `monthly()`, `quarterly()`, `yearly()`, `cron('* * * * *')`, `hourlyAt(17)`, `dailyAt('13:00')`, and `weeklyOn(1, '8:00')`.
- `php artisan schedule:list`, `php artisan schedule:run`, and `php artisan schedule:work` are documented scheduler commands.
- The docs confirm the cron entry `* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1`.
- The docs confirm `withoutOverlapping()` and `withoutOverlapping(10)` for preventing scheduled task overlap.
- The docs confirm `evenInMaintenanceMode()` for running a scheduled task during maintenance mode.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 console or scheduling topic.
- Every command, facade, namespace, class, attribute, property, method, input helper, output helper, scheduler method, frequency method, cron entry, queue chain, path, and behavior is traceable to the lookup or references.
- Symfony Console, cron, queue driver, and OS-level scheduler behavior is not inferred when the Laravel 13 docs did not confirm it.
- Unconfirmed console or scheduler features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
