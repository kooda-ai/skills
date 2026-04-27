---
name: laravel-13-factories-seeders
description: 'Use when: working with Laravel 13 model factories, database seeding, database/factories, database/seeders, make:model --factory, make:seeder, DatabaseSeeder, db:seed, migrate:fresh --seed, HasFactory, factory states, trashed(), afterMaking(), afterCreating(), has(), for(), hasAttached(), recycle(), and Laravel 13 factory/seeder code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 factory, seeder, DatabaseSeeder, state, relationship seeding, or review task'
---

# Laravel 13 Factories and Seeders

## Purpose
Use this skill to create, review, or explain Laravel 13 model factories and database seeders using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact factory or seeding topic.
2. Do not add factory commands, factory paths, traits, attributes, state methods, relationship methods, callback hooks, seeder commands, seeder traits, or execution helpers unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, class names, trait names, command names, directories, and example values.
5. Do not infer behavior from older Laravel versions, Faker docs, Pest helpers outside the returned snippets, package docs, source code, blog posts, or general Laravel memory.
6. Keep generic model generation, casts, and pagination in `laravel-13-eloquent-database`; use this slice when the task is specifically about factory definitions, test/dev data generation, and seeding workflows.

## Reference Map
- Factory generation boundaries, base structure, `HasFactory`, `UseFactory`, `UseModel`, and built-in `trashed()` state: [factory-structure-basics.md](./references/factory-structure-basics.md)
- Factory callbacks, relationship builders, magic relationship helpers, pivot attributes, and `recycle(...)`: [factory-states-relationships.md](./references/factory-states-relationships.md)
- Seeder generation, `DatabaseSeeder`, `db:seed`, `migrate:fresh --seed`, `call(...)`, `WithoutModelEvents`, mass-assignment behavior, and seeding with factories: [seeding-execution.md](./references/seeding-execution.md)

## Workflow
1. Identify the exact surface: factory generation, model-factory linkage, factory definition, state method, built-in soft-delete state, after-make or after-create hook, parent/child relationship seeding, many-to-many seeding, reusing existing related models, seeder generation, database seeder orchestration, muting model events, or seed execution.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, traits, methods, directories, attributes, relationship helpers, and execution patterns.
5. For factory topics not confirmed in the references, such as the exact `make:factory` shell syntax with arguments, `Sequence` code blocks, custom namespace generation, full `definition(): array` example code, or advanced factory attributes beyond returned snippets, rely on the fresh Context7 lookup.
6. For seeding topics not confirmed in the references, such as `callSilently(...)`, seeder dependency injection patterns beyond `run()`, production seeding safeguards, or custom seed command combinations beyond the returned snippets, rely on the fresh Context7 lookup.
7. For reviews, flag only documented mismatches: unsupported factory trait or attribute, unconfirmed state or relationship helper, missing documented event muting trait where intended, wrong seeder path, unsupported execution command, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel 13 factories are dedicated classes for defining default model attributes and generating test or seeding data according to the Eloquent factories docs.
- The docs state factory classes extend Laravel's base factory class and define a `definition` method, and that the `fake` helper provides Faker access.
- The docs confirm generating a model with an associated factory using `php artisan make:model Flight --factory` or `php artisan make:model Flight -f`.
- The docs state the `make:factory` Artisan command creates factory classes in `database/factories`, even though the current docs result did not return a full concrete shell example.
- The docs confirm the `HasFactory` trait and also document explicit factory linkage with `#[UseFactory(...)]`, `#[UseModel(...)]`, and overriding `newFactory()` when conventions do not apply.
- The docs confirm the built-in `trashed()` state for models that support soft deletes.
- The docs confirm custom state methods built with `state(...)` and callback registration through `configure()`, `afterMaking(...)`, and `afterCreating(...)`.
- The docs confirm factory relationship helpers including `has(...)`, `for(...)`, `hasAttached(...)`, magic methods such as `hasPosts(...)` and `hasRoles(...)`, and `recycle(...)` for reusing existing related models.
- The docs confirm `php artisan make:seeder UserSeeder` and state seeders live in `database/seeders`.
- The docs confirm `php artisan db:seed`, `php artisan db:seed --class=UserSeeder`, `php artisan migrate:fresh --seed`, and `php artisan migrate:fresh --seed --seeder=UserSeeder`.
- The docs confirm `DatabaseSeeder` can orchestrate other seeders through `$this->call([...])`.
- The docs state mass assignment protection is automatically disabled during database seeding.
- The docs confirm `WithoutModelEvents` to mute model events during seeding, including nested seeders called through `call(...)`.
- The docs confirm seeding with factories such as `User::factory()->count(50)->hasPosts(1)->create()`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 factory or seeding topic.
- Every command, trait, attribute, method, directory, relationship helper, seeder helper, and behavior statement is traceable to the lookup or references.
- Generic Eloquent model concerns are not duplicated when the existing database slice already owns them.
- Unconfirmed factory or seeding features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
