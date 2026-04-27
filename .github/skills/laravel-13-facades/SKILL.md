---
name: laravel-13-facades
description: 'Use when: working with Laravel 13 facades, Illuminate\Support\Facades namespace, facades vs dependency injection, facades vs helper functions, Facade base class behavior, getFacadeAccessor(), facade testing with shouldReceive(), real-time facades, Facades\ prefixes, and Laravel 13 facade code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 facades, real-time facades, facade testing, facade vs DI/helpers, or facade review task'
---

# Laravel 13 Facades

## Purpose
Use this skill to create, review, or explain Laravel 13 facade concepts, real-time facades, and facade-specific testing patterns using only details confirmed in the current Laravel 13.x documentation.

## Source Rule
1. Before giving final code, commands, architecture guidance, or review findings, query the current Laravel 13.x documentation for the exact facade topic.
2. Do not add facade behavior, imports, namespace rules, base-class internals, real-time facade patterns, testing helpers, helper comparisons, or facade root mappings unless they appear in the current documentation result or the reference files below.
3. If a requested detail is not confirmed by the current documentation result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented namespace segments, facade names, binding names, helper names, class names, and testing methods.
5. Do not infer behavior from older Laravel versions, framework source, blog posts, package docs, or general Laravel memory.
6. Use feature-specific split skills for the underlying APIs behind facades such as `Cache`, `Storage`, `Log`, `Http`, `Auth`, `URL`, `Route`, `Schema`, `DB`, or `Mail`. Use this slice when the task is specifically about facades as an abstraction.

## Reference Map
- Facade purpose, namespace, facade vs dependency injection, facade vs helper functions, `shouldReceive()`, and how facade resolution works: [facade-concepts.md](./references/facade-concepts.md)
- Real-time facades, `Facades\` imports, and real-time facade testing patterns: [real-time-facades.md](./references/real-time-facades.md)
- Facade class reference structure and representative facade-to-root mappings from the Laravel 13 reference table: [facade-class-reference.md](./references/facade-class-reference.md)

## Workflow
1. Identify the exact surface: facade import, facade namespace, facade vs dependency injection, facade vs helper, facade testing, facade root resolution, `getFacadeAccessor()`, real-time facade, `Facades\` import, or facade class reference lookup.
2. Query the current Laravel 13.x documentation for that exact topic.
3. Load the relevant reference file from the map above.
4. Use only documented imports, helper names, methods, class names, binding names, and examples.
5. Route feature-specific API questions to the owning split skill when the real task is about cache, auth, logging, HTTP client, URL generation, database access, filesystem storage, queues, mail, notifications, or validation rather than facade behavior itself.
6. For reviews, flag only documented mismatches: wrong facade namespace, unsupported facade claim, misuse of real-time facade imports, unconfirmed facade testing pattern, unconfirmed helper equivalence statement, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel facades provide a static-looking interface to objects available in the service container.
- Laravel facades are in the `Illuminate\Support\Facades` namespace.
- The docs show facades such as `Cache` and `Route` imported from `Illuminate\Support\Facades`.
- The docs describe facades as static proxies to underlying service-container classes and state that they remain more testable and flexible than traditional static methods.
- The docs compare facades with dependency injection and show facade testing with `Cache::shouldReceive(...)`.
- The docs compare facades with helper functions and state there is no practical difference between a documented helper call and its corresponding facade call.
- The docs warn about class scope creep when many facades are used in a single class.
- The docs show that facades extend `Illuminate\Support\Facades\Facade` and use `__callStatic()` to defer calls to the container-resolved object.
- The docs show `getFacadeAccessor()` returning the binding name used to resolve the underlying service from the container.
- The docs show real-time facades by prefixing an imported class or interface with `Facades\`.
- The docs show real-time facades can be tested with `shouldReceive(...)`.
- The docs include a facade class reference table listing facade name, underlying class, and service-container binding key where applicable.

## Completion Check
- A fresh Laravel 13 documentation lookup was performed for the exact facade topic.
- Every namespace, helper comparison, testing method, base-class statement, real-time facade rule, and facade root mapping is traceable to the lookup or references.
- Feature-specific facade APIs remain delegated to their owning split skills.
- Unconfirmed facade behavior is omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.