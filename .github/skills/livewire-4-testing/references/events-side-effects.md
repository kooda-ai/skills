# Events And Side Effects

## Event Assertions
- The retrieved docs confirm `assertDispatched('post-created')` after calling an action such as `save`.
- The retrieved docs confirm parameter checks with a callback shape: `assertDispatched('notify', function ($event, $params) { ... })`.
- In the documented callback, `$params` can be inspected for values such as `message`.

## Redirects, Authorization, And JavaScript
- `assertRedirect(url)` asserts that the component performed a redirect to the specified URL or route.
- `assertForbidden()` asserts that the last action was unauthorized.
- `assertJs(code)` asserts that the component evaluated specific JavaScript code.
- `assertNoJs()` asserts that no JavaScript was evaluated by the component.

## URL Attribute Context
- The retrieved URL docs confirm the `#[Url]` attribute and parameters such as `as`, `history`, `keep`, `except`, and `nullable`.
- The retrieved URL docs confirm that `#[Url]` can sync a public property with the browser URL.
- The current Testing excerpts did not confirm a testing helper or assertion for URL query-string state. Run a narrower Context7 lookup before writing URL-specific tests.

## Helpers Not Confirmed In The Retrieved Testing Excerpts
Do not use these unless a fresh Context7 lookup confirms them for Livewire 4 Testing:

- `assertDontSee()`
- `assertSet()`
- `assertHasNoErrors()`
- `assertNotDispatched()`
- `assertDispatchedTo()`
- `assertOk()`
- `assertStatus()`
- `actingAs()` or authentication-specific setup inside `Livewire::test()` examples
- Full-page component testing helpers beyond the confirmed `Livewire::test(...)` initialization shapes
- Pagination-specific testing helpers
- Computed-property-specific testing helpers
- Lifecycle-hook-specific testing helpers