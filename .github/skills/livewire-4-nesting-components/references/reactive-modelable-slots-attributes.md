# Reactive Props, Modelable Data, Slots, And Attributes

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 nesting topic.

## Reactive Props
- Props are not reactive by default.
- Livewire's documented reason is that every component is independent: a parent update sends only the parent's state to the server to re-render, not the child component's state.
- This behavior is intended to keep the amount of data sent between server and client minimal.
- Add `#[Reactive]` from `Livewire\Attributes\Reactive` to a child property when that child prop must update after the parent passes a new value.
- The docs warn to understand the performance implications of `#[Reactive]` and only add it when it makes sense for the scenario.
- If child components are created primarily to isolate updates and then kept in sync with `#[Reactive]`, the docs recommend considering islands instead.

## Modelable Child Data
- `wire:model` can be used directly on a child component through Livewire's Modelable feature.
- The docs describe this as common when extracting an input element into a dedicated Livewire component while still accessing its state in the parent.
- Add `#[Modelable]` from `Livewire\Attributes\Modelable` to the child property that should receive the parent's `wire:model` binding.
- The parent can bind with syntax such as `<livewire:todo-input wire:model="todo" />`.
- The child can bind its internal input to the modelable property, such as `<input type="text" wire:model="value">`.
- The docs state that Livewire currently supports a single `#[Modelable]` attribute, so only the first one will be bound.

## Slots
- Slots pass Blade content from a parent component into a child component.
- A child renders default slot content with the `$slot` variable.
- Named slots use `<livewire:slot name="actions">` in the parent.
- The child can access a named slot through `$slots['actions']`.
- The child can check whether a named slot was provided with `$slots->has('actions')`.
- Slots are evaluated in the context of the parent component.
- Properties and methods referenced inside the slot belong to the parent, not the child.

## Forwarding HTML Attributes
- Livewire components support forwarding HTML attributes from a parent to a child using the `$attributes` variable.
- A parent can pass normal HTML attributes such as `class`, for example `<livewire:comment :$comment class="border-b" />`.
- The child can apply forwarded attributes with `$attributes`, including documented syntax such as `<div {{ $attributes->class('bg-white rounded-md') }}>`.
- Attributes that match public property names are automatically passed as props and excluded from `$attributes`.
- Remaining attributes such as `class`, `id`, or `data-*` are available through `$attributes`.