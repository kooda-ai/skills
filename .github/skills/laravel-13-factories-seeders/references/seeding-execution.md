# Seeding and Execution

## Seeder Generation and Location
The seeding docs show generating a seeder with Artisan:

```shell
php artisan make:seeder UserSeeder
```

- The docs state generated seeders are placed in `database/seeders`.
- The docs state a seeder class contains a `run` method that is executed when seeding runs.

## DatabaseSeeder and Manual Inserts
The seeding docs show the default `DatabaseSeeder` shape:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeders.
     */
    public function run(): void
    {
        DB::table('users')->insert([
            'name' => Str::random(10),
            'email' => Str::random(10).'@example.com',
            'password' => Hash::make('password'),
        ]);
    }
}
```

## Calling Additional Seeders
The seeding docs show orchestrating additional seeders from `DatabaseSeeder`:

```php
/**
 * Run the database seeders.
 */
public function run(): void
{
    $this->call([
        UserSeeder::class,
        PostSeeder::class,
        CommentSeeder::class,
    ]);
}
```

## Seeding With Factories
The docs show seeding related models with factories:

```php
use App\Models\User;

/**
 * Run the database seeders.
 */
public function run(): void
{
    User::factory()
        ->count(50)
        ->hasPosts(1)
        ->create();
}
```

## Running Seeders
The seeding docs show these execution commands:

```shell
php artisan db:seed

php artisan db:seed --class=UserSeeder
```

```shell
php artisan migrate:fresh --seed

php artisan migrate:fresh --seed --seeder=UserSeeder
```

## Muting Model Events
The seeding docs show muting model events with `WithoutModelEvents`:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;

class DatabaseSeeder extends Seeder
{
    use WithoutModelEvents;

    /**
     * Run the database seeders.
     */
    public function run(): void
    {
        $this->call([
            UserSeeder::class,
        ]);
    }
}
```

## Confirmed Behavior
- The docs state mass assignment protection is automatically disabled during database seeding.
- The docs state `WithoutModelEvents` suppresses model events even for nested seeders executed through `call(...)`.
- The docs state dependencies may be type-hinted in a seeder `run()` method and are resolved through the service container.

## Boundaries
- Run a fresh lookup before using `callSilently(...)`, seeder discovery behavior, production confirmation prompts, seed ordering guarantees beyond `call(...)`, or custom seeding workflows not shown in the returned docs.
