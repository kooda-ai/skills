# Support Utility Boundaries

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x helpers, strings, and collections.

## Confirmed In This Slice
This slice confirms only the support utilities returned by the current Context7 lookups:

- `collect(...)` and `Illuminate\Support\Collection` basics.
- `pluck(...)` and `groupBy(...)` examples.
- `Illuminate\Support\LazyCollection`, `LazyCollection::make(...)`, `cursor()`, `lazy()`, and `lazyById()` examples.
- `Illuminate\Support\Str`, `Str::of(...)`, and fluent string method examples.
- `str(...)` returning `Illuminate\Support\Stringable` when passed a string.
- `str()` returning an `Illuminate\Support\Str` instance when no argument is provided.
- `Str::chopEnd(...)`.

## Not Confirmed In This Slice
Do not add concrete APIs for these helper families unless a fresh Context7 lookup confirms them:

- `Illuminate\Support\Arr` methods.
- `Illuminate\Support\Number` methods.
- Path helpers such as application, base, config, database, public, resource, or storage paths.
- Miscellaneous helpers such as `blank`, `filled`, `rescue`, `tap`, `value`, `with`, `once`, or `retry`.
- UUID, ULID, random string, slug, pluralization, word, markdown, or masking helpers not returned in the current string lookup.
- Collection methods not named in [collections.md](./collections.md) or [lazy-collections.md](./lazy-collections.md).

## Review Checklist
When reviewing helper or collection code, check only documented issues:

- Using a helper family that this slice does not confirm without a fresh Context7 lookup.
- Copying malformed namespaces from Context7 results without a narrower lookup.
- Assuming every collection method mutates the same instance despite the docs stating collections are generally immutable.
- Claiming Eloquent `cursor()` loads all models at once despite the docs stating it loads one model at a time.
- Using query builder lazy updates without considering the documented `lazyById()` guidance for modifying records.
