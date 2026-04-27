---
name: laravel-13-database-migrations-query-builder
description: 'Use when: working with Laravel 13 database migrations, database/migrations, Schema facade, Blueprint, Migration classes, up(), down(), Schema::create(), Schema::drop(), column methods, migrate commands, make:migration, query builder, DB::table(), get(), where(), grouped where clauses, raw expressions, insert(), update(), delete(), aggregates, limit(), offset(), DB::select(), transactions, DB::beginTransaction(), DB::commit(), DB::rollBack(), and Laravel 13 database code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 migration, schema, query builder, DB facade, transaction, or database review task'
---

# Laravel 13 Database, Migrations, And Query Builder

## Purpose
Use this skill to create, review, or explain Laravel 13 database migrations, schema builder code, raw database access, transactions, and query builder usage using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact database, migration, schema, or query builder topic.
2. Do not add migration commands, migration file paths, schema methods, column methods, indexes, foreign keys, query builder methods, raw SQL APIs, transaction methods, database config keys, or CLI commands unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or class name in a malformed way, run a narrower lookup before using that import or class name in code.
4. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Migration purpose, generation location, migration commands, `Schema::create()`, `Schema::drop()`, `Migration`, `Blueprint`, and documented column methods: [migrations-schema.md](./references/migrations-schema.md)
- Query builder retrieval, filtering, grouped clauses, subqueries, raw expressions, inserts, updates, deletes, aggregates, limits, and offsets: [query-builder.md](./references/query-builder.md)
- Raw `DB` access, `DB::select()`, PDO binding note, and manual transactions: [database-access-transactions.md](./references/database-access-transactions.md)

## Workflow
1. Identify the exact surface: migration generation, migration execution, schema creation, table modification, column method, query retrieval, filtering, subquery, raw expression, insert, update, delete, aggregate, limit/offset, raw SQL, transaction, or database review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, imports, facades, class names, methods, SQL snippets, column methods, and query builder chains.
5. For migration topics not in the references, such as index creation, foreign key constraints, column modifiers, dropping columns, modifying columns, squashing migrations, or custom migration paths, rely on the fresh Context7 lookup.
6. For query builder topics not in the references, such as joins, unions, ordering beyond raw ordering, chunking, lazy collections, locking, JSON where clauses, update-or-insert, upserts, increments, or pagination, rely on the fresh Context7 lookup.
7. For database topics not in the references, such as database configuration, multiple connections, query listeners, database CLI inspection commands, query monitoring, or transaction retry closures, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unsupported command, unconfirmed schema method, unconfirmed column method, wrong facade import, unsafe raw SQL not using bindings where docs show bindings, unconfirmed query builder method, or transaction API not confirmed by the current lookup.

## Confirmed Core Patterns
- Migrations are described as version control for the database and are stored in `database/migrations`.
- The docs confirm `php artisan migrate`, `php artisan migrate:status`, `php artisan migrate --step`, `php artisan migrate --pretend`, `php artisan migrate --isolated`, and `php artisan migrate --force`.
- The docs confirm `php artisan make:model Flight --migration` for creating a model with a corresponding migration.
- A migration may return an anonymous class extending `Migration` and define `up(): void` and `down(): void` methods.
- The docs show `Schema::create('flights', function (Blueprint $table) { ... })` and `Schema::drop('flights')`.
- Documented migration imports include `Illuminate\Database\Migrations\Migration`, `Illuminate\Database\Schema\Blueprint`, and `Illuminate\Support\Facades\Schema`.
- Documented column examples include `id()`, `string(...)`, `timestamps()`, `date(...)`, `decimal(...)`, `enum(...)`, `foreignIdFor(...)`, `json(...)`, `text(...)`, `boolean(...)`, and many listed numeric/date/binary/JSON/UUID/relationship/specialty methods.
- The query builder uses the `DB` facade `table()` method to begin a query and `get()` to retrieve results.
- The docs state Laravel's query builder uses PDO parameter binding to protect against SQL injection attacks for query bindings.
- Documented query examples include `where(...)`, grouped `where(function (Builder $query) { ... })`, `orWhere(...)`, subquery `where(...)`, `whereColumn(...)`, `selectRaw(...)`, `whereRaw(...)`, `havingRaw(...)`, `orderByRaw(...)`, `groupByRaw(...)`, `insert(...)`, `insertOrIgnore(...)`, `insertUsing(...)`, `insertGetId(...)`, `update(...)`, `delete(...)`, `count()`, `max(...)`, `avg(...)`, `offset(...)`, and `limit(...)`.
- The docs show raw SQL selection with `DB::select('select * from users where active = ?', [1])` returning an array of `stdClass` objects.
- The docs confirm manual transactions with `DB::beginTransaction()`, `DB::commit()`, and `DB::rollBack()`.

## Completion Check
- A fresh Context7 lookup was performed for the exact database, migration, schema, or query builder topic.
- Every command, class, facade, method, column method, SQL expression, binding, and generated path is traceable to the lookup or references.
- Raw SQL examples preserve documented binding patterns when bindings are shown.
- Unconfirmed database features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
