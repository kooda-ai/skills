---
name: laravel-13-eloquent-relationships
description: 'Use when: working with Laravel 13 Eloquent relationships, hasOne(), hasMany(), belongsTo(), belongsToMany(), dynamic relationship properties, relationship query builders, eager loading with with(), load(), loadMissing(), withWhereHas(), constrained eager loading, many-to-many attach(), detach(), sync(), pivot attributes, wherePivot(), custom pivot models, polymorphic morphTo(), morphMany(), loadMorph(), hasManyThrough(), one-of-many latestOfMany(), oldestOfMany(), ofMany(), and Laravel 13 relationship code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 Eloquent relationship definition, eager loading, pivot, polymorphic, through, one-of-many, or review task'
---

# Laravel 13 Eloquent Relationships

## Purpose
Use this skill to create, review, or explain Laravel 13 Eloquent relationship definitions, relationship queries, eager loading, many-to-many pivot operations, polymorphic relationships, through relationships, and one-of-many relationships using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Eloquent relationship topic.
2. Do not add relationship methods, return types, foreign key conventions, pivot APIs, eager loading APIs, polymorphic APIs, through relationship APIs, one-of-many APIs, factory relationship helpers, namespaces, classes, or query behavior unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or import in a malformed way, do not reproduce that malformed code. Run a narrower lookup or omit the malformed snippet while preserving only confirmed method names and concepts.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, database conventions, or general Laravel memory.

## Reference Map
- Basic relationship definitions for `hasOne()`, `hasMany()`, `belongsTo()`, `belongsToMany()`, dynamic properties, and relationship query-builder boundaries: [basic-relationships.md](./references/basic-relationships.md)
- Eager loading with `with()`, constrained `with()`, collection `load()`, lazy eager loading, `loadMissing()`, and `withWhereHas()`: [eager-loading-querying.md](./references/eager-loading-querying.md)
- Many-to-many operations with `attach()`, `detach()`, `sync()`, pivot attributes, `wherePivot()`, and custom pivot models: [many-to-many-pivot.md](./references/many-to-many-pivot.md)
- Polymorphic `morphTo()`, `morphMany()`, `loadMorph()`, factory polymorphic helpers, `hasManyThrough()`, `latestOfMany()`, `oldestOfMany()`, `ofMany()`, and `one()`: [polymorphic-through-one-of-many.md](./references/polymorphic-through-one-of-many.md)

## Workflow
1. Identify the exact surface: basic relationship definition, inverse relationship, dynamic property access, relationship query builder, eager loading, lazy eager loading, constrained eager loading, relationship existence with eager loading, many-to-many pivot operation, polymorphic relation, morph eager loading, through relationship, one-of-many relation, factory relationship helper, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented methods, return types, namespaces, imports, relationship names, query-builder chains, and examples.
5. For relationship topics not in the references, such as custom foreign keys, custom owner keys, `hasOneThrough()` definitions, `morphOne()` concrete examples, `morphToMany()` definitions, `morphedByMany()` definitions, `withPivot()` examples, `withTimestamps()`, touching parents, default models, counting aggregates, preventing lazy loading, or relationship testing, rely on the fresh Context7 lookup.
6. For reviews, flag only documented mismatches: wrong relationship method, missing documented return type, unconfirmed pivot operation, unconfirmed eager-loading API, malformed import/namespace, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Eloquent relationship methods are defined on model classes and return relationship type objects such as `HasMany`, `BelongsTo`, `BelongsToMany`, `MorphTo`, `MorphMany`, `HasManyThrough`, `HasOne`, or `HasOneThrough` in the returned docs.
- `hasMany(Post::class)` is documented for a `User::posts()` relationship and for a `Post::comments()` relationship.
- `hasOne(Phone::class)` is documented for a `User::phone()` relationship, though the returned namespace snippet was malformed and should not be copied as-is.
- `belongsTo(Author::class)` and `belongsTo(Post::class)` are documented inverse relationship examples.
- Many-to-many relationships are defined with methods that return `belongsToMany(...)`.
- Related models can be accessed through dynamic relationship properties such as `$post->tags`.
- `with('author')` eager loads a relationship to reduce query count.
- `with([... => function ($query) { ... }])` constrains eager loading queries.
- Collections and models can call `load(...)`; `loadMissing(...)` is documented for loading a relationship only if missing.
- `withWhereHas(...)` filters parent models based on relationship existence while eager loading those relationships.
- Many-to-many relationships support `attach(...)`, `detach(...)`, `sync(...)`, `syncWithPivotValues(...)`, and `syncWithoutDetaching(...)` in the returned docs.
- Pivot attributes are available through the `pivot` attribute in the documented many-to-many example.
- `wherePivot(...)` is documented for constraining `belongsToMany` queries by intermediate table columns.
- A custom pivot model may be selected with `using(RoleUser::class)` and must extend `Illuminate\Database\Eloquent\Relations\Pivot` according to the docs.
- Polymorphic relationships can use `morphTo()` on the child and `morphMany(...)` on parent models.
- `loadMorph(...)` is documented for eager loading nested relationships on `morphTo` relationships.
- `hasManyThrough(...)` is documented for `Application::deployments()`.
- `latestOfMany()`, `oldestOfMany()`, `ofMany(...)`, and `one()` are documented for one-of-many relationship patterns.

## Completion Check
- A fresh Context7 lookup was performed for the exact Eloquent relationship topic.
- Every method, return type, class, import, relationship name, pivot API, eager loading API, and behavior is traceable to the lookup or references.
- Malformed snippets from Context7 are not copied into final guidance.
- Unconfirmed relationship features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
