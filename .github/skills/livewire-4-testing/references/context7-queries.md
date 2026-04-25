# Context7 Queries

Use `/websites/livewire_laravel_4_x` for all Livewire 4 Testing source checks.

## Baseline Queries
- Core component testing: `Livewire 4 testing documentation: component testing overview, Livewire::test, PHPUnit examples, Pest examples, assertions, set, call, toggle, refresh, dispatch, assertSee, assertViewHas, mounting components with parameters`.
- Validation and uploads: `Livewire 4 testing documentation for forms, validation, validation errors, Livewire\\Form form objects, file uploads, temporary uploaded files, Storage::fake, UploadedFile::fake, WithFileUploads, assertHasErrors`.
- Side effects: `Livewire 4 testing documentation for events, dispatch, assertDispatched parameters, redirects, authorization assertForbidden, JavaScript assertions assertJs assertNoJs, query string URL attribute, action parameters`.

## Lookup Rules
1. Query the exact topic before writing code or review findings.
2. If a broad query omits a helper or assertion, do not use it yet; run a narrower query for that helper.
3. Treat snippets from non-testing pages as supporting context only. Do not turn them into testing guidance unless the Testing docs confirm the test shape.
4. Preserve documented names exactly: `Livewire::test`, `set`, `toggle`, `call`, `refresh`, `dispatch`, `assertSee`, `assertViewHas`, `assertHasErrors`, `assertDispatched`, `assertRedirect`, `assertForbidden`, `assertJs`, and `assertNoJs`.
5. Leave out helpers that the current Context7 result does not confirm.