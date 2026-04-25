# Context7 Query Prompts

Use these query shapes to refresh the source context before answering Livewire 4 Nesting Components questions. Always keep the query scoped to `/websites/livewire_laravel_4_x`.

## Rendering, Props, And Keys
```text
Livewire 4 nesting components documentation: nested components, including child components in parent Blade views, initial parent render, independent child rendering on later parent requests, when to use Blade components instead, passing dynamic props, static props, boolean props, shortened attribute syntax, receiving props with mount or matching public properties, rendering children in loops, required unique wire:key, and forcing a child component to re-render by changing keys. Return documented syntax, examples, warnings, and caveats only.
```

## Reactive Props And Modelable Child Data
```text
Livewire 4 nesting components documentation: props not reactive by default, independent component behavior, #[Reactive] child props, performance implications, islands as an alternative to reactive props, #[Modelable] child properties, parent wire:model on child components, modelable input examples, and the single modelable property limitation. Return documented syntax, namespaces, examples, warnings, and caveats only.
```

## Slots And Forwarded Attributes
```text
Livewire 4 nesting components documentation: default slots, named slots, <livewire:slot>, $slot, $slots, $slots['actions'], $slots->has(), slot parent-context evaluation, forwarding HTML attributes with $attributes, $attributes->class(), public-property attributes excluded from $attributes, and remaining class id data-* attributes. Return documented syntax, examples, warnings, and caveats only.
```

## Islands, Communication, Dynamic, And Recursive Children
```text
Livewire 4 nesting components documentation: islands versus nested components, @island, lazy islands, named islands, when to use islands, when to use nested components, quick decision guide, child-to-parent events with #[On] and dispatch, client-side $dispatch performance, direct $parent access, dynamic components with <livewire:dynamic-component> and <livewire:is>, dynamic component keys, recursive components, and infinite recursion warning. Return documented syntax, examples, warnings, and caveats only.
```