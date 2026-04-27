---
name: laravel-13-validation-auth
description: 'Use when: working with Laravel 13 validation, request validate(), form requests, make:request, rules(), messages(), validated(), safe(), authorize(), validation redirects or JSON responses, authentication, Auth facade, Auth::login(), Auth::loginUsingId(), Auth::user(), Auth::id(), request user(), auth middleware, verified middleware, authorization gates, policies, Gate::authorize(), Gate::define(), Response::denyWithStatus(), Response::denyAsNotFound(), Blade @can directives, Authorize attribute, and Laravel 13 validation/auth code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 validation, form request, auth, authorization, policy, gate, middleware, or review task'
---

# Laravel 13 Validation And Auth

## Purpose
Use this skill to create, review, or explain Laravel 13 validation, form request, authentication, and authorization code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, or review findings, query Context7 for `/websites/laravel_13_x` with the exact validation, authentication, or authorization topic.
2. Do not add validation rules, request methods, form request hooks, authentication commands, starter-kit behavior, guards, middleware names, facades, policy methods, gate helpers, Blade directives, attributes, or authorization response behavior unless they appear in the current Context7 result or the reference files below.
3. If the user asks about package-specific authentication such as Sanctum, resolve and query that package's Context7 library before adding package behavior beyond snippets returned by the Laravel 13 framework docs.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Controller validation, form request generation, `rules()`, `messages()`, `validated()`, `safe()`, and `authorize()`: [validation-form-requests.md](./references/validation-form-requests.md)
- `Auth` facade login/user helpers, route auth middleware, verified middleware, and the documented Sanctum middleware snippet: [authentication.md](./references/authentication.md)
- Gates, policies, authorization responses, Blade authorization directives, and controller authorization attribute: [authorization.md](./references/authorization.md)

## Workflow
1. Identify the exact surface: controller validation, form request generation, form request rules/messages/authorization, validated data retrieval, authentication helper, route protection, guard-specific middleware, verified routes, gate check, policy method, authorization response, Blade authorization, controller authorization attribute, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented methods, imports, middleware names, commands, generated paths, rule examples, response behavior, and directive syntax.
5. For validation topics not in the reference, such as custom rules, conditional validation, `Validator` facade usage, error bags, old input, localization, file validation, or nested array validation, rely on the fresh Context7 lookup.
6. For authentication topics not in the reference, such as starter kits, registration, passwords, sessions, logout, remember tokens, guards configuration, password confirmation, password reset, or email verification internals, rely on the fresh Context7 lookup.
7. For authorization topics not in the reference, such as policy generation commands, policy discovery, `can` / `cannot` methods, middleware authorization, inline authorization, before/after hooks, or custom denial messages, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unsupported helper, unconfirmed middleware, wrong facade import, unconfirmed rule syntax, unconfirmed generated path, unsupported policy signature, or package behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `$request->validate([...])` is documented inside a controller and automatically returns a redirect or JSON response when validation fails.
- Validation rules may be expressed as pipe-delimited strings or arrays in the documented examples.
- `php artisan make:request StorePostRequest` creates a custom form request class in `app/Http/Requests`.
- `php artisan make:controller PhotoController --model=Photo --resource --requests` creates request classes such as `StorePhotoRequest` and `UpdatePhotoRequest` in `app/Http/Requests` for generated controller `store` and `update` methods.
- A form request `rules(): array` method returns validation rules.
- A form request `messages(): array` method returns custom error strings.
- Type-hinting a form request in a controller method automatically triggers validation before the method body executes.
- `$request->validated()` returns validated input data in the documented form request example.
- `$request->safe()->only([...])` and `$request->safe()->except([...])` retrieve portions of validated input data in the documented example.
- A form request `authorize` method controls whether the authenticated user may perform the action; returning `false` automatically returns a 403 response and prevents the controller method from executing.
- The `Auth` facade is documented with `login()`, `guard(...)->login()`, `loginUsingId()`, `user()`, and `id()` examples.
- `$request->user()` is documented for retrieving the authenticated user from a controller request.
- The docs show route protection with `middleware('auth')`, `middleware('auth:admin')`, and `middleware(['auth', 'verified'])`.
- `Gate::authorize('create', Post::class)` is documented for authorizing actions that do not require a model instance and throws an authorization exception that results in a 403 HTTP response when unauthorized.
- A policy method may accept `User $user` and a model such as `Post $post`, and policies are resolved via the service container.
- The docs show `Gate::define(...)` returning `Response::allow()`, `Response::denyWithStatus(404)`, or `Response::denyAsNotFound()`.
- Blade authorization directives documented in the returned context include `@can`, `@elsecan`, `@endcan`, `@canany`, and `@endcanany`.
- The docs show `#[Authorize('create', [Comment::class, 'post'])]` as a shortcut for policy-based authorization on controller methods.

## Completion Check
- A fresh Context7 lookup was performed for the exact validation, authentication, or authorization topic.
- Every validation rule, request method, command, generated path, middleware name, facade method, policy signature, gate helper, directive, attribute, and response behavior is traceable to the lookup or references.
- Package-specific auth behavior is not inferred from Laravel framework docs alone.
- Unconfirmed validation/auth features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
