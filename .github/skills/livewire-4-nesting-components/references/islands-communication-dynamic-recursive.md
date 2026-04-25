# Islands, Communication, Dynamic, And Recursive Children

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 nesting topic.

## Islands Versus Nested Components
- Nested components and islands both isolate updates to specific regions, but the docs say they serve different purposes.
- Use islands for performance isolation without the overhead of a separate component file, props, or event communication.
- `@island` creates an isolated region inside a component.
- `@island(lazy: true)` defers expensive content until after the initial page load.
- `@island(name: 'stats')` and `@island(name: 'chart')` document multiple independent UI regions in one component.
- Islands share the parent component's lifecycle, state, and methods.
- Use nested components when you need reusable, self-contained functionality.
- Use nested components when the child needs separate lifecycle hooks such as `mount()` or `updated()`.
- Use nested components when the child needs encapsulated state and logic, true independence across parent updates, or component-library boundaries.
- The docs quick guide maps reusable components, separate lifecycle methods, and complex isolated state to nested components.
- The docs quick guide maps performance optimization, deferred expensive content, and one-place usage to islands.

## Child-to-parent Events
- Parent-child communication can use Livewire's event system.
- The parent can listen with `#[On('remove-todo')]` from `Livewire\Attributes\On` on the parent action.
- The child can dispatch from PHP with `$this->dispatch('remove-todo', todoId: $this->todo->id)`.
- In the documented remove example, server-side child dispatch takes two network requests: one for the child action that dispatches the event and one after the client-side event is intercepted by the parent.
- The docs recommend dispatching client-side when possible to avoid the first request.
- Client-side dispatch from a child template can use `wire:click="$dispatch('remove-todo', { todoId: {{ $todo->id }} })"`.
- If child components primarily trigger parent updates through events, the docs recommend considering islands because islands share component context and can call component methods directly.

## Direct Parent Access
- Livewire provides a magic `$parent` variable to the child Blade template.
- `$parent` can access parent actions and properties directly from the child template.
- The docs show direct parent action syntax such as `wire:click="$parent.remove({{ $todo->id }})"`.
- The docs describe event communication as an indirection that may or may not be desirable depending on the scenario.

## Dynamic Child Components
- Use `<livewire:dynamic-component :is="$current" />` to choose a child component at runtime.
- The documented multi-step form example uses `<livewire:dynamic-component :is="$current" :wire:key="$current" />`.
- The alternative dynamic syntax is `<livewire:is :component="$current" :wire:key="$current" />`.
- The docs warn not to forget a unique key for each dynamic child component.
- Although Livewire automatically generates a key for dynamic component tags, that same key will apply to all child components, so later renders will be skipped.

## Recursive Components
- Livewire components may be nested recursively, meaning a parent component renders itself as its child.
- The documented recursive example renders `survey-question` children from `$this->subQuestions`.
- Recursive child components still use unique keys, such as `:wire:key="$subQuestion->id"`.
- The docs warn that standard recursion rules apply and the template must include logic that prevents infinite recursion.