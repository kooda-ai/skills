---
name: livewire-4-nesting-components
description: 'Use when: working with Livewire 4 Nesting Components, nested components, parent-child components, passing props, static props, boolean props, shortened attribute syntax, wire:key, forced child re-rendering, #[Reactive], #[Modelable], slots, named slots, $slot, $slots, $attributes, islands vs nested components, child events, #[On], $dispatch, $parent, dynamic components, and recursive components. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 nested component task, parent-child props, keys, reactive/modelable props, slots, islands, events, dynamic child concern'
---

# Livewire 4 Nesting Components

## Purpose
Use this skill to create, review, or explain Livewire 4 nested components, component islands, and parent-child communication using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 nesting topic.
2. Do not add component syntax, prop behavior, key behavior, attributes, directives, event APIs, lifecycle claims, island guidance, or examples unless they appear in the retrieved documentation.
3. If a requested nesting detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup using the query map or leave the topic out.
4. Keep examples close to documented snippets and preserve documented tag names, attribute names, directive names, class names, attribute namespaces, method names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controllers, Alpine habits, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Nested rendering, component extraction decisions, props, keys, and forced child re-rendering: [rendering-props-keys.md](./references/rendering-props-keys.md)
- Reactive props, modelable child data, slots, named slots, and forwarded attributes: [reactive-modelable-slots-attributes.md](./references/reactive-modelable-slots-attributes.md)
- Islands, child-to-parent communication, direct parent access, dynamic child components, and recursive components: [islands-communication-dynamic-recursive.md](./references/islands-communication-dynamic-recursive.md)

## Workflow
1. Identify the nesting concern: extraction decision, nested rendering, prop passing, loop keys, forced child re-initialization, reactive props, modelable child state, slots, forwarded attributes, islands, child-to-parent communication, direct parent access, dynamic child components, recursive components, or performance tradeoff.
2. Run a narrow Context7 query for the exact Livewire 4 nesting topic before producing code or review findings.
3. Load the relevant reference file from the map above as a checklist only after the current Context7 result confirms the topic.
4. For extraction decisions, confirm whether the content needs Livewire dynamic behavior or direct performance benefit; otherwise prefer the documented Blade component recommendation.
5. For child rendering, use documented `<livewire:... />` syntax and account for the documented independence of nested components after the initial parent render.
6. For props, choose documented dynamic, static, boolean, or shortened attribute syntax, and receive props through `mount()` or matching public properties when confirmed.
7. For children rendered in loops, require a unique `:wire:key` and treat missing keys as a correctness issue.
8. For child updates, choose between non-reactive default props, `#[Reactive]`, `#[Modelable]`, changing `wire:key`, or islands according to the documented scenario.
9. For child content, use documented default slots, named slots, `$slots->has(...)`, and `$attributes` forwarding only when the lookup confirms the needed pattern.
10. For parent-child communication, choose documented PHP dispatch with `#[On]`, client-side `$dispatch`, or `$parent` direct access, and include the documented request-count/performance note when relevant.
11. For dynamic or recursive children, preserve documented dynamic component tags, required keys, and recursion termination warning.
12. Finish by checking that every tag, prop syntax, directive, attribute, event helper, method, namespace, island directive, and caveat is traceable to the current Context7 result and the loaded reference file.

## Decision Points
- Use a Blade component when the extracted content does not need to be live.
- Use a nested Livewire component when the child needs reusable, self-contained behavior, separate lifecycle hooks, encapsulated state and logic, true independence, or component-library boundaries.
- Use an island when the docs-confirmed goal is isolated re-rendering inside one component without separate child component files, props, events, or child communication.
- Keep props non-reactive by default; use `#[Reactive]` only when parent changes must update the child and the performance implications are acceptable.
- Use `#[Modelable]` when a parent should bind `wire:model` directly to a child component property.
- Change a child key only when the documented goal is to destroy and re-initialize that child component.
- Use direct `$parent` access only when the parent-child relationship is clear and the documented direct-call syntax fits the task.

## Confirmed Core Patterns
- A parent nests a Livewire child by placing the child tag in the parent Blade view, such as `<livewire:todos />`.
- On the initial page render, the parent renders the nested component in place; on a later parent network request, the child skips rendering because it is its own independent component on the page.
- Dynamic props use a leading colon, static string props omit the colon, boolean true props may be passed by including only the key, and matching variable/prop names may use shortened syntax such as `:$todos`.
- Child props can be received through `mount($todos)` or by omitting `mount()` when the public property and parameter names match.
- Child components rendered in loops require unique keys; Livewire relies heavily on keys and will behave incorrectly without them.
- Changing a child component key forces Livewire to create a new child instance, re-initialize it from scratch, and discard the old instance.
- Props are not reactive by default; `#[Reactive]` on a child property opts that prop into updates when the parent passes a new value.
- `#[Modelable]` on a child property lets the parent use `wire:model` on the child component; the docs state only one `#[Modelable]` attribute is currently supported and only the first one will be bound.
- Slots pass Blade content from the parent to the child; named slots use `<livewire:slot name="actions">`, `$slots['actions']`, and `$slots->has('actions')`.
- Slots are evaluated in the parent component context, so properties and methods referenced inside the slot belong to the parent.
- Livewire components can forward remaining HTML attributes with `$attributes`; attributes matching public property names are passed as props and excluded from `$attributes`.
- Parent-child communication can use `#[On]` plus `$this->dispatch(...)`, client-side `$dispatch(...)`, or direct `$parent` access from the child template.
- Dynamic children use `<livewire:dynamic-component :is="$current" :wire:key="$current" />` or `<livewire:is :component="$current" :wire:key="$current" />`.
- Recursive components are supported, but templates must include logic that prevents infinite recursion.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Nesting Components topic.
- Reference files were used only after the fresh lookup confirmed the relevant topic.
- The answer does not include APIs, syntax, event behavior, island behavior, lifecycle claims, or warnings absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 tag names, directive names, attribute names, event names, method signatures, namespace imports, and key patterns.
- Loop-rendered children have unique keys, dynamic children have explicit keys, and forced re-render guidance uses changed keys only for documented re-initialization behavior.
- Parent-child communication guidance includes documented tradeoffs only: server dispatch, client-side dispatch to avoid the first request when possible, `$parent` for direct access, and islands when child event communication is unnecessary.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.