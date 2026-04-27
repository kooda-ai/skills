---
name: laravel-13-eloquent-advanced
description: 'Use when: working with Laravel 13 advanced Eloquent, local scopes, Scope attribute, dynamic scopes, pending attributes, withAttributes(), chained scopes, higher order orWhere scopes, custom Eloquent collections, CollectedBy attribute, newCollection(), accessors, mutators, Attribute objects, casts(), encrypted casts, custom casts, make:cast, CastsAttributes, value object casts, model observers, make:observer, ObservedBy attribute, model lifecycle events, Prunable, pruning queries, and Laravel 13 advanced Eloquent code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 advanced Eloquent scopes, collections, casts, observers, pruning, or review task'
---

# Laravel 13 Advanced Eloquent

## Purpose
Use this skill to create, review, or explain Laravel 13 advanced Eloquent behavior such as scopes, custom collections, mutators/casts, observers, model events, and pruning using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact advanced Eloquent topic.
2. Do not add scope APIs, model attributes, builder types, collection customization APIs, accessor/mutator behavior, cast types, cast interfaces, observer commands, observer registration, model event names, pruning traits, pruning commands, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented attribute names, method names, command names, class names, namespaces, traits, and return types.
5. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Local scopes with `#[Scope]`, dynamic scopes, pending attributes with `withAttributes()`, chained scopes, higher-order `orWhere`, and custom Eloquent collections: [scopes-collections.md](./references/scopes-collections.md)
- Custom casts, `make:cast`, `CastsAttributes`, value-object casts, encrypted casts, and accessor/mutator boundary: [mutators-casts.md](./references/mutators-casts.md)
- Observers, `make:observer`, `ObservedBy`, model lifecycle event boundary, `Prunable`, and pruning query definition: [observers-pruning.md](./references/observers-pruning.md)

## Workflow
1. Identify the exact surface: local scope, dynamic scope, pending attribute scope, chained scopes, custom collection, accessor, mutator, built-in cast, encrypted cast, custom cast, value object cast, observer generation, observer registration, model lifecycle event, pruning query, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, imports, attributes, classes, traits, interfaces, method signatures, builder types, and examples.
5. For scope topics not in the references, such as global scopes, anonymous global scopes, removing scopes, pending attribute behavior beyond returned examples, or additional scope attributes, rely on the fresh Context7 lookup.
6. For mutator/cast topics not in the references, such as concrete setter mutators, inbound-only casts, cast parameters, enum casts, array/object/collection cast examples, encrypted cast variants beyond the summary, or exact accessor attributes outside shown examples, rely on the fresh Context7 lookup.
7. For observer/event/pruning topics not in the references, such as exact model event names, observer method names, muting events, queued anonymous event listeners, `MassPrunable`, `model:prune`, pruning schedules, soft-deleting pruning behavior, or testing model events, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed attribute, wrong builder type, unsupported scope return behavior, unconfirmed cast interface, wrong cast return shape, unconfirmed observer registration, unsupported pruning trait, unconfirmed lifecycle event, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Local scopes can be defined with the `Illuminate\Database\Eloquent\Attributes\Scope` attribute on Eloquent model methods.
- Scope methods in the returned examples receive `Illuminate\Database\Eloquent\Builder` and return `void` while mutating the query.
- The docs state scopes should return the query builder instance or `void`.
- Dynamic scopes can accept parameters after the `$query` parameter, as shown by `ofType(Builder $query, string $type)` and `User::ofType('admin')->get()`.
- Pending attribute scopes can use `withAttributes(...)` to apply attributes to both the query `WHERE` clause and models created by the scope.
- `withAttributes(..., asConditions: false)` is documented for applying attributes only to created models.
- Local scopes can be chained, as in `User::popular()->active()->orderBy('created_at')->get()`.
- The docs show logical grouping for `orWhere` with scopes and also the higher-order `orWhere->active()` form.
- Custom Eloquent collections can be configured with the `Illuminate\Database\Eloquent\Attributes\CollectedBy` attribute.
- Custom collections can also be configured by overriding `newCollection(array $models = []): Collection`.
- The `newCollection()` example uses `Model::isAutomaticallyEagerLoadingRelationships()` and `withRelationshipAutoloading()`.
- `php artisan make:cast AsJson` is documented for generating a custom cast class.
- Custom casts can implement `Illuminate\Contracts\Database\Eloquent\CastsAttributes` with `get(...)` and `set(...)` methods.
- A model can register a custom cast in `protected function casts(): array` using `AsJson::class`.
- The docs show a value-object cast returning an `Address` object from `get(...)` and returning an attribute array from `set(...)`.
- The docs state accessors, mutators, and attribute casting transform Eloquent attribute values during retrieval or assignment.
- The docs state encrypted casts automatically encrypt model attribute values using Laravel's built-in encryption features.
- The docs state encrypted cast variants exist for arrays, collections, and objects, and that encrypted text length is unpredictable and should use `TEXT` or larger columns.
- The docs state encrypted attributes cannot be queried or searched at the database level.
- `php artisan make:observer UserObserver --model=User` creates an observer class for a specific model in `app/Observers`.
- Observers can be registered by applying `Illuminate\Database\Eloquent\Attributes\ObservedBy` to the model class.
- Eloquent models dispatch events for moments in the model lifecycle, including retrieval, creation, updating, saving, deletion, and restoration according to the docs.
- The docs state events ending with `-ing` are dispatched before persistence and events ending with `-ed` are dispatched after persistence.
- Models can use `Illuminate\Database\Eloquent\Prunable` and define `prunable(): Builder` to return a pruning query.
- The docs show `static::where('created_at', '<=', now()->minus(months: 1))` as a pruning query example.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 advanced Eloquent topic.
- Every command, attribute, class, trait, interface, method, builder type, return type, cast behavior, observer behavior, event statement, and pruning behavior is traceable to the lookup or references.
- Eloquent lifecycle, global scopes, mutator/cast, collection, and pruning details are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed advanced Eloquent features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
