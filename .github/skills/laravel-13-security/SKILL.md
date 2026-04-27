---
name: laravel-13-security
description: 'Use when: working with Laravel 13 security utilities, hashing, Hash facade, Hash::make(), Hash::check(), Hash::needsRehash(), HASH_DRIVER, encryption, Crypt facade, Crypt::encryptString(), Crypt::decryptString(), DecryptException, APP_KEY, APP_PREVIOUS_KEYS, key:generate, CSRF protection, @csrf, csrf_token(), X-CSRF-TOKEN, X-XSRF-TOKEN, preventRequestForgery(), RateLimiter, Limit::perMinute(), throttle middleware, RateLimiter::attempt(), and Laravel 13 security code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 hashing, encryption, CSRF, rate limiting, or security review task'
---

# Laravel 13 Security

## Purpose
Use this skill to create, review, or explain Laravel 13 framework security utilities such as hashing, encryption, CSRF protection, and rate limiting using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact security topic.
2. Do not add hashing drivers, hashing methods, encryption methods, environment variables, config keys, CSRF middleware APIs, CSRF headers, rate limiter methods, `Limit` methods, middleware strings, imports, exception classes, status codes, or examples unless they appear in the current Context7 result or the reference files below.
3. If a security topic belongs to a package such as Sanctum, Scout, Fortify, or a frontend client library, use only the package-specific details returned by the current lookup or resolve and query that package's Context7 docs before adding package behavior.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented facade names, method names, middleware strings, header names, environment variable names, exception classes, status codes, and example values.
6. Do not infer behavior from older Laravel versions, OWASP guides, browser docs, package docs, source code, blog posts, or general Laravel/security memory.

## Reference Map
- `Hash` facade usage, `Hash::make()`, `Hash::check()`, `Hash::needsRehash()`, hashing drivers, `HASH_DRIVER`, and hashing config boundary: [hashing.md](./references/hashing.md)
- `Crypt` facade usage, `Crypt::encryptString()`, `Crypt::decryptString()`, `DecryptException`, `APP_KEY`, `key:generate`, `APP_PREVIOUS_KEYS`, MAC tamper detection, and key rotation behavior: [encryption.md](./references/encryption.md)
- CSRF form tokens, `@csrf`, `csrf_token()`, `X-CSRF-TOKEN`, `X-XSRF-TOKEN`, `preventRequestForgery(...)`, and CSRF boundaries: [csrf.md](./references/csrf.md)
- Named route rate limiters, `RateLimiter`, `Limit`, `throttle` middleware, response-based limiters, custom responses, action rate limiting, manual attempts, and clearing attempts: [rate-limiting.md](./references/rate-limiting.md)

## Workflow
1. Identify the exact surface: password hashing, hash verification, hash rehashing, hashing driver configuration, string encryption, string decryption, encryption key configuration, key rotation, CSRF form token, CSRF AJAX header, CSRF cookie header, CSRF URI exclusion, named route limiter, throttle middleware, response-based route limiter, rate-limited action, manual rate-limit attempt tracking, or security review.
2. Query Context7 for that exact Laravel 13 security topic.
3. Load the relevant reference file from the map above.
4. Use only documented facades, methods, environment variables, config keys, middleware configuration APIs, header names, exception classes, status codes, imports, and examples.
5. For hashing topics not in the references, such as per-driver option names, `Hash::driver()`, `isHashed`, custom hashers, algorithm verification details, or password validation rules, rely on the fresh Context7 lookup.
6. For encryption topics not in the references, such as object/array encryption APIs beyond `encryptString`, serialization behavior, cipher configuration, multi-key examples beyond `APP_PREVIOUS_KEYS`, or decrypting non-string payloads, rely on the fresh Context7 lookup.
7. For CSRF topics not in the references, such as middleware class names, route-specific exclusions beyond `preventRequestForgery`, test helpers, SPA package setup, Sanctum authentication flows, or frontend client behavior beyond returned header/cookie statements, rely on the fresh Context7 lookup and package-specific docs when needed.
8. For rate limiting topics not in the references, such as `Limit::none`, multiple limits, Redis throttle configuration, named middleware aliases, queue rate limiting, event throttling, or exact response headers beyond the custom-response callback shape, rely on the fresh Context7 lookup.
9. For reviews, flag only documented mismatches: missing documented hash verification, storing plain secrets when docs show encryption, unconfirmed encryption API, missing CSRF token/header for documented forms/AJAX, unsafe CSRF exclusions not backed by docs, wrong throttle middleware string, unconfirmed rate limiter method, or package behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The `Hash` facade provides secure Bcrypt and Argon2 hashing for storing user passwords.
- Laravel uses the `bcrypt` hashing driver by default according to the hashing docs.
- Supported hashing drivers returned by the docs include `bcrypt`, `argon`, and `argon2id`.
- The hashing driver may be specified with the `HASH_DRIVER` environment variable.
- The docs show `Hash::make($request->newPassword)` before storing a password.
- The docs show `Hash::check('plain-text', $hashedPassword)` to verify a plain-text password against a hash.
- The docs show `Hash::needsRehash($hashed)` to determine whether current hash settings require updating a stored hash.
- Laravel encryption is configured through the `key` option in `config/app.php`, driven by the `APP_KEY` environment variable.
- The docs state `php artisan key:generate` should be used to generate the `APP_KEY` value.
- The docs show `Crypt::encryptString($request->token)` for encrypting a string before storage.
- The docs state encrypted values use OpenSSL and AES-256-CBC and are signed with a message authentication code to prevent decrypting tampered values.
- The docs show `Crypt::decryptString($encryptedValue)` inside a `try` / `catch` for `Illuminate\Contracts\Encryption\DecryptException`.
- The docs state changing `APP_KEY` logs out authenticated users and prevents decrypting data encrypted with the previous key unless previous keys are configured.
- The docs state `APP_PREVIOUS_KEYS` may contain comma-delimited previous encryption keys for graceful decryption after key rotation.
- The docs show `@csrf` inside a form and state it is equivalent to a hidden `_token` input using `csrf_token()`.
- The CSRF docs state Laravel checks CSRF tokens as POST parameters and supports the `X-CSRF-TOKEN` request header.
- The docs state Laravel provides an encrypted `XSRF-TOKEN` cookie and JavaScript libraries such as Angular and Axios can include it as the `X-XSRF-TOKEN` request header for same-origin requests.
- The docs show excluding CSRF URIs in `bootstrap/app.php` with `$middleware->preventRequestForgery(except: [...])`.
- The docs state CSRF middleware is automatically disabled during automated tests.
- The docs show named rate limiters registered with `RateLimiter::for(...)` and `Limit::perMinute(...)->by(...)`.
- The docs show applying a named route limiter with `Route::middleware(['throttle:uploads'])->group(...)`.
- The docs state exceeding a named limiter returns a `429` HTTP status code by default and custom responses can be configured with `Limit::response(...)`.
- The docs show response-based route limiting using `Limit::perMinute(...)->by(...)->after(function (Response $response) { ... })`.
- The docs show `RateLimiter::attempt(...)`, `RateLimiter::tooManyAttempts(...)`, `RateLimiter::increment(...)`, `RateLimiter::remaining(...)`, `RateLimiter::availableIn(...)`, and `RateLimiter::clear(...)` for manually rate-limited actions.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 security topic.
- Every facade, method, environment variable, config key, middleware API, middleware string, header name, exception class, status code, import, and behavior statement is traceable to the lookup or references.
- Package-specific security behavior, browser behavior, frontend client behavior, hashing options, encryption options, and rate limiter APIs are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed security features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.