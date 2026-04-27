---
name: laravel-13-requests-responses
description: 'Use when: working with Laravel 13 HTTP requests, Illuminate\Http\Request, request dependency injection, route closure Request injection, controller method injection, constructor injection, request input(), RedirectResponse, response helper, response headers, JSON responses, JSONP callbacks, view responses, downloads, redirect(), back(), with(), withInput(), flashed session data, Uri redirects, event stream frontend packages, useEventStream(), useJsonStream(), and Laravel 13 request/response code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 request, response, redirect, download, JSON, view response, stream frontend, or review task'
---

# Laravel 13 Requests And Responses

## Purpose
Use this skill to create, review, or explain Laravel 13 HTTP request and response code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact request, response, redirect, download, or stream topic.
2. Do not add request methods, response helpers, response macros, headers, cookies, redirect helpers, file response APIs, stream APIs, frontend stream package APIs, classes, imports, or middleware behavior unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented helper names, package names, method names, route strings, headers, and class imports.
5. Do not infer behavior from older Laravel versions, Symfony docs, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- `Illuminate\Http\Request`, dependency injection in controllers and route closures, controller constructor/method injection, and `input()`: [http-requests.md](./references/http-requests.md)
- String and array route responses, `response(...)`, headers, JSON/JSONP responses, view responses, and downloads: [responses-json-views-downloads.md](./references/responses-json-views-downloads.md)
- Redirects with flashed data/input, URI redirects, event stream frontend packages, `useEventStream()`, and `useJsonStream()`: [redirects-streams.md](./references/redirects-streams.md)

## Workflow
1. Identify the exact surface: request injection, request input, controller dependency injection, basic route response, custom response object, response header, JSON response, JSONP response, view response, file download, redirect, flashed session data, input flashing, URI redirect, event stream frontend consumption, JSON stream frontend consumption, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented classes, helpers, imports, package names, hooks, methods, options, and examples.
5. For request topics not in the references, such as path, URL, method, host, IP, headers, bearer tokens, query input, JSON input, boolean/date/enum retrieval, uploaded files, cookies, old input, or flashing input from the request object, rely on the fresh Context7 lookup.
6. For response topics not in the references, such as cookies, redirects by route/action, away redirects, streamed server responses, `streamJson`, `eventStream`, `streamDownload`, binary files, cache headers, response macros, or attachment headers, rely on the fresh Context7 lookup.
7. For reviews, flag only documented mismatches: unsupported request method, unconfirmed response helper, unconfirmed stream API, wrong package name, unconfirmed redirect method, missing documented binding, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `Illuminate\Http\Request` provides an object-oriented interface for incoming HTTP requests, including access to request data such as input, cookies, and uploaded files.
- Laravel's service container injects the current request when `Illuminate\Http\Request` is type-hinted in route closures or controller methods.
- The docs show `$request->input('name')` inside a controller method.
- Controller constructor injection and method injection are documented, including a `Request $request` parameter and a route parameter such as `string $id`.
- Routes may return strings, which Laravel converts into HTTP responses.
- Routes may return arrays, which Laravel converts into JSON payloads.
- `response('Hello World', 200)->header('Content-Type', 'text/plain')` is documented for custom response objects with status codes and headers.
- `response()->json([...])` is documented for JSON responses and automatically sets `Content-Type` to `application/json`.
- `response()->json(...)->withCallback($request->input('callback'))` is documented for JSONP responses.
- `response()->view('hello', $data, 200)->header('Content-Type', $type)` is documented for view responses with status and headers.
- `response()->download($pathToFile)` and `response()->download($pathToFile, $name, $headers)` are documented for file downloads, and the docs state the filename must be ASCII compatible.
- `redirect('/dashboard')->with('status', 'Profile updated!')` is documented for redirecting with flashed session data.
- `back()->withInput()` is documented for flashing the current request input before redirecting back.
- `Uri::of('https://example.com')->redirect()` and returning a `Uri` instance from a route are documented redirect patterns.
- The docs list `@laravel/stream-react`, `@laravel/stream-vue`, and `@laravel/stream-svelte` for consuming event streams and JSON streams in frontend frameworks.
- The docs document `useEventStream(...)` and `useJsonStream(...)` in the returned frontend stream examples.

## Completion Check
- A fresh Context7 lookup was performed for the exact request, response, redirect, download, or stream topic.
- Every request method, response helper, redirect helper, stream package, hook, option, class, import, header, and behavior is traceable to the lookup or references.
- Server-side stream APIs are not added unless a current Context7 lookup confirms them.
- Unconfirmed request/response features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
