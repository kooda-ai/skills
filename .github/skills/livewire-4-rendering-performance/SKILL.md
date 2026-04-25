---
name: livewire-4-rendering-performance
description: 'Use when: working with Livewire 4 Islands, @island, wire:island, lazy islands, deferred islands, append/prepend island modes, nested islands, Lazy Loading, lazy/defer components, #[Lazy], #[Defer], placeholders, bundled lazy requests, full-page lazy routes, Computed Properties, #[Computed], computed cache, persist/cache options, and rendering performance. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 islands, lazy/defer loading, computed property, or rendering performance concern'
---

# Livewire 4 Rendering Performance

## Purpose
Use this skill to create, review, or explain Livewire 4 islands, lazy loading, deferred loading, and computed properties using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact rendering or performance topic.
2. Do not add island parameters, lazy-loading behavior, placeholder rules, request bundling behavior, computed-property cache options, or examples unless they appear in the retrieved documentation.
3. If a detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave it out.
4. Keep examples close to documented snippets and preserve directive names, attributes, method names, parameter names, options, and value strings.
5. Do not infer behavior from Livewire 3, frontend framework patterns, package source code, or memory.

## Covered Topics
- Islands with `@island`, `wire:island`, append/prepend modes, nesting, polling, and JavaScript triggering
- Lazy and deferred component loading
- Placeholder rendering for lazy components and islands
- Request isolation and bundling for lazy/deferred components
- Computed properties with `#[Computed]`

## Workflow
1. Identify the concern: isolated re-rendering, slow initial content, on-demand content, lazy component loading, deferred loading, placeholder UX, request bundling, derived data, or computed caching.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. For isolated regions inside one component, use `@island ... @endisland` when the docs-confirmed task benefits from updating only a portion of the component.
4. For expensive island content, combine `@island(lazy: true)` or `@island(defer: true)` with a documented `@placeholder` when needed.
5. For external island triggers, name the island with `@island(name: '...')` and scope an action with `wire:island="name"`. Use `wire:island.append` or `wire:island.prepend` only for documented append/prepend behavior.
6. For JavaScript-triggered island actions, use `$wire.$island('name')` or `$wire.$island('name', { mode: 'append' })` only as documented.
7. For nested islands, account for the documented default that inner islands are skipped when an outer island re-renders.
8. Use `always: true` only when the island should re-render whenever the parent component updates, and `skip: true` only for on-demand initial rendering with placeholder content.
9. Keep islands out of loops and conditionals; put the loop or conditional inside the island when the docs-confirmed task needs those constructs.
10. For full components that should not block initial rendering, use `<livewire:component lazy />`, `<livewire:component defer />`, `#[Lazy]`, `#[Defer]`, route `->lazy()`, or route `->defer()` only after confirming which loading behavior is needed.
11. For lazy placeholders in view-based components, use `@placeholder ... @endplaceholder`. For class-based components, use `placeholder()` returning HTML or a view. Ensure placeholder and component roots use the same element type.
12. For passed props on lazy components, account for documented dehydration and later rehydration, including Eloquent models being serialized and re-queried before the lazy request is handled.
13. For many lazy or deferred components, use `bundle: true`, `lazy.bundle`, `defer.bundle`, `#[Lazy(bundle: true)]`, or `#[Defer(bundle: true)]` only when the docs-confirmed page should trade independent parallel loading for fewer requests.
14. For tests that should assert final lazy content, use `Livewire::withoutLazyLoading()` only as documented.
15. For derived values, add `#[Computed]` to a method and access it as `$this->name`; use `unset($this->name)` only when the docs-confirmed task needs to bust the computed cache during a request.
16. For computed caching beyond a single request, use `#[Computed(persist: true)]`, `seconds`, `cache: true`, `key`, or `tags` only according to the current docs.
17. Finish by checking that every island option, lazy/defer flag, placeholder rule, computed option, and performance caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- Islands allow isolated regions within a Livewire component to update independently without creating separate child components.
- When an action occurs inside an island, only that island re-renders; the rest of the component remains untouched.
- Islands load with the page by default; `lazy: true` defers initial rendering until the island becomes visible, while `defer: true` loads after page load regardless of visibility.
- A named island can be targeted from another action using `wire:island="name"`; islands with the same name are linked and render as a group.
- `wire:island.append` adds new island content to the end, and `wire:island.prepend` adds it to the beginning.
- Nested inner islands are skipped by default when an outer island re-renders.
- `wire:poll` inside an island refreshes only that island.
- Islands have access to component properties and methods, but not template variables defined outside the island.
- Lazy components skip the initial component load and fetch the full component later, while deferred components load immediately after the initial page load completes.
- Lazy and deferred component requests are isolated by default and therefore load independently in parallel.
- Bundling lazy or deferred components sends multiple lazy/deferred updates as one network request when explicitly enabled.
- Lazy placeholders default to an empty `<div></div>` unless a placeholder is defined.
- `#[Computed]` turns a method into a derived property accessed through `$this->property`.
- Computed properties cache their result for the duration of a request by default.
- `unset($this->computedProperty)` clears a computed value's cache during the request.
- `#[Computed(persist: true)]` caches across requests for the same component instance, with a documented default of 3600 seconds.
- Computed properties cannot be used on `Livewire\Form` objects.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact islands, lazy loading, or computed property topic.
- No island, lazy/defer, placeholder, bundling, or computed-cache behavior absent from the retrieved Livewire 4.x docs was added.
- Islands are not placed inside loops or conditionals unless the current docs explicitly support the specific pattern.
- Lazy placeholder guidance distinguishes view-based `@placeholder` from class-based `placeholder()`.
- Computed property examples access values through `$this` and avoid `Livewire\Form` objects.
- Performance guidance notes request isolation, bundling tradeoffs, and possible state divergence only when relevant to the task.
