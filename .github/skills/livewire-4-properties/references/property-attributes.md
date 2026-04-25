# Property Attributes

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 property attribute topic.

## `#[Locked]`
- Import `Livewire\Attributes\Locked`.
- Add `#[Locked]` above a public property to prevent it from being modified on the client side.
- The docs show locking an ID property that is initialized in `mount()` and later used by an action.
- Public Eloquent model properties are automatically locked by Livewire.

## `#[Url]`
- Import `Livewire\Attributes\Url`.
- Add `#[Url]` above a public property to synchronize it with the browser query string.
- The documented options include `as`, `history`, `keep`, `except`, and `nullable`.
- `as` uses a custom query parameter name instead of the property name.
- `history: true` pushes URL changes to the browser history.
- `keep: true` keeps the query parameter when navigating away from the current page.
- `except` excludes matching values from being reflected in the URL.
- Confirm nullable behavior with the current Context7 result before describing it in final guidance.

## `#[Session]`
- Confirm the current `#[Session]` documentation before adding syntax or options.
- The docs describe `#[Session]` as an alternative for simple user-specific values that should persist across page refreshes, do not need to be shareable via URL, and are not computationally expensive to store.

## `#[Computed]`
- Import `Livewire\Attributes\Computed`.
- Add `#[Computed]` above a method to expose it as a computed property.
- Computed properties can be accessed inside component methods and inside templates.
- In templates, computed properties must be accessed through `$this`, such as `$this->user`.
- The docs state that computed properties are not supported on `Livewire\Form` objects.
- Computed properties are memoized for the duration of a single component request.
- Use `unset($this->propertyName)` to clear a computed property's memo after underlying state changes.
- The docs document `#[Computed(persist: true)]`, `seconds`, `#[Computed(cache: true)]`, and custom `key` for caching behavior; confirm exact options before use.

## `#[Reactive]`
- Import `Livewire\Attributes\Reactive`.
- Props passed to child components are not reactive by default because nested components are independent.
- Add `#[Reactive]` above a child property when parent changes should update that child prop.
- The docs warn to understand performance implications and add `#[Reactive]` only when it makes sense for the scenario.

## `#[Modelable]`
- Import `Livewire\Attributes\Modelable`.
- Add `#[Modelable]` above a child component property so a parent can bind to the child component with `wire:model`.
- The docs show a child `$value` property marked `#[Modelable]` and a parent using `<livewire:todo-input wire:model="todo" />`.
- The docs state that Livewire currently supports a single `#[Modelable]` attribute, and only the first one will be bound.

## `#[Validate]`
- Import `Livewire\Attributes\Validate`.
- Add `#[Validate(...)]` above a property to attach validation rules.
- Use the validation docs for supported rule syntax, messages, attributes, localization, real-time validation behavior, and `rules()` fallbacks.