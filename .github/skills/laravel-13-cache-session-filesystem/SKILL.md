---
name: laravel-13-cache-session-filesystem
description: 'Use when: working with Laravel 13 cache, Cache facade, Cache::get(), default cache values, Cache::add(), Cache::increment(), Cache::decrement(), Cache::forever(), Cache::forget(), session data, Request session(), session() helper, session get defaults, put(), push(), pull(), flash(), reflash(), keep(), now(), forget(), flush(), filesystem storage, Storage facade, disks, Storage::put(), Storage::disk(), file uploads, storeAs(), putFileAs(), Storage::url(), public disk, storage:link, storage:unlink, and Laravel 13 cache/session/filesystem code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 cache, session, filesystem, Storage facade, public disk, upload, or review task'
---

# Laravel 13 Cache, Session, And Filesystem

## Purpose
Use this skill to create, review, or explain Laravel 13 cache, session, and filesystem storage code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact cache, session, filesystem, upload, disk, or storage-link topic.
2. Do not add cache store names, config keys, cache methods, session methods, filesystem disks, storage methods, upload APIs, visibility behavior, URL behavior, symbolic link commands, helpers, facades, classes, or generated paths unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, command names, disk names, paths, helpers, and facades.
5. Do not infer behavior from older Laravel versions, Flysystem docs, S3 docs, cache driver docs, session driver docs, blog posts, source code, or general Laravel memory.

## Reference Map
- `Cache` facade retrieval, default values, `add()`, `increment()`, `decrement()`, `forever()`, and `forget()` boundary: [cache.md](./references/cache.md)
- Request session access, `session()` helper, `get()`, defaults, `put()`, `push()`, `pull()`, flash data, `forget()`, and `flush()`: [session.md](./references/session.md)
- `Storage` facade, disks, `put()`, uploaded file storage, `storeAs()`, `putFileAs()`, `storage:link`, public disk, URLs, `asset()`, and `storage:unlink`: [filesystem-storage.md](./references/filesystem-storage.md)

## Workflow
1. Identify the exact surface: cache retrieval, cache default value, cache counter, permanent cache storage, session retrieval, session mutation, flash data, session deletion, file storage, disk selection, uploaded file storage, public disk, storage link, file URL, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented facades, helpers, methods, commands, disk names, paths, and examples.
5. For cache topics not in the references, such as `put()`, `remember()`, `pull()`, tags, stores, locks, memoization, events, pruning, or testing, rely on the fresh Context7 lookup.
6. For session topics not in the references, such as `has()`, `missing()`, `all()`, `regenerate()`, `invalidate()`, CSRF/session security, blocking, drivers, configuration, or cookies, rely on the fresh Context7 lookup.
7. For filesystem topics not in the references, such as `get()`, `exists()`, `missing()`, `delete()`, `copy()`, `move()`, directories, visibility, temporary URLs, scoped/read-only disks, S3 setup, testing fakes, or file validation, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed method, wrong facade import, unconfirmed disk/path, unsupported command, unconfirmed helper, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `Illuminate\Support\Facades\Cache` is documented for cache access.
- `Cache::get('key')` retrieves a cache value and returns `null` if the key does not exist.
- `Cache::get('key', 'default')` returns a default value when the key does not exist.
- `Cache::add('key', 0, now()->plus(hours: 4))`, `Cache::increment(...)`, and `Cache::decrement(...)` are documented for integer cache values.
- `Cache::forever('key', 'value')` stores an item without an expiration time, and the docs state it must be manually removed using `forget()`.
- Session data can be retrieved from `$request->session()->get('key')`, with string or closure defaults.
- The global `session()` helper can retrieve values, retrieve defaults, or store key-value pairs.
- `$request->session()->put(...)`, `push(...)`, and `pull(...)` are documented for storing and modifying session data.
- `$request->session()->flash(...)`, `reflash()`, `keep(...)`, and `now(...)` are documented for flash data.
- `$request->session()->forget(...)` and `flush()` are documented for deleting session data.
- `Illuminate\Support\Facades\Storage` is documented for filesystem storage.
- `Storage::put('avatars/1', $content)` stores content on the default disk.
- `Storage::disk('s3')->put('avatars/1', $content)` stores content on a specific disk in the returned example.
- Uploaded files can use `$request->file('avatar')->storeAs(...)`, and `Storage::putFileAs(...)` is documented for custom names.
- `php artisan storage:link` creates the symbolic link for the public disk, and `php artisan storage:unlink` destroys configured symbolic links.
- The `public` disk is included in the application's `filesystems` configuration file, uses the `local` driver by default, and stores files in `storage/app/public` according to the docs.
- The docs state the public link maps `storage/app/public` to `public/storage`.
- `Storage::url('file.jpg')` and `asset('storage/file.txt')` are documented URL patterns.
- Additional symbolic links can be configured in the `links` array using `public_path(...)` and `storage_path(...)`.

## Completion Check
- A fresh Context7 lookup was performed for the exact cache, session, filesystem, upload, disk, URL, or symbolic link topic.
- Every facade, helper, method, command, disk, path, config file, and behavior is traceable to the lookup or references.
- Cache/session/filesystem driver behavior is not inferred when the current lookup did not confirm it.
- Unconfirmed cache/session/filesystem features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
