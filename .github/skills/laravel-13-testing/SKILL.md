---
name: laravel-13-testing
description: 'Use when: working with Laravel 13 testing, Pest tests, PHPUnit tests, HTTP tests, feature tests, Tests\Feature, TestCase, get(), assertStatus(), assertSee(), actingAs(), withSession(), console tests, artisan(), expectsQuestion(), expectsOutput(), doesntExpectOutput(), assertExitCode(), facade testing, Cache::shouldReceive(), Exceptions::fake(), Exceptions::assertReported(), time travel helpers, and Laravel 13 test reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 test task, Pest/PHPUnit HTTP/console/facade/exception/time test, or review'
---

# Laravel 13 Testing

## Purpose
Use this skill to create, review, or explain Laravel 13 tests using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final test code or review findings, query Context7 for `/websites/laravel_13_x` with the exact testing topic.
2. Do not add test helpers, assertions, fakes, traits, namespaces, directory paths, factory behavior, database reset behavior, queue/event/mail/notification fakes, or mocking APIs unless they appear in the current Context7 result or [testing-patterns.md](./references/testing-patterns.md).
3. If a Context7 result renders a namespace or import in a malformed way, run a narrower lookup before using that import in code.
4. Do not infer behavior from older Laravel versions, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- HTTP tests, session/auth helpers, console tests, facade testing, exception reporting tests, model factories in tests, and time travel: [testing-patterns.md](./references/testing-patterns.md)

## Workflow
1. Identify the exact testing surface: HTTP request, response assertion, session/auth setup, console command, facade mock, exception reporting, factory-created model, time travel, Pest syntax, PHPUnit syntax, or test review.
2. Query Context7 for that exact Laravel 13 testing topic.
3. Load [testing-patterns.md](./references/testing-patterns.md).
4. Use only documented helper calls, assertions, facades, imports, test class names, and examples.
5. For features not in the reference, such as JSON assertions, redirects, validation assertions, database transactions, database assertions, file uploads, queues, events, mail, notifications, browser tests, or parallel testing, rely on the fresh Context7 lookup before adding code.
6. For reviews, flag only documented mismatches: unsupported helper, unconfirmed fake, unconfirmed assertion, wrong facade, missing documented import, or test behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The docs show both Pest and PHPUnit styles for HTTP, console, facade, and exception reporting tests.
- HTTP tests can use `$this->get('/')` and `$response->assertStatus(200)`.
- HTTP tests can use `actingAs($user)`, `withSession(['banned' => false])`, and `get('/')` together.
- Console tests can use `$this->artisan('question')`, `expectsQuestion(...)`, `expectsOutput(...)`, `doesntExpectOutput(...)`, and `assertExitCode(0)`.
- Facade testing can use `Cache::shouldReceive('get')->with('key')->andReturn('value')` and then assert the response with `assertSee('value')`.
- Exception reporting tests can use `Exceptions::fake()` and `Exceptions::assertReported(...)`.
- Time-sensitive Pest tests can use `$this->travel(1)->week()`.
- Factory-backed tests can use `User::factory()->create()` in documented examples.

## Completion Check
- A fresh Context7 lookup was performed for the exact testing topic.
- Every helper, assertion, facade, import, fake, factory call, and syntax choice is traceable to the lookup or reference.
- Unconfirmed testing features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
