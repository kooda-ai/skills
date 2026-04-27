---
name: laravel-13-pagination-urls
description: 'Use when: working with Laravel 13 pagination, paginate(), simplePaginate(), cursorPaginate(), pagination links, appends(), withQueryString(), withPath(), fragment(), onEachSide(), pagination views, paginator JSON, manual paginator classes, URL generation, url(), route(), URL facade, named route parameters, query URLs, current/previous URLs, signed URLs, URL::signedRoute(), URL::temporarySignedRoute(), signed middleware, hasValidSignature(), and Laravel 13 pagination/URL code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 pagination, URL generation, signed URL, paginator view, or review task'
---

# Laravel 13 Pagination And URLs

## Purpose
Use this skill to create, review, or explain Laravel 13 pagination, URL generation, named route URLs, query-string URL helpers, and signed URLs using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact pagination or URL topic.
2. Do not add paginator classes, pagination methods, pagination view commands, JSON keys, URL helpers, URL facade methods, route helper behavior, signed URL APIs, middleware names, exception classes, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or import in a malformed way, run a narrower lookup before using that import in code.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented helper names, facade methods, middleware strings, command names, paths, query parameter names, route names, and example values.
6. Do not infer behavior from older Laravel versions, frontend packages, route model binding details beyond returned snippets, database vendor docs, package docs, source code, blog posts, or general Laravel memory.

## Reference Map
- Eloquent/query builder pagination, `paginate()`, `simplePaginate()`, `cursorPaginate()`, URL customization, manual paginator classes, view customization, Bootstrap view selection, and paginator JSON: [pagination.md](./references/pagination.md)
- `url()` and `route()` helpers, named route parameters, Eloquent model parameters, query URLs, current/full/previous URLs, and URL default boundary: [url-generation.md](./references/url-generation.md)
- `URL::signedRoute()`, `URL::temporarySignedRoute()`, relative signed URLs, request signature validation, signed middleware, and invalid signature rendering: [signed-urls.md](./references/signed-urls.md)

## Workflow
1. Identify the exact surface: Eloquent pagination, query builder pagination, simple pagination, cursor pagination, paginator link customization, custom pagination view, Bootstrap pagination views, paginator JSON response, manual paginator instance, arbitrary URL generation, named route URL generation, query string URLs, current/previous URL access, signed URL creation, temporary signed URL, signature validation, signed middleware, invalid signed URL response, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented helpers, facade methods, paginator methods, command names, classes, middleware strings, exception classes, response behavior, and examples.
5. For pagination topics not in the references, such as pagination configuration files, custom default views beyond Bootstrap snippets, `onEachSide()` variants, cursor limitations beyond the returned order-by statement, multiple paginator page names, custom page resolvers, or API resource pagination beyond the existing API resource skill, rely on the fresh Context7 lookup.
6. For URL topics not in the references, such as route model binding internals, controller/action URL helpers, asset URLs, secure URLs, URL macros, force root URL, force scheme, default URL middleware imports, or localization URL patterns, rely on the fresh Context7 lookup.
7. For signed URL topics not in the references, such as ignoring signed URL parameters in middleware, named middleware aliases, exception handler imports beyond shown snippets, expiration edge cases, or custom invalid-signature flows beyond the returned example, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed paginator method, unsupported cursor pagination assumption, wrong signed middleware string, unconfirmed signature validation API, unconfirmed URL helper behavior, malformed import copied from Context7, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `User::paginate(15)` is documented for paginating Eloquent results.
- `DB::table('users')->simplePaginate(15)` is documented when only Next and Previous links are needed.
- `DB::table('users')->orderBy('id')->cursorPaginate(15)` is documented for cursor pagination and requires an `orderBy` clause in the returned docs.
- `User::where('votes', '>', 100)->cursorPaginate(15)` is documented for Eloquent cursor pagination.
- Paginator links can append explicit query parameters with `appends(['sort' => 'votes'])`.
- Paginator links can append all current request query string values with `withQueryString()`.
- Paginator links can use a custom path with `withPath('/admin/users')`.
- Paginator links can append a hash fragment with `fragment('users')`.
- The docs show `$paginator->url($page)` for generating a URL for a specific page.
- The docs show `$paginator->getPageName()` and state the default query-string page parameter is `page`.
- Pagination link output can be customized with `links('view.name')` and `links('view.name', ['foo' => 'bar'])`.
- `php artisan vendor:publish --tag=laravel-pagination` publishes pagination views to `resources/views/vendor/pagination`.
- `Paginator::useBootstrapFive()` and `Paginator::useBootstrapFour()` are documented in an `App\Providers\AppServiceProvider` `boot(): void` example.
- The docs show `{{ $users->onEachSide(5)->links() }}` for adjusting the pagination link window.
- Returning `User::paginate()` directly from a route automatically serializes paginator results to JSON with metadata and data.
- Manual paginator classes documented by the current docs include `Illuminate\Pagination\Paginator`, `Illuminate\Pagination\LengthAwarePaginator`, and `Illuminate\Pagination\CursorPaginator`.
- The `url()` helper can generate arbitrary URLs and `url()->query(...)` can add query parameters, overwrite existing values, and handle array parameters.
- `route(...)` generates URLs for named routes, handles route parameters, and appends extra arguments to the query string according to the docs.
- `route('post.show', ['post' => $post])` is documented for generating a URL from an Eloquent model parameter.
- `url()->current()`, `url()->full()`, `URL::current()`, `url()->previous()`, and `url()->previousPath()` are documented.
- `URL::signedRoute('unsubscribe', ['user' => 1])` is documented for creating signed URLs.
- `URL::signedRoute(..., absolute: false)` is documented for relative signed URLs.
- `URL::temporarySignedRoute(...)` is documented for signed URLs that expire after a specified duration.
- `$request->hasValidSignature()` and `$request->hasValidSignatureWhileIgnoring(['page', 'order'])` are documented.
- The `signed` middleware is documented for automatic signed URL validation and returns a `403` response if the signature is invalid.
- The `signed:relative` middleware string is documented for relative signed URLs.
- The docs show rendering `Illuminate\Routing\Exceptions\InvalidSignatureException` to a custom `errors.link-expired` view with status `403` in `bootstrap/app.php`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 pagination or URL topic.
- Every paginator method, class, helper, facade method, middleware string, exception class, command, path, JSON statement, and behavior is traceable to the lookup or references.
- Route model binding internals, frontend pagination behavior, URL defaults, signed URL edge cases, and package-specific behavior are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed pagination or URL features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
