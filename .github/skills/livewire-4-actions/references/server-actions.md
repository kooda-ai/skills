# Server Actions

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 Actions topic.

## Basic Actions
- Actions are methods on a component that can be triggered by frontend interactions.
- `wire:submit="save"` on a `<form>` calls the `save()` action on the server.
- `wire:click="download"` on an element calls the `download()` action when clicked.
- `wire:click="delete({{ $post->id }})"` passes a Blade value into the action.
- `wire:submit="methodName(param1, param2)"` and `wire:click="methodName(param1, param2)"` are documented action-call syntaxes.

## Parameters And Authorization
- Action parameters should be treated like HTTP request input and should not be trusted.
- The docs require authorization of ownership before updating or deleting database records based on action parameters.
- A malicious user can call a public action directly from the JavaScript console with arbitrary parameters.
- UI checks such as hiding a button do not replace server-side authorization.
- Dangerous helper methods that are not intended to be callable from the client should be `protected` or `private`.

## Model Parameters And Dependency Injection
- Eloquent models may be resolved by a corresponding model ID when an action parameter is type-hinted with the model class.
- Laravel dependency injection is supported in action signatures by type-hinting dependencies.
- In the documented dependency injection example, the container-resolved dependency is received before the provided action parameter.

## Event Listener Directives
The docs list these event listener examples:

- `wire:click`: triggered when an element is clicked.
- `wire:submit`: triggered when a form is submitted.
- `wire:keydown`: triggered when a key is pressed down.
- `wire:keyup`: triggered when a key is released.
- `wire:mouseenter`: triggered when the mouse enters an element.
- `wire:*`: whatever follows `wire:` is used as the listener event name.

The docs show custom browser events such as `wire:transitionend`, third-party events such as `wire:trix-change`, and dispatched custom events such as `wire:custom-event`.

## Key Modifiers
The docs list these key modifiers:

- `.shift`, `.enter`, `.space`, `.ctrl`, `.cmd`, `.meta`, `.alt`, `.up`, `.down`, `.left`, `.right`, `.escape`, `.tab`, `.caps-lock`, `.equal`, `.period`, and `.slash`.

## Event Handler Modifiers
The docs list these event handler modifiers:

- `.prevent`: equivalent of calling `.preventDefault()`.
- `.stop`: equivalent of calling `.stopPropagation()`.
- `.window`: listens for events on the window object.
- `.outside`: only listens for clicks outside the element.
- `.document`: listens for events on the document object.
- `.once`: ensures the listener is only called once.
- `.debounce`: debounces the handler by 250ms by default.
- `.debounce.100ms`: debounces the handler for a specific amount of time.
- `.throttle`: throttles the handler to being called every 250ms at minimum.
- `.throttle.100ms`: throttles the handler at a custom duration.
- `.self`: only calls the listener if the event originated on this element.
- `.camel`: converts an event name to camel case.
- `.dot`: converts an event name to dot notation.
- `.passive`: keeps a touch listener from blocking scroll performance.
- `.capture`: listens in the capturing phase.

## Event Object And Custom Events
- `$event` can be used inside event listeners such as `wire:keydown.enter="search($event.target.value)"`.
- `$event.target` is documented for referencing the element that triggered the event.
- `.window` is documented for listening to a custom event that bubbles to the window.
- The docs note that `wire:` uses Alpine's `x-on` directive under the hood.

## Refreshing And Preserving Scroll
- `$refresh` triggers a server roundtrip and re-renders the component without calling a custom method.
- Pending data updates, such as `wire:model` bindings, are applied on the server when `$refresh` runs.
- `x-on:click="$wire.$refresh()"` triggers the same refresh from Alpine.
- `.preserve-scroll` maintains the current scroll position during updates, such as `wire:click.preserve-scroll="loadMore"`.

## Renderless Actions
- `#[Renderless]` from `Livewire\Attributes\Renderless` skips the render portion of Livewire's lifecycle after an action.
- `$this->skipRender()` can be called inside an action to conditionally skip rendering.
- `.renderless` can be used directly on an element, such as `wire:click.renderless="trackClick"`.
- The docs frame renderless actions for side effects that do not change the rendered Blade template.

## Async Actions
- Livewire serializes actions within the same component by default; later actions wait for an in-flight action.
- `wire:click.async="logActivity"` makes an action run in parallel.
- `#[Async]` from `Livewire\Attributes\Async` marks an action as async regardless of where it is called.
- Documented async use cases include analytics, logging, background operations, external services, and JavaScript-only results.
- The docs warn never to use async actions for component state mutations reflected in the UI, because parallel requests can cause race conditions and lost updates.