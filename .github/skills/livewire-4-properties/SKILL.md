---
name: livewire-4-properties
description: 'Use when: working with Livewire 4 Properties, public properties, component state, mount initialization, fill(), reset(), pull(), wire:model, property types, $wire, #[Locked], #[Url], #[Session], #[Computed], #[Reactive], #[Modelable], #[Validate], form object properties, Wireable, Synthesizers, and property security. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 property state, binding, attribute, type, or security concern'
---

# Livewire 4 Properties

## Purpose
Use this skill to create, review, or explain Livewire 4 property state using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 property topic.
2. Do not add property APIs, attributes, helper methods, directive modifiers, supported types, security guidance, JavaScript APIs, form object behavior, or caveats unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented namespaces, attributes, method names, directive names, modifier names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel request habits, Alpine patterns, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Public state, lifecycle helpers, supported types, Wireable, and Synthesizers: [public-state-and-types.md](./references/public-state-and-types.md)
- `wire:model`, modifiers, form object properties, and property validation: [binding-and-validation.md](./references/binding-and-validation.md)
- Property-related attributes including `#[Url]`, `#[Locked]`, `#[Computed]`, `#[Reactive]`, `#[Modelable]`, `#[Session]`, and `#[Validate]`: [property-attributes.md](./references/property-attributes.md)
- JavaScript access, dehydration, public-property security, and Eloquent property notes: [security-and-javascript.md](./references/security-and-javascript.md)

## Workflow
1. Identify the property concern: public state, initialization, helper method, supported type, `wire:model` binding, form object property, validation attribute, URL/session persistence, computed property, nested component prop, JavaScript access, custom type, or security.
2. Run a narrow Context7 query for the exact Livewire 4 Properties topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For public state, confirm whether the task needs a class property default, `mount()`, `fill()`, `reset()`, `pull()`, or a documented form object helper.
5. For binding, confirm the exact `wire:model` directive, modifier, update timing, casting modifier, nested property path, and validation behavior.
6. For property attributes, confirm the exact attribute namespace, target, options, limitations, and documented example before recommending it.
7. For nested components, confirm whether a child prop should stay non-reactive, use `#[Reactive]`, or use `#[Modelable]` with parent `wire:model`.
8. For computed values, confirm `#[Computed]` usage, `$this` access, memoization, invalidation, and caching options from the current docs.
9. For custom or non-primitive values, confirm the supported type list and whether the docs call for `Livewire\Wireable` or Synthesizers.
10. For security, treat public properties as user input, confirm locking behavior, and validate or authorize before persistence when the docs require it.
11. Finish by checking that every property, attribute, helper, directive modifier, type, JavaScript API, and security claim is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Livewire properties store and manage component state.
- Public properties are accessible and modifiable on both the server and the client side.
- Property values can be initialized with class declarations and with `mount()` before the first render.
- `fill(array $values)`, `reset(...)`, and `pull(...)` are documented property or form-property helpers.
- `wire:model="propertyName"` binds HTML inputs to component properties.
- By default, `wire:model` updates do not send network requests until an action such as `wire:click` or `wire:submit` runs; request-triggering modifiers are documented separately.
- Livewire documents primitive property types, common PHP or Laravel property types, `Livewire\Wireable`, and Synthesizers for advanced custom type support.
- `#[Locked]` prevents client-side modification of a public property, and public Eloquent model properties are automatically locked by Livewire.
- `#[Url]` synchronizes a property with the browser query string.
- `#[Reactive]` and `#[Modelable]` are documented for parent-child property behavior in nested components.
- `#[Computed]` exposes a method as a computed property that is accessed through `$this`.
- Public property values must be treated like user input before persistence or sensitive operations.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Properties topic.
- The answer does not include APIs, modifiers, attributes, types, security guidance, or behavior absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 namespaces, attributes, method signatures, directive names, modifier names, and property paths.
- Public property guidance accounts for documented client-side access and tampering concerns.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.