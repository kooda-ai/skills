---
name: livewire-4-lifecycle-hooks
description: 'Use when: working with Livewire 4 Lifecycle Hooks, mount(), boot(), hydrate(), dehydrate(), updating(), updated(), property-specific update hooks, array update hooks, rendering(), rendered(), exception($e, $stopPropagation), trait-prefixed hooks, form object update hooks, lifecycle dependency injection, and lifecycle security. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 lifecycle hook, initialization, hydration, update hook, render hook, exception hook, trait hook, or form-object hook concern'
---

# Livewire 4 Lifecycle Hooks

## Purpose
Use this skill to create, review, or explain Livewire 4 lifecycle hooks using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 lifecycle hook topic.
2. Do not add lifecycle hooks, method signatures, parameters, dependency injection behavior, security guidance, custom-type guidance, form-object hooks, or examples unless they appear in the retrieved documentation.
3. If a requested lifecycle detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented hook names, namespaces, attributes, method signatures, parameter names, directive names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controller lifecycle habits, Alpine patterns, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Component lifecycle hook table, usage notes, signatures, trait hooks, and form-object hooks: [lifecycle-hooks.md](./references/lifecycle-hooks.md)

## Workflow
1. Identify the lifecycle concern: initialization, every-request setup, property update interception, hydration and dehydration, rendering, exception handling, trait reuse, form-object property hooks, dependency injection, or sensitive public-property handling.
2. Run a narrow Context7 query for the exact Livewire 4 lifecycle topic before producing code, review findings, or explanation.
3. Load the relevant reference file from the map above.
4. For initialization, use documented `mount()` behavior for accepting parameters and initializing state once when the component is first created.
5. For setup that must run on every server request, use documented `boot()` behavior, especially for protected properties that are not persisted between requests.
6. For property changes, choose documented `updating` hooks before a property is set and documented `updated` hooks after a property is set. Use property-specific hooks when the docs show the target property in the method name.
7. For array properties, include the documented additional `$key` argument and the documented null-key behavior when the whole array is updated.
8. For custom state transformation, use documented `hydrate()` and `dehydrate()` behavior only when needed, and include the docs' recommendation to use Wireables or Synthesizers for custom types.
9. For render timing, use documented `rendering($view, $data)` before rendering and `rendered($view, $html)` after rendering.
10. For exception handling, use documented `exception($e, $stopPropagation)` behavior and call `$stopPropagation()` only according to the docs.
11. For traits, use documented camelCased trait-name prefixes, such as `mountHasPostForm()` for a `HasPostForm` trait.
12. For form objects, use only documented `Livewire\Form` property update hooks such as `updating`, `updated`, property-specific hooks, and array-property hooks.
13. Finish by checking that every hook, parameter, namespace, attribute, recommendation, caveat, and example is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- The documented component lifecycle hooks are `mount()`, `hydrate()`, `boot()`, `updating()`, `updated()`, `rendering()`, `rendered()`, `dehydrate()`, and `exception($e, $stopPropagation)`.
- `mount()` is used instead of `__construct()` for accepting parameters and initializing state when the component is first created.
- Lifecycle hook methods support Laravel dependency injection through type-hinted parameters.
- `boot()` runs at the beginning of every request, both initial and subsequent, and can initialize protected properties that are not persisted between requests.
- Client-side users can update public properties, most commonly through `wire:model`; update hooks can validate, authorize, prevent, or normalize values around those updates.
- `hydrate()` runs at the beginning of every subsequent request, and `dehydrate()` runs at the end of every component request.
- The docs demonstrate `hydrate()` and `dehydrate()` for DTO transformation but recommend Wireables or Synthesizers for custom types.
- `rendering($view, $data)` runs before the component view is rendered, and `rendered($view, $html)` runs after rendering.
- `exception($e, $stopPropagation)` can inspect an exception and call `$stopPropagation()` to catch the issue.
- Traits can define lifecycle hooks prefixed with the camelCased trait name to avoid conflicts.
- `Livewire\Form` objects support property update hooks similar to component update hooks.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact lifecycle hook topic.
- The answer does not include hooks, signatures, parameters, namespaces, attributes, custom-type advice, security guidance, or examples absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 hook names, method signatures, parameter names, namespaces, attributes, and property names.
- Public-property guidance accounts for documented client-side updates and the documented `#[Locked]` or authorization guidance for sensitive public properties.
- Hydration guidance includes the documented Wireables or Synthesizers recommendation when custom types are involved.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.