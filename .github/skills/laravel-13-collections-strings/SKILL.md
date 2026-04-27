---
name: laravel-13-collections-strings
description: 'Use when: working with Laravel 13 collections, collect(), Illuminate\Support\Collection, collection pipelines, pluck(), groupBy(), lazy collections, LazyCollection, cursor(), lazy(), lazyById(), string helpers, Illuminate\Support\Str, Str::of(), str(), Stringable, fluent string methods, string validation methods, Str::chopEnd(), and Laravel 13 collection/string code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 collection, lazy collection, Str/Stringable helper, or review task'
---

# Laravel 13 Collections And Strings

## Purpose
Use this skill to create, review, or explain Laravel 13 collections, lazy collections, and string helper code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact collection, lazy collection, string helper, or support utility topic.
2. Do not add collection methods, lazy collection APIs, helper functions, string methods, imports, class names, immutability behavior, Eloquent collection behavior, query streaming behavior, or examples unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or import in a malformed way, run a narrower lookup before using that import in code.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented helper names, class names, method names, callback shapes, and example values.
6. Do not infer behavior from older Laravel versions, PHP SPL docs, Symfony docs, package docs, source code, blog posts, or general Laravel/PHP memory.

## Reference Map
- `collect()`, `Illuminate\Support\Collection`, collection immutability, `pluck(...)`, and `groupBy(...)`: [collections.md](./references/collections.md)
- `Illuminate\Support\LazyCollection`, `LazyCollection::make(...)`, Eloquent `cursor()`, `lazy()`, and query builder `lazy()` / `lazyById()`: [lazy-collections.md](./references/lazy-collections.md)
- `Illuminate\Support\Str`, `Str::of(...)`, `str(...)`, `Stringable`, fluent string examples, string validation methods, and `Str::chopEnd(...)`: [strings.md](./references/strings.md)
- Boundaries for unconfirmed helper families such as `Arr`, `Number`, path helpers, and miscellaneous helpers: [support-boundaries.md](./references/support-boundaries.md)

## Workflow
1. Identify the exact surface: collection creation, collection transformation, `pluck`, `groupBy`, lazy collection generator, Eloquent cursor streaming, query builder lazy streaming, fluent string operation, `str()` helper, string validation, `Str::chopEnd`, or support utility review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented helpers, methods, classes, imports, callback signatures, behavior statements, and examples.
5. For collection topics not in the references, such as `map`, `filter`, `reject`, `reduce`, `sortBy`, `values`, `each`, `contains`, `partition`, macros, higher-order messages, or method return details beyond the returned snippets, rely on the fresh Context7 lookup.
6. For lazy collection topics not in the references, such as `chunkWhile`, file streaming details beyond the returned generator example, cursor pagination, generator cleanup behavior, or database streaming caveats beyond `lazyById`, rely on the fresh Context7 lookup.
7. For string/helper topics not in the references, such as `Arr`, `Number`, path helpers, `blank`, `filled`, `rescue`, `tap`, `value`, `once`, UUID/ULID generation, pluralization, slugging, random strings, or full method signatures for unlisted `Str` methods, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed helper, malformed import copied from Context7, unsupported collection method claim, unconfirmed lazy streaming behavior, unconfirmed string method, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `Illuminate\Support\Collection` provides a fluent wrapper for working with arrays of data.
- The docs show creating a collection with `collect([1, 2, 3])`.
- The docs state collections allow chaining methods for fluent mapping and reducing of the underlying array.
- The docs state collections are generally immutable, meaning each `Collection` method returns an entirely new `Collection` instance.
- The docs state collections can also be created using `make` and `fromJson` methods.
- The docs state Eloquent query results are always returned as `Collection` instances.
- `pluck(...)` retrieves values for a key, can key results by another key, supports nested values using dot notation, and uses the last matching item when duplicate keys exist.
- `groupBy(...)` groups items by a key or callback and can handle multiple grouping criteria with `preserveKeys: true` in the returned example.
- `Illuminate\Support\LazyCollection` leverages PHP generators to process large datasets efficiently while minimizing memory usage.
- `LazyCollection::make(...)` is documented with a generator that reads lines from a file handle, then chains `chunk(...)`, `map(...)`, and `each(...)`.
- Eloquent `cursor()` returns a `LazyCollection` and loads only one model at a time according to the docs.
- `collect([1, 2, 3, 4])->lazy()` returns a `LazyCollection` instance.
- Query builder `lazy()` and `lazyById()` return `LazyCollection` streams according to the docs.
- The docs state `lazyById()` should be used when modifying records during iteration to ensure consistent iteration.
- `Illuminate\Support\Str` is documented for fluent string operations using `Str::of(...)`.
- The `str(...)` helper returns an `Illuminate\Support\Stringable` instance for a given string and is equivalent to `Str::of(...)` according to the docs.
- Calling `str()` without an argument returns an instance of `Illuminate\Support\Str` according to the docs.
- The docs show `Str::of(...)` examples for `after`, `afterLast`, `apa`, `append`, `ascii`, `basename`, `before`, `beforeLast`, `between`, `betweenFirst`, `camel`, `charAt`, and `classBasename`.
- The docs show fluent validation methods such as `is`, `isAscii`, `isEmpty`, `isJson`, `isUlid`, `isUrl`, and `isUuid`.
- `Str::chopEnd(...)` removes the last occurrence of a value only if that value appears at the end of the string, and the docs state the value may be a string or array.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 collection, lazy collection, string helper, or support utility topic.
- Every helper, method, class, import, callback shape, behavior statement, and example is traceable to the lookup or references.
- Array helpers, number helpers, miscellaneous helpers, string methods, and collection methods are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed collection/string/support utility features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
