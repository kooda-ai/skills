---
name: laravel-13-http-client
description: 'Use when: working with Laravel 13 HTTP client, Http facade, Http::get(), Http::post(), head(), put(), patch(), delete(), JSON request data, Http::withHeaders(), response body(), json(), object(), collect(), resource(), status(), successful(), redirect(), failed(), clientError(), serverError(), header(), headers(), HTTP client exceptions, throw(), throwIf(), throwUnless(), throwIfStatus(), throwUnlessStatus(), throwIfServerError(), throwIfClientError(), retry(), withRequestMiddleware(), withResponseMiddleware(), Http::fake(), Http::assertSent(), Http::failedRequest(), and Laravel 13 HTTP client code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 HTTP client request, response, error handling, testing, or review task'
---

# Laravel 13 HTTP Client

## Purpose
Use this skill to create, review, or explain Laravel 13 HTTP client code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact HTTP client topic.
2. Do not add HTTP client methods, request options, headers, middleware APIs, response methods, exception behavior, retry behavior, fake/testing helpers, classes, facades, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, facade names, class names, callback signatures, URLs, and payload shapes.
5. Do not infer behavior from older Laravel versions, Guzzle documentation, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- `Http` facade request methods, JSON request payloads, `withHeaders()`, and response inspection methods: [requests-responses.md](./references/requests-responses.md)
- Response exception helpers, retry failure behavior, `onError()`, and request/response middleware boundaries: [errors-retries-middleware.md](./references/errors-retries-middleware.md)
- `Http::fake()`, `Http::assertSent()`, request inspection, and `Http::failedRequest()` testing boundary: [testing.md](./references/testing.md)

## Workflow
1. Identify the exact surface: outbound request method, request payload, request header, response body/status/header access, exception throwing, retry failure handling, middleware, faking, sent-request assertion, failed request simulation, or code review.
2. Query Context7 for that exact Laravel 13 HTTP client topic.
3. Load the relevant reference file from the map above.
4. Use only documented facades, methods, response helpers, callback types, exception classes, imports, and examples.
5. For request features not in the references, such as query parameters, form requests, raw bodies, `acceptJson()`, bearer tokens, timeout settings, connection timeout settings, attachments, pooling, macros, response sequences, recorded requests, stray request prevention, or global middleware, rely on a fresh Context7 lookup.
6. For reviews, flag only documented mismatches: unconfirmed HTTP client option, wrong facade import, unsupported response method, unconfirmed exception behavior, unsupported fake helper, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `Illuminate\Support\Facades\Http` is documented for making outbound HTTP requests.
- The docs confirm HTTP client methods including `head`, `get`, `post`, `put`, `patch`, and `delete`.
- `Http::get('http://example.com')` is a documented GET request example.
- `Http::post('http://example.com/users', ['name' => 'Steve'])` is a documented POST request example.
- For `POST`, `PUT`, and `PATCH` requests, passing an array as the second argument sends the data as JSON by default according to the docs.
- `Http::withHeaders([...])->post(...)` is documented in the sent-request assertion example.
- The documented response object is `Illuminate\Http\Client\Response`.
- The docs confirm response inspection methods including `body()`, `json()`, `object()`, `collect()`, `resource()`, `status()`, `successful()`, `redirect()`, `failed()`, `clientError()`, `header()`, and `headers()`.
- The docs state the response object implements `ArrayAccess` for direct JSON data access.
- Laravel's HTTP client wrapper does not throw exceptions for client or server errors by default according to the docs.
- The docs confirm `throw()`, `throwIf()`, `throwUnless()`, `throwIfStatus()`, `throwUnlessStatus()`, `throwIfServerError()`, and `throwIfClientError()` for throwing `Illuminate\Http\Client\RequestException` based on response status or conditions.
- The docs confirm `Http::retry(3, 100, throw: false)->post(...)` for returning the last response instead of throwing a `RequestException` when all retries fail.
- The docs confirm `onError()` as a way to execute a callback when a client or server error occurs.
- The docs confirm `withRequestMiddleware()` and `withResponseMiddleware()` for Guzzle middleware on specific requests.
- The docs confirm `Http::fake()` and `Http::assertSent(...)` for asserting sent requests.
- The docs confirm the `Http::assertSent(...)` closure receives an `Illuminate\Http\Client\Request` instance.
- The docs confirm request inspection with `hasHeader(...)`, `url()`, and array access for request payload fields in the assertion example.
- The docs confirm `Http::failedRequest([...], 404)` for simulating an `Illuminate\Http\Client\RequestException` in tests.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 HTTP client topic.
- Every facade, method, response helper, exception class, callback type, request option, fake helper, import, URL, and payload shape is traceable to the lookup or references.
- Guzzle-specific behavior is not inferred when the Laravel 13 HTTP client docs did not confirm it.
- Unconfirmed HTTP client features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
