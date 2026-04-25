# Actions And Lifecycle

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 actions, JavaScript action, or lifecycle hook topic.

## Actions
- Actions are methods on a component that can be triggered by frontend interactions such as clicks and form submissions.
- `wire:submit="save"` intercepts form submission and calls the `save()` action on the server.
- `wire:click="delete({{ $post->id }})"` passes a Blade value into an action parameter.
- Action parameters are user input; the docs say to authorize ownership before updating or deleting database records.
- Eloquent models can be resolved by type-hinting an action parameter with a model class and passing the model ID.
- Laravel dependency injection is supported by type-hinting dependencies in an action signature.

## Event Listener Directives
The docs list these event listener examples:

- `wire:click`: triggered when an element is clicked.
- `wire:submit`: triggered when a form is submitted.
- `wire:keydown`: triggered when a key is pressed down.
- `wire:keyup`: triggered when a key is released.
- `wire:mouseenter`: triggered when the mouse enters an element.
- `wire:*`: whatever follows `wire:` is used as the listener event name.

The docs list these key modifiers: `.shift`, `.enter`, `.space`, `.ctrl`, `.cmd`, `.meta`, `.alt`, `.up`, `.down`, `.left`, `.right`, `.escape`, `.tab`, `.caps-lock`, `.equal`, `.period`, and `.slash`.

The docs list these event handler modifiers: `.prevent`, `.stop`, `.window`, `.outside`, `.document`, `.once`, `.debounce`, `.debounce.100ms`, `.throttle`, `.throttle.100ms`, `.self`, `.camel`, `.dot`, `.passive`, and `.capture`.

## Built-In Action Patterns
- `$refresh` triggers a server roundtrip and re-renders the component without calling a custom method.
- `x-on:click="$wire.$refresh()"` triggers refresh from Alpine.
- `wire:confirm="..."` shows a confirmation dialog before triggering the action; the user can press OK, Cancel, or Escape.
- The `.preserve-scroll` modifier maintains scroll position during updates, such as `wire:click.preserve-scroll="loadMore"`.
- The `$event` value can be used in an event listener, such as `wire:keydown.enter="search($event.target.value)"`.
- During a `wire:submit` form action, Livewire automatically disables submit buttons and marks inputs inside the form as read-only while the request is processing.

## Calling Actions From Alpine
- Alpine can call PHP actions with `$wire.save()`.
- Parameters passed to `$wire.actionName(...)` are passed to the PHP method.
- `$wire` actions return a promise while the network request is processing, and the promise resolves with the backend action return value.
- The docs say that for actions primarily consumed by JavaScript, consider `#[Json]`, which returns data via promise resolution or rejection, handles validation errors with promise rejection, and skips re-rendering.

## JavaScript Actions
- JavaScript actions run entirely on the client side without a server request.
- Define a JavaScript action with `$js()` inside a component `<script>` tag.
- Call a JavaScript action from Blade with `wire:click="$js.bookmark"` or from Alpine with `$wire.$js.bookmark()`.
- A PHP action can call a JavaScript action with `$this->js('onPostSaved')`.
- For class-based components, the docs say script tags must be wrapped with `@script` and `@endscript` so JavaScript is scoped to the component.

## Magic Actions
The docs list these magic actions:

- `$parent`: access parent component properties and actions from a child template.
- `$set`: set a component property from a template, such as `$set('query', '')`.
- `$refresh`: re-render the component.
- `$toggle`: toggle a boolean property.
- `$dispatch`: dispatch a Livewire event directly in the browser.
- `$event`: access the JavaScript event object in an event listener.

## Skipping Renders
- Use `#[Renderless]` from `Livewire\Attributes\Renderless` above an action when invoking it should skip the render portion of Livewire's lifecycle.
- Call `$this->skipRender()` inside an action to conditionally skip rendering.
- Use `.renderless` directly on an element, such as `wire:click.renderless="incrementViewCount"`.

## Async Actions
- By default, Livewire serializes actions within the same component so later actions wait for an in-flight action.
- `wire:click.async="logActivity"` runs an action in parallel.
- `#[Async]` from `Livewire\Attributes\Async` marks a method as async regardless of where it is called.
- The docs say async actions are useful for fire-and-forget operations such as analytics, logging, background operations, and JavaScript-only results.
- The docs warn never to use async actions for state mutations reflected in the UI because simultaneous requests can cause race conditions and lost updates.

## Action Security
- Every public method in a Livewire component is callable from the client, even if no `wire:click` references it.
- Always authorize action parameters, because they are arbitrary user input.
- Always authorize server-side; hiding a button in the UI does not prevent a user from calling the public action from DevTools.
- Mark dangerous helper methods as `protected` or `private` so they cannot be called from the client side.

## Lifecycle Hooks
The docs list these component lifecycle hooks:

- `mount()`: called when a component is created.
- `hydrate()`: called when a component is re-hydrated at the beginning of a subsequent request.
- `boot()`: called at the beginning of every request, initial and subsequent.
- `updating()`: called before updating a component property.
- `updated()`: called after updating a property.
- `rendering()`: called before the component view is rendered.
- `rendered()`: called after the component view is rendered.
- `dehydrate()`: called at the end of every component request.
- `exception($e, $stopPropagation)`: called when an exception is thrown.

## Lifecycle Details
- Livewire components do not use `__construct()` for initialization; use `mount()` to accept parameters and initialize state once.
- Lifecycle hook methods support Laravel dependency injection through type-hinted parameters.
- Use `boot()` for setup code that must run every request, such as re-initializing protected properties that are not persisted.
- `updating($property, $value)` runs before a property is updated; `updated($property)` runs after.
- Property-specific hooks such as `updatedUsername()` and the corresponding `updating` form are documented.
- Array property hooks receive an additional `$key` argument; when the array itself is updated instead of a specific key, `$key` is null.
- `hydrate()` and `dehydrate()` can transform component state at the beginning and end of requests, though the docs recommend Wireables or Synthesizers for custom types.
- `rendering($view, $data)` runs before the view is rendered; `rendered($view, $html)` runs after rendering.
- `exception($e, $stopPropagation)` can inspect the exception and call `$stopPropagation()` to catch the issue.
- Traits can define prefixed hook methods using the camelCased trait name, such as `mountHasPostForm()`, `hydrateHasPostForm()`, `bootHasPostForm()`, `updatingHasPostForm()`, `updatedHasPostForm()`, `renderingHasPostForm()`, `renderedHasPostForm()`, and `dehydrateHasPostForm()`.
- Form objects support property update hooks such as `updating`, `updated`, `updatingTitle`, `updatedTitle`, `updatingTags($value, $key)`, and `updatedTags($value, $key)`.