# Console Commands

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Artisan console commands.

## Generating Commands
The docs show generating a command class with Artisan:

```shell
php artisan make:command SendEmails
```

The structure docs also show:

```bash
php artisan make:command YourCommandName
```

The docs state the command creates the necessary file within `app/Console/Commands`. They also state the directory is created the first time `make:command` is run if it does not exist.

## Class-Based Commands
The docs show a class-based command using PHP attributes:

```php
<?php

namespace App\Console\Commands;

use App\Models\User;
use App\Support\DripEmailer;
use Illuminate\Console\Attributes\Description;
use Illuminate\Console\Attributes\Signature;
use Illuminate\Console\Command;

#[Signature('mail:send {user}')]
#[Description('Send a marketing email to a user')]
class SendEmails extends Command
{
    /**
     * Execute the console command.
     */
    public function handle(DripEmailer $drip): void
    {
        $drip->send(User::find($this->argument('user')));
    }
}
```

Confirmed imports and classes from this snippet:

- `App\Console\Commands`
- `Illuminate\Console\Attributes\Description`
- `Illuminate\Console\Attributes\Signature`
- `Illuminate\Console\Command`
- `handle(...)`

## Signature Property Pattern
The docs also show defining the command name and signature with a protected property:

```php
/**
 * The name and signature of the console command.
 *
 * @var string
 */
protected $signature = 'mail:send {user}';
```

The docs show argument and option descriptions separated by a colon:

```php
protected $signature = 'mail:send
                        {user : The ID of the user}
                        {--queue : Whether the job should be queued}';
```

## Retrieving Arguments And Options
The docs show retrieving individual and all input values:

```php
public function handle(): void
{
    $userId = $this->argument('user');
}

$arguments = $this->arguments();

$queueName = $this->option('queue');
$options = $this->options();
```

Confirmed helpers: `argument()`, `arguments()`, `option()`, and `options()`.

## Writing Output
The docs show console output helpers:

```php
$this->info('The command was successful!');
$this->error('Something went wrong!');
$this->line('Display this on the screen');
$this->newLine(3);

$this->table(
    ['Name', 'Email'],
    User::all(['name', 'email'])->toArray()
);
```

Confirmed helpers: `info()`, `error()`, `line()`, `newLine()`, and `table()`.

## Prompting For Input
The docs show prompt helpers:

```php
$name = $this->ask('What is your name?');
$name = $this->ask('What is your name?', 'Taylor');
$password = $this->secret('What is the password?');
if ($this->confirm('Do you wish to continue?')) {
    // ...
}
if ($this->confirm('Do you wish to continue?', true)) {
    // ...
}
```

Confirmed helpers: `ask()`, `secret()`, and `confirm()`.

## Closure-Based Commands
The docs show closure-based commands in `routes/console.php` with the `Artisan::command` method:

```php
Artisan::command('mail:send {user}', function (string $user) {
    $this->info("Sending email to: {$user}!");
});
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `PromptsForMissingInput`, `promptForMissingArgumentsUsing()`, `choice()`, progress bars, command isolation, signal handling, command registration details, stub publishing, auto-completion, console events, or command testing helpers.
