---
name: laravel-13-authentication-account-flows
description: 'Use when: working with Laravel 13 authentication account flows, starter kits, registration, login, logout, password reset, forgot-password, reset-password, password confirmation, password.confirm middleware, email verification, MustVerifyEmail, verification.notice, verification.verify, verification.send, verified middleware, resend verification notifications, and Laravel 13 account-flow code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 registration, login, logout, password reset, password confirmation, email verification, or account-flow review task'
---

# Laravel 13 Authentication Account Flows

## Purpose
Use this skill to create, review, or explain Laravel 13 account flows such as starter-kit authentication scaffolding, manual login/logout, password reset, password confirmation, and email verification using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, routes, middleware guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact authentication account-flow topic.
2. Do not add starter-kit commands, generated files, route paths, route names, middleware aliases, form requests, contracts, notification methods, facades, session methods, password broker methods, events, or controller methods unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented route paths, route names, middleware aliases, contract names, class names, helper names, redirect targets, and example messages.
5. Do not infer behavior from older Laravel versions, Fortify docs, Breeze/Jetstream package docs, Sanctum docs, blog posts, source code, or general Laravel memory.
6. If the task depends on starter-kit package internals beyond what the Laravel 13 framework docs state, resolve and query the relevant package docs before adding those details.

## Reference Map
- Starter-kit authentication scaffolding, manual login attempts, session regeneration, and logout flow: [starter-kits-login-logout.md](./references/starter-kits-login-logout.md)
- Password reset request/reset routes, `Password::reset(...)`, reset status handling, and reset-link request boundary: [password-reset-flows.md](./references/password-reset-flows.md)
- Password confirmation routes, `password.confirm` middleware, `Hash::check(...)`, and session confirmation state: [password-confirmation.md](./references/password-confirmation.md)
- Email verification notice/handler/resend routes, `MustVerifyEmail`, `EmailVerificationRequest`, and `verified` middleware: [email-verification.md](./references/email-verification.md)

## Workflow
1. Identify the exact account-flow surface: starter-kit auth scaffolding, manual login, logout, forgot-password request form, password reset submission, password confirmation, email verification notice, verification handler, resend verification link, or route protection for verified users.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented route paths, route names, middleware aliases, facades, session methods, contract names, events, and redirect behavior.
5. Keep generic auth helpers, route auth middleware, validation rules, gates, policies, and authorization responses in `laravel-13-validation-auth`; use this slice for end-user account flows.
6. For starter-kit details not confirmed in the framework docs, such as exact package installation flags, generated controller lists, Fortify callbacks, or UI implementation details, rely on the fresh package-specific lookup.
7. For password-reset details not confirmed in the references, such as the exact `Password::sendResetLink(...)` route block, password broker configuration, custom brokers, reset notifications, or customized views, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unsupported route path or name, missing documented middleware alias, unconfirmed session regeneration or invalidation step, missing `MustVerifyEmail` contract where verification is expected, unsupported password-confirmation flow, or package behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel starter kits provide the routes, controllers, and views needed for user registration and authentication according to the starter-kit and authentication docs.
- The docs state installing a starter kit in a fresh application and running database migrations gives access to registration and login functionality.
- The starter-kit docs state these kits use Laravel Fortify for authentication logic.
- The docs show a manual login controller method validating `email` and `password`, calling `Auth::attempt($credentials)`, regenerating the session with `$request->session()->regenerate()`, and redirecting with `redirect()->intended('dashboard')`.
- The docs show logout using `Auth::logout()`, `$request->session()->invalidate()`, and `$request->session()->regenerateToken()` before redirecting to `/`.
- The password-reset docs show a guest-only `password.request` route at `/forgot-password` and a guest-only `password.reset` route at `/reset-password/{token}`.
- The password-reset docs show `Password::reset(...)` with `Hash::make(...)`, `setRememberToken(Str::random(60))`, and `event(new PasswordReset($user))` in the reset callback.
- The password-confirmation docs show a named `password.confirm` route at `/confirm-password` protected by `auth` middleware and a POST handler using `Hash::check(...)`, `$request->session()->passwordConfirmed()`, and `redirect()->intended()`.
- The docs show protecting sensitive routes with the `password.confirm` middleware alias.
- Email verification requires the user model to implement `Illuminate\Contracts\Auth\MustVerifyEmail` according to the verification docs.
- The docs show a verification notice route named `verification.notice`, a signed verification handler route named `verification.verify`, and a resend route named `verification.send`.
- The verification handler uses `Illuminate\Foundation\Auth\EmailVerificationRequest` and calls `$request->fulfill()`.
- The resend route calls `$request->user()->sendEmailVerificationNotification()` and uses `['auth', 'throttle:6,1']` middleware.
- The docs show protecting routes for verified users with `['auth', 'verified']` middleware.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 account-flow topic.
- Every route path, route name, middleware alias, facade method, session method, contract, event, request class, and redirect statement is traceable to the lookup or references.
- Generic auth helpers and authorization behavior are not duplicated when the existing `laravel-13-validation-auth` slice already owns them.
- Starter-kit package internals and Fortify-specific implementation details are not inferred from framework docs alone.
- Unconfirmed account-flow details are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
