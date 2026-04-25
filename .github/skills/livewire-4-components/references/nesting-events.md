# Nesting And Events

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 nesting or event topic.

## Nesting Components
- Nest a component by including its Livewire tag in a parent component's Blade view, such as `<livewire:todos />`.
- On initial render, the parent renders the nested component in place.
- On subsequent parent network requests, the nested component skips rendering because it is its own independent component on the page.
- The docs recommend using a Blade component instead of a nested Livewire component when the extracted content does not need to be live.
- The docs recommend considering islands when the goal is isolated re-rendering without separate child components, props, events, or child communication.

## Passing Props To Children
- Pass dynamic props with `:todos="$this->todos"` or `:$todos` when the variable and prop names match.
- Pass static string props without the colon, such as `label="Todo Count:"`.
- Pass boolean true values by including only the key, such as `inline`.
- Receive child props through `mount($todos)`, or omit `mount()` when the property and parameter names match.

## Keys And Child Rendering
- When rendering child components in a loop, include a unique key for each iteration.
- The docs show `:wire:key="$todo->id"` on a nested component.
- The docs warn that keys are not optional for Livewire child components in loops and that Livewire can behave incorrectly without them.
- To force a child component to re-render, change its key; the docs show generating a dynamic key from the content of the passed data.

## Reactive And Modelable Props
- Props are not reactive by default because every component is independent.
- Add `#[Reactive]` from `Livewire\Attributes\Reactive` to a child property when parent changes should update that child prop.
- The docs warn to understand the performance implications and add `#[Reactive]` only when it makes sense for the scenario.
- Add `#[Modelable]` from `Livewire\Attributes\Modelable` to a child property so a parent can use `wire:model` directly on the child component.
- The docs state that Livewire currently supports a single `#[Modelable]` attribute, and only the first one will be bound.

## Slots And Attributes
- Default slots pass Blade content from the parent into the child; the child renders it with `$slot`.
- Named slots use `<livewire:slot name="actions">...</livewire:slot>` and are accessed in the child with `$slots['actions']`.
- `$slots->has('actions')` checks whether a named slot was provided.
- Slots are evaluated in the parent component context, so properties and methods referenced inside the slot belong to the parent.
- Livewire components support forwarding HTML attributes with `$attributes`.
- Attributes matching public property names are passed as props and excluded from `$attributes`; remaining attributes such as `class`, `id`, or `data-*` are available through `$attributes`.

## Islands Versus Nested Components
- The docs describe islands as useful for performance isolation, lazy or deferred expensive content, multiple independent UI regions, and regions that do not need their own lifecycle.
- `@island` creates an isolated region inside a component.
- `@island(lazy: true)` lazy-loads an island.
- `@island(name: 'stats')` names an island.
- The docs describe nested components as better for reusable self-contained functionality, separate lifecycle hooks, encapsulated state and logic, true independence, and component libraries.
- The quick decision guide in the docs maps reusable components, separate lifecycle methods, and complex isolated state to nested components; performance optimization, deferred expensive content, and one-place usage often map to islands.

## Parent-Child Communication
- Add `#[On('remove-todo')]` from `Livewire\Attributes\On` to a parent action to listen for a child-dispatched event.
- Dispatch from a component with `$this->dispatch('remove-todo', todoId: $this->todo->id)`.
- Dispatch from the browser with `$dispatch('remove-todo', { todoId: ... })` inside `wire:click`.
- The docs say to prefer dispatching client-side when possible because it avoids an extra network request.
- A child can call a parent action directly with `$parent`, such as `wire:click="$parent.remove({{ $todo->id }})"`.

## Dynamic And Recursive Children
- Render a runtime-selected child with `<livewire:dynamic-component :is="$current" />`.
- The alternative syntax is `<livewire:is :component="$current" />`.
- Dynamic children should still receive a unique key, such as `:wire:key="$current"`.
- Livewire components may be nested recursively, but the docs warn that templates must prevent infinite recursion.

## Component Events
- Dispatch an event from PHP with `$this->dispatch('post-created')`.
- Pass event data with named arguments, such as `$this->dispatch('post-created', title: $post->title)`.
- Listen with `#[On('post-created')]` above the method to call.
- Additional event data is passed to the listener action as arguments.
- Dynamic listener names can use component data, such as `#[On('post-updated.{post.id}')]`.
- Listen to a specific child component event in a Blade template with `<livewire:edit-post @saved="$refresh">`.
- Forward child event values with `$event.detail`, such as `@saved="close($event.detail.postId)"`.

## JavaScript And Alpine Events
- Inside a component script, listen with `this.$on('post-created', () => { ... })`.
- Inside a component script, dispatch with `this.$dispatch('post-created')`.
- `this.$dispatchSelf('post-created')` dispatches only to the component where the script resides and prevents bubbling.
- Global JavaScript can listen after `livewire:init` with `Livewire.on('post-created', (event) => { ... })`; the returned cleanup function unregisters the listener.
- Alpine can listen with `x-on:post-created="..."` and globally with `x-on:post-created.window="..."`.
- Alpine can dispatch with `$dispatch('post-created')` and pass data with `$dispatch('post-created', { title: 'Post Title' })`.
- Livewire events are plain browser events under the hood.

## Event Targeting And Testing
- Dispatch directly to another component with `$this->dispatch('post-created')->to(component: Dashboard::class)`.
- Dispatch to itself with `$this->dispatch('post-created')->to(self: true)` as shown in the retrieved docs.
- Dispatch events from Blade with `$dispatch('show-post-modal', { id: ... })`.
- Dispatch directly to another component from Blade with `$dispatchTo('posts', 'show-post-modal', { id: ... })`.
- Test dispatched events with `assertDispatched('post-created')`.
- Test listeners by calling `->dispatch('post-created')` in a Livewire test and asserting the result.

## Echo Events
- Livewire can listen for Laravel Echo events when Echo is installed and `window.Echo` is globally available.
- Listen with `#[On('echo:orders,OrderShipped')]`.
- Dynamic channel names can use `getListeners()` or dynamic attribute syntax such as `#[On('echo:orders.{order.id},OrderShipped')]`.
- Access the Echo payload through an `$event` parameter.
- Custom broadcast names from `broadcastAs()` must be prefixed with a dot in the listener, such as `echo:scores,.score.submitted`.
- The docs show public, private, and presence channel listener prefixes: `echo:`, `echo-private:`, and `echo-presence:`.