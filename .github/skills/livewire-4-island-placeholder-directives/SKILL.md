---
name: livewire-4-island-placeholder-directives
description: 'Use when: working with Livewire 4 Blade directives @island and @placeholder, island rendering, isolated re-renders, wire:island, named islands, linked islands, lazy islands, deferred islands, skipped initial rendering, custom placeholders, placeholder root matching, nested islands, island polling, append/prepend modes, JavaScript island triggers, loops/conditionals limitations, and island scope rules. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 @island, @placeholder, wire:island, lazy island, deferred island, or island rendering concern'
---

# Livewire 4 Island And Placeholder Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 Blade island and placeholder directives using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact `@island`, `@placeholder`, or `wire:island` topic.
2. Do not add island parameters, placeholder behavior, JavaScript APIs, scope rules, lazy or deferred behavior, polling behavior, append/prepend behavior, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, parameter names, method names, attribute names, option names, and value strings.
5. Do not infer behavior from Livewire 3, frontend framework island patterns, Alpine habits outside the Livewire docs, package source code, or memory.

## Covered Directives
- `@island ... @endisland`
- `@placeholder ... @endplaceholder`
- Related documented `wire:island` attributes

## Workflow
1. Identify whether the task is about isolated island rendering, lazy loading, deferred loading, skipped initial rendering, placeholders, named island refreshes, append/prepend behavior, nested islands, polling, JavaScript triggering, loops or conditionals, island state synchronization, or island scope.
2. Run a narrow Context7 query for the exact Livewire 4 directive or option before producing code or review findings.
3. For isolated rendering, wrap the independently updating region in `@island ... @endisland`.
4. Use component properties and methods inside islands. Do not rely on parent template variables or loop variables inside the island unless the current docs confirm another pattern.
5. Name an island with `@island(name: 'revenue')` when another part of the template needs to target that island.
6. Target a named island from an action trigger with `wire:island="revenue"` only when the current docs confirm that targeted refresh behavior.
7. Use `wire:island.append="name"` or `wire:island.prepend="name"` only for documented append or prepend behavior.
8. Use `$wire.$island(name, options)` only when the current Context7 result confirms JavaScript or Alpine island triggering for the task.
9. For lazy islands, use `@island(lazy: true)` and add `@placeholder ... @endplaceholder` when a custom loading state is needed.
10. For deferred islands, use `@island(defer: true)` only when the docs-confirmed task needs loading immediately after page load regardless of visibility.
11. For on-demand initial rendering, use `@island(skip: true)` with a documented placeholder trigger such as `wire:click="$refresh"`.
12. Use `always: true` only when the current docs confirm the island should re-render whenever the parent component updates.
13. For nested islands, account for the documented behavior that inner islands are skipped when an outer island re-renders unless the docs confirm a different option for the task.
14. Use `wire:poll` inside an island when the docs-confirmed task should refresh only that island.
15. Keep islands out of loops and conditionals; the docs say islands cannot be used inside `@foreach`, `@if`, or other control structures because they do not have access to loop variables or conditional context.
16. Put loops or conditionals inside the island when the docs-confirmed task needs those constructs.
17. For `@placeholder` in lazy or deferred view-based components, use the directive in single-file or multi-file components. For class-based components, use the documented `placeholder()` method instead.
18. Ensure placeholder and component root elements use the same element type when using `@placeholder` for lazy components.
19. Include the documented state synchronization caveat when multiple island or root component requests can mutate the same component state: the last response to return wins.
20. Finish by checking that every directive, parameter, related attribute, JavaScript call, placeholder rule, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `@island ... @endisland` wraps a section of a Blade template that can re-render independently.
- When an action occurs inside an island, the island can re-render without affecting other parts of the component.
- `@island(name: 'revenue')` gives an island a name for targeted updates.
- `wire:island="revenue"` can target a named island from another action trigger in the documented example.
- `wire:island.append` appends new content to the existing island container.
- `wire:island.prepend` prepends new content to the existing island container.
- `$wire.$island(name, options)` is documented for triggering island actions from Alpine.js or JavaScript, with options such as `{ mode: 'append' }`.
- `@island(lazy: true)` is documented with `@placeholder` for a custom loading state while island content is fetched.
- `@island(defer: true)` loads immediately after page load regardless of visibility, while `@island(lazy: true)` loads when the island becomes visible in the viewport.
- `@island(skip: true)` prevents the island from rendering initially; the docs show a placeholder button using `wire:click="$refresh"` to load the island on demand.
- `always: true` is a documented island configuration parameter that forces the island to re-render whenever the parent component updates.
- `@placeholder ... @endplaceholder` defines custom placeholder content for a lazy or skipped island in the documented examples.
- The docs show lazy island placeholder content as a loading indicator and skipped island placeholder content as an on-demand load trigger.
- `wire:poll` inside an island is documented to refresh only the island, not the entire component.
- Islands can use component properties and methods.
- Islands cannot access parent template variables or loop variables in the documented scope example.
- Islands cannot be used inside `@foreach`, `@if`, or other control structures; the documented alternative is to put the loop or conditional inside the island.
- Island requests can run in parallel, and if islands and the root component mutate the same state, divergent state can occur with the last response winning.
- `@placeholder` displays custom content while lazy or deferred components and islands are loading.
- `@placeholder` works for single-file and multi-file components; class-based components use `placeholder()` instead.
- The placeholder and component must share the same root element type.
- The docs describe skeleton loaders as a common placeholder pattern.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact `@island`, `@placeholder`, or `wire:island` topic.
- The answer does not include island parameters, placeholder rules, JavaScript APIs, polling behavior, append/prepend behavior, or scope claims absent from the retrieved Livewire 4.x docs.
- Examples preserve documented directive names, option names, attribute names, method names, and value strings.
- Island scope guidance distinguishes component properties and methods from parent template variables and loop variables.
- Lazy, deferred, skipped, nested, polling, loop/conditional, placeholder-root, and state-synchronization guidance appears only when confirmed by the current Context7 result.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
