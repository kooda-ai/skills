---
name: livewire-4-testing
description: 'Use when: working with Livewire 4 Testing, Livewire::test(), PHPUnit Livewire tests, Pest-style tests, component mounting, mount parameters, set(), toggle(), call(), refresh(), dispatch(), assertSee(), assertViewHas(), assertHasErrors(), assertDispatched(), assertRedirect(), assertForbidden(), assertJs(), assertNoJs(), file upload tests, Storage::fake(), UploadedFile::fake(), and documented testing helpers. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 component test, validation test, upload test, event assertion, redirect, forbidden action, JS assertion, or testing helper concern'
---

# Livewire 4 Testing

## Purpose
Use this skill to create, review, or explain Livewire 4 tests using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 Testing topic.
2. Do not add testing helpers, namespaces, assertions, method signatures, Pest or PHPUnit conventions, upload behavior, event behavior, authorization behavior, redirect behavior, or JavaScript assertion behavior unless they appear in the retrieved documentation.
3. If a requested Testing detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented class names, component names, method names, property names, assertion names, callback parameters, and value strings.
5. Do not infer testing APIs from Livewire 3, Laravel HTTP tests, Pest habits, PHPUnit habits, browser tests, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Component mounting, interaction helpers, and rendered output assertions: [component-interactions.md](./references/component-interactions.md)
- Validation tests, form-object cautions, and file upload tests: [validation-forms-uploads.md](./references/validation-forms-uploads.md)
- Events, redirects, forbidden actions, JavaScript assertions, and unconfirmed helpers: [events-side-effects.md](./references/events-side-effects.md)

## Workflow
1. Identify the test target: component mounting, mount parameters, rendered content, view data, public property mutation, action call, action parameters, validation error, form object, file upload, dispatched event, redirect, forbidden action, JavaScript evaluation, or browser-event dispatch from the test.
2. Run a narrow Context7 query for the exact Livewire 4.x Testing topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. Start component tests with documented `Livewire::test(...)` usage, choosing a component name string or component class plus mount parameters only when the current lookup confirms the shape.
5. Interact with components using only documented helpers from the lookup, such as `set()`, array `set([...])`, `toggle()`, `call()`, parameterized `call()`, `refresh()`, and `dispatch()`.
6. Assert rendered output or view data with documented helpers from the lookup, such as `assertSee()` and `assertViewHas()`.
7. For validation tests, set invalid state, call the validating action, and use documented `assertHasErrors()` shapes.
8. For form-object tests, first confirm the testing syntax for the form property path in the current Context7 result; do not assume `form.*` test paths from Blade binding examples alone.
9. For file uploads, use only documented Laravel fake upload and storage helpers returned by the lookup, such as `Storage::fake()`, `UploadedFile::fake()->image()`, `set()`, `call()`, and `Storage::disk(...)->assertExists()`.
10. For events and side effects, use only documented assertions returned by the lookup, such as `assertDispatched()`, `assertRedirect()`, `assertForbidden()`, `assertJs()`, and `assertNoJs()`.
11. Finish by checking that every helper, assertion, class, namespace, callback argument, component identifier, mount parameter, action parameter, and side-effect claim is traceable to the current Context7 result and the loaded reference file.

## Decision Points
- Use a component name string when the docs-confirmed example targets a named component such as `post.create` or `show-posts`.
- Use a component class when the docs-confirmed example targets a class such as `UpdatePost::class` or `UploadPhoto::class`.
- Use mount parameters only when the lookup confirms the `Livewire::test(Component::class, [...])` form for the target.
- Use direct `set()` calls for simple public properties; use array `set([...])` when setting multiple public properties together is confirmed.
- Use `call()` after state setup for behavior that occurs inside a public component method.
- Use `assertViewHas()` when the test needs to inspect data passed to the view; use `assertSee()` when checking rendered text.
- Use `assertHasErrors()` for validation failures and include specific rule assertions only when the lookup confirms the array shape.
- Use upload fakes and storage fakes for file upload tests; do not replace them with browser-style upload testing unless docs confirm that approach.
- Use event, redirect, forbidden, and JavaScript assertions only for side effects that the component action actually triggers in the documented flow.

## Confirmed Core Patterns
- Livewire component tests use `Livewire::test(...)` from `Livewire\Livewire` in the retrieved docs.
- Documented initialization examples include `Livewire::test('post.create')` and `Livewire::test(UpdatePost::class, ['post' => $post])`.
- Documented PHPUnit examples import `Tests\TestCase`, use `Livewire::test(...)`, chain `set()` and `call()`, and assert database state outside the Livewire chain.
- Documented interaction helpers include single-property `set('property', $value)`, array `set([...])`, `toggle('booleanProperty')`, `call('methodName')`, parameterized `call('methodName', $param1, $param2)`, `refresh()`, and `dispatch('eventName', ...)`.
- Documented rendered-output and view-data assertions include `assertSee()` and `assertViewHas()`, including `assertViewHas('posts', function ($posts) { ... })` and `assertViewHas('postCount', 3)`.
- Documented validation assertions include `assertHasErrors('title')` and `assertHasErrors(['title' => ['min:3']])`.
- Documented upload tests use `Storage::fake()`, `UploadedFile::fake()->image()`, `Livewire::test(...)->set(...)->call(...)`, and `Storage::disk(...)->assertExists(...)`.
- Documented event tests use `assertDispatched('post-created')` and a closure shape like `assertDispatched('notify', function ($event, $params) { ... })`.
- Documented side-effect assertions include `assertForbidden()`, `assertRedirect(url)`, `assertJs(code)`, and `assertNoJs()`.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Testing topic.
- The answer uses only APIs, assertions, helpers, namespaces, examples, and side-effect claims confirmed by the current Context7 result.
- Each helper, assertion, component identifier, class name, mount parameter, action parameter, callback parameter, and fake upload or storage helper is traceable to the retrieved Livewire 4.x docs.
- Unconfirmed helpers are not inferred from older Livewire versions, Laravel HTTP tests, Pest, PHPUnit, browser tests, package source code, or memory.
- If the user asks for a Testing topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.