---
name: livewire-4-advanced-nesting-boundaries
description: 'Use when: working with Livewire 4 advanced Nesting, component boundaries, nested components, props, wire:key, forced child re-rendering, #[Reactive], #[Modelable], slots, $attributes, islands vs children, child events, dynamic components, recursive components, component organization, and nesting troubleshooting. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 nesting, component boundary, key, reactive prop, modelable prop, slot, dynamic child, or recursive component concern'
---

# Livewire 4 Advanced Nesting Boundaries

## Purpose
Use this skill to create, review, or explain Livewire 4 nested component boundaries, parent-child state flow, keys, dynamic children, recursive children, and nesting troubleshooting using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Nesting, child component, prop, key, slot, island, event, dynamic component, recursive component, or troubleshooting topic.
2. Do not add child rendering behavior, prop reactivity, key behavior, slot behavior, event behavior, island tradeoffs, dynamic component syntax, recursive caveats, or troubleshooting steps unless they appear in the retrieved documentation.
3. If a requested nesting detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the detail out.
4. Preserve documented tag names, directive names, attribute names, method names, attribute namespaces, event helpers, and example key patterns exactly.
5. Do not infer behavior from Livewire 3, Vue or React nesting patterns, Alpine habits outside the Livewire docs, package source code, or memory.

## Covered Topics
- Nested Livewire components and component independence
- Static, dynamic, boolean, and shortened prop syntax
- `wire:key` and forced child re-rendering
- `#[Reactive]` and `#[Modelable]`
- Slots, named slots, `$slot`, `$slots`, and `$attributes`
- Islands versus nested components
- Parent-child communication with events and `$parent`
- Dynamic child components
- Recursive child components
- Component organization and nesting troubleshooting

## Workflow
1. Identify the boundary concern: extraction choice, child rendering, prop passing, loop keys, forced child reset, reactive prop, modelable prop, slot content, forwarded attributes, island alternative, event communication, `$parent`, dynamic child, recursion, or component-not-found troubleshooting.
2. Run a narrow Context7 query for the exact Livewire 4 nesting topic before producing code or review findings.
3. For extraction decisions, ask whether the content needs Livewire dynamic behavior or a direct performance benefit; otherwise use the documented Blade component recommendation.
4. For nested children, use documented `<livewire:... />` tags and account for the documented child independence after initial render.
5. For props, choose documented dynamic colon syntax, static string syntax, boolean true syntax, or shortened syntax only when confirmed.
6. For child props, receive values through `mount(...)` or matching public properties only as documented.
7. For children in loops, require a unique `:wire:key` and treat missing loop keys as a correctness issue.
8. For forced child re-rendering, change the key only when the docs-confirmed goal is to create a new child instance and discard the old instance.
9. For parent updates flowing into a child, keep props non-reactive by default and use `#[Reactive]` only when the docs-confirmed task needs child props updated from parent changes.
10. For parent `wire:model` binding to a child, use `#[Modelable]` only as documented and include the documented one-modelable-property limitation when relevant.
11. For child content, use documented default slots, named slots, `$slots->has(...)`, and `$attributes` forwarding only when the lookup confirms the needed pattern.
12. For communication, choose documented `dispatch()` with `#[On]`, client-side `$dispatch`, or direct `$parent` access according to the docs-confirmed scenario.
13. For dynamic children, preserve documented `<livewire:dynamic-component :is="$current" :wire:key="$current" />` or `<livewire:is :component="$current" :wire:key="$current" />` syntax.
14. For recursive components, include termination logic and unique child keys because the docs warn against infinite recursion.
15. For troubleshooting, use only documented checks such as component file path, component name, namespace configuration, manual registration, `php artisan view:clear`, exactly one root element, syntax errors, Laravel logs, and class-name conflicts.
16. Finish by checking that every tag, prop syntax, attribute, key strategy, event helper, dynamic component syntax, recursive warning, and troubleshooting step is traceable to the current Context7 result.

## Confirmed Core Patterns
- A parent nests a Livewire child by placing the child tag in the parent Blade view, such as `<livewire:todos />`.
- On initial render, the parent renders the child in place; on later parent requests, the child skips rendering because it is an independent component on the page.
- Props can be passed as dynamic values, static strings, boolean true attributes, or shortened same-name attributes when documented.
- Loop-rendered child components require unique keys, and the docs state Livewire will behave incorrectly without them.
- Changing a child component key creates a new child instance, re-initializes it, and discards the old instance.
- Props are not reactive by default; `#[Reactive]` opts a child prop into updates from the parent.
- `#[Modelable]` lets a parent use `wire:model` on a child component property, and the docs state only the first modelable property is bound.
- Slots are evaluated in the parent component context.
- Dynamic children use documented dynamic component tags and explicit keys.
- Recursive components are supported, but templates must prevent infinite recursion.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact nesting boundary topic.
- No child rendering, prop behavior, key behavior, slot behavior, event behavior, dynamic component behavior, recursion behavior, or troubleshooting step absent from the retrieved Livewire 4.x docs was added.
- Loop-rendered children have unique keys and dynamic children have explicit keys.
- Parent-child communication guidance uses only documented event helpers, `$dispatch`, or `$parent` patterns.
- Unconfirmed nesting edge cases are explicitly left out or followed by a narrower Context7 lookup.
