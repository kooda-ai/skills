---
name: laravel-13-eloquent-database
description: 'Use when: working with Laravel 13 Eloquent, models, app\Models, Illuminate\Database\Eloquent\Model, make:model, generated related classes, --migration, --all, -a, custom casts, make:cast, CastsAttributes, casts(), pagination, User::paginate(), and Laravel 13 database/Eloquent code reviews. Use laravel-13-factories-seeders for dedicated factory and seeding work. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 Eloquent/database task, model/cast/pagination code, or review'
---

# Laravel 13 Eloquent And Database

## Purpose
Use this skill to create, review, or explain Laravel 13 Eloquent and database code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Eloquent or database topic.
2. Do not add migration APIs, schema builder methods, model properties, relationship methods, query builder methods, mass assignment rules, casts, pagination methods, or generated-artifact behavior unless they appear in the current Context7 result or [eloquent-database.md](./references/eloquent-database.md).
3. If a Context7 result renders a namespace or import in a malformed way, run a narrower lookup before using that import in code.
4. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Model generation, model location, migrations option, all-in-one model generation, generated related classes, custom casts, and pagination: [eloquent-database.md](./references/eloquent-database.md)

## Workflow
1. Identify the exact surface: model generation, generated related classes, migration option, custom cast, model `casts()`, pagination, or Eloquent/database code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load [eloquent-database.md](./references/eloquent-database.md).
4. Use only documented commands, paths, interfaces, method names, model examples, and helper calls.
5. Route dedicated factory-definition, factory-state, relationship-seeding, `DatabaseSeeder`, and seed-command work to `laravel-13-factories-seeders`.
6. For features not in the reference, such as migrations, schema columns, relationships, mass assignment, queries, scopes, collections, serialization, pagination views, database transactions, or advanced generated-artifact behavior, rely on the fresh Context7 lookup before adding code.
7. For reviews, flag only documented mismatches: unsupported command option, unconfirmed model path, unconfirmed interface, unconfirmed model method, unsupported generated-artifact claim, or unconfirmed pagination/query API.

## Confirmed Core Patterns
- Eloquent models are typically stored in `app\Models` and extend `Illuminate\Database\Eloquent\Model`.
- `php artisan make:model Flight --migration` creates a model with its corresponding database migration.
- `php artisan make:model Flight --all` and `php artisan make:model Flight -a` generate a model, migration, factory, seeder, policy, controller, and form requests.
- `php artisan make:model` generation may include related artifacts such as a factory or seeder depending on the selected options.
- Use `laravel-13-factories-seeders` when the task is about implementing or reviewing those generated factory or seeder files.
- `php artisan make:cast AsJson` generates a custom cast class.
- Custom casts can implement `Illuminate\Contracts\Database\Eloquent\CastsAttributes` with `get(...)` and `set(...)` methods.
- A model can return a cast mapping from `protected function casts(): array`.
- The docs show `User::paginate(15)` for paginating Eloquent model results.

## Completion Check
- A fresh Context7 lookup was performed for the exact Eloquent/database topic.
- Every command, flag, generated artifact, interface, method, model path, cast mapping, and pagination method is traceable to the lookup or reference.
- Factory-definition and seeding details are delegated to `laravel-13-factories-seeders` unless the current lookup is specifically about generated artifacts from `make:model`.
- Unconfirmed database and Eloquent features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
