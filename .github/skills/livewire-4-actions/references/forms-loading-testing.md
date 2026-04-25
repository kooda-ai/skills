# Forms Loading Testing

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 form action, confirmation, loading, or testing topic.

## Form Submission
- `wire:submit` is added to a `<form>` element to intercept the form submission and call a Livewire component method.
- `wire:submit` internally calls `event.preventDefault()` without needing the `.prevent` modifier.
- By default, while Livewire sends a form submission to the server, it disables form submit buttons and marks all form inputs as `readonly`.
- The documented form pattern combines `wire:submit="save"`, inputs using `wire:model`, and a submit button.

## Confirmation
- `wire:confirm="message"` can be added alongside an action such as `wire:click` or `wire:submit`.
- `wire:confirm` uses the browser confirmation alert.
- If the user presses escape or Cancel, the action is not performed.
- If the user presses OK, the action is completed.
- `wire:confirm.prompt="message|expected-input"` prompts the user for input and only confirms if the input matches the expected string case-sensitively.

## Loading Indicators
- `wire:loading` hides an element by default with `display: none` and shows it when a request is sent to the server.
- `wire:loading.remove` shows an element by default and hides it during requests.
- `wire:loading.class="opacity-50"` adds a CSS class during loading.
- `wire:loading.class.remove="bg-blue-500"` removes a CSS class during loading.
- `wire:loading.attr="disabled"` toggles an attribute during loading.
- Display modifiers documented for `wire:loading` include `.inline-flex`, `.inline`, `.block`, `.table`, `.flex`, and `.grid`.
- Delay modifiers documented for `wire:loading` include `.delay`, `.delay.shortest`, `.delay.shorter`, `.delay.short`, `.delay.long`, `.delay.longer`, and `.delay.longest`.

## Loading Targets
- By default, `wire:loading` is triggered whenever a component makes a request to the server.
- `wire:target="remove"` scopes a loading indicator to a specific action.
- `wire:target="save, remove"` scopes a loading indicator to multiple actions.
- `wire:target="remove({{ $post->id }})"` scopes a loading indicator to a specific action and parameter set.
- `wire:target="username"` scopes a loading indicator to a property update.
- `wire:target.except="download"` shows a loading indicator for every Livewire update request except the named action or property.

## `data-loading`
- Livewire automatically adds a `data-loading` attribute to any element that triggers a network request.
- The docs describe `data-loading` selectors as a v4 loading-state approach that can be simpler and more flexible than `wire:loading` for styling.
- Tailwind examples include `data-loading:opacity-50`, `data-loading:pointer-events-none`, `has-data-loading:opacity-50`, `in-data-loading:hidden`, and `not-data-loading:hidden`.
- Standard CSS can target `[data-loading]` and element-specific selectors such as `button[data-loading]`.

## Testing Actions
- Use `Livewire::test('component.name')->call('save')` to trigger a component action in tests.
- `call('remove', $postId)` calls an action with parameters.
- `set('title', '...')` sets a property before calling an action.
- `toggle('sortAsc')` toggles a boolean property.
- `refresh()` triggers a component re-render.
- `dispatch('post-created')` dispatches an event from the component.
- `Livewire::actingAs($user)` sets the authenticated user for a test.
- `assertHasErrors('title')` and `assertHasErrors(['title' => ['required', 'min:6']])` assert validation errors.
- `assertForbidden()` and `assertUnauthorized()` assert authorization failures.
- `assertRedirect('/posts')` and `assertRedirectToRoute('posts.index')` assert redirects.
- `assertDispatched('post-created')` and `assertNotDispatched('post-created')` assert events.
- `assertJs("alert('...')")` asserts that JavaScript was evaluated by `$this->js()`.
- `assertNoJs()` asserts that no JavaScript was evaluated.
- The docs recommend Pest for Livewire testing and say PHPUnit can use the same testing utilities.
- `Livewire::visit()` is documented for browser tests that interact with components in a real browser.