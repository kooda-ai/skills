---
name: livewire-4-dom-stream-sort-directives
description: 'Use when: working with Livewire 4 HTML directives for DOM diff control, refs, sorting, streaming, and client text updates, including wire:ignore, wire:ref, wire:replace, wire:sort, wire:stream, wire:text, refs for events and streaming, drag-and-drop sorting, custom web components, and optimistic text UI. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 DOM, ref, replace, ignore, sort, stream, or text directive concern'
---

# Livewire 4 DOM, Stream, And Sort Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 HTML directives that control DOM diffing, refs, drag-and-drop sorting, streamed content, and client-side text updates using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact directive topic.
2. Do not add DOM diffing behavior, ref behavior, sorting APIs, streaming APIs, text-update behavior, modifiers, caveats, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, modifier names, method names, parameter names, attribute names, and value strings.
5. Do not infer behavior from Livewire 3, Alpine habits outside the Livewire docs, browser APIs beyond the retrieved docs, package source code, or memory.

## Covered Directives
- `wire:ignore`
- `wire:ref`
- `wire:replace`
- `wire:sort`
- `wire:stream`
- `wire:text`

## Workflow
1. Identify whether the task is about excluding DOM from Livewire updates, naming targets, replacing DOM, sorting lists, streaming response chunks, or updating text content on the client.
2. Run a narrow Context7 query for the exact Livewire 4 directive before producing code or review findings.
3. For `wire:ignore`, wrap DOM managed by third-party JavaScript libraries or custom form inputs so Livewire does not update that portion of the page.
4. Use `wire:ignore.self` only for the documented behavior of ignoring changes to attributes of the root element rather than observing changes to its contents.
5. For `wire:replace`, use the directive when DOM diffing should be skipped for an element's children and the content should be replaced with new server-rendered elements.
6. Use `wire:replace.self` when the target element itself and all children should be replaced.
7. For `wire:ref`, name an element or component with `wire:ref="name"` so it can be targeted inside the current component.
8. Use refs for documented tasks: dispatching events to a child component with `->to(ref: 'name')`, accessing DOM elements through `$refs`, accessing a component through `$refs.name.$wire`, or streaming content with `->to(ref: 'name')`.
9. For dynamic refs in loops, combine documented dynamic `wire:ref` values with `wire:key` as shown in the docs.
10. Account for documented ref scoping: refs are scoped to the current component, and if multiple elements share a ref name, the first encountered element is used.
11. For `wire:sort`, add `wire:sort="method"` to the parent and `wire:sort:item="id"` to each sortable child.
12. Implement the handler so it accepts the item identifier and the new zero-based position. Persisting the new order is the developer's responsibility.
13. For sorting across groups, use `wire:sort:group="name"` on containers with the same group and `wire:sort:group-id="identifier"` so the handler receives the destination group identifier as a third parameter.
14. Use `wire:sort:handle` to restrict dragging to a child handle element.
15. Use `wire:sort:ignore` to prevent specific child areas such as buttons from starting drag operations.
16. For `wire:stream`, pair a target such as `wire:stream="answer"` with server-side `$this->stream(to: 'answer', content: $partial)` or the documented fluent ref targeting form when current docs confirm it.
17. Remember that appending streamed content is the default. Use `replace: true` or `wire:stream.replace` when streamed content should replace the target contents instead.
18. Include the documented caveat that `wire:stream` is not compatible with Laravel Octane when relevant.
19. For `wire:text`, use `wire:text="expression"` to update an element's text content from a component property or expression without waiting for a network roundtrip to re-render the component.
20. Use `wire:text` for documented optimistic UI patterns only when the component state is updated on the client and the server action persists the change in the background.
21. Finish by checking that every directive, modifier, handler signature, ref target, streaming target, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `wire:ignore` prevents Livewire from updating the contents of an element, even if they change between requests.
- `wire:ignore` is documented for third-party JavaScript libraries and custom form inputs.
- `wire:ignore.self` only ignores changes to attributes of the root element rather than observing changes to its contents.
- `wire:replace` skips DOM diffing on an element's children and replaces the content with new elements from the server.
- `wire:replace` is documented for third-party JavaScript libraries, custom web components, and cases where element reuse could cause state problems.
- `wire:replace.self` replaces the target element itself and all children.
- `wire:ref="name"` names an element or component for targeting inside Livewire.
- Refs are documented for dispatching events to a specific component, targeting DOM elements with `$refs`, accessing a component's `$wire`, and streaming content to an element.
- `$this->dispatch('close')->to(ref: 'modal')` dispatches an event directly to a component ref in the documented example.
- `$this->stream($chunk)->to(ref: 'answer')` streams content to a referenced element in the documented example.
- Refs are scoped to the current component, and duplicate ref names resolve to the first element encountered.
- `wire:sort="handleSort"` on a parent and `wire:sort:item="id"` on children enables drag-and-drop sorting.
- When an item is dropped, Livewire calls the handler with the item identifier and new zero-based position.
- Sorting across groups uses `wire:sort:group` and `wire:sort:group-id`; only the destination group's handler fires when moving an item between groups.
- `wire:sort:handle` restricts dragging to a handle element.
- `wire:sort:ignore` prevents drag initiation from specific child areas.
- `wire:sort` has no modifiers.
- `wire:stream` streams content to the page before a request completes.
- `wire:stream` is documented for countdowns and chat-bot responses.
- `wire:stream` is not compatible with Laravel Octane according to the docs.
- `$this->stream(to: 'target', content: '...')` appends by default.
- Passing `replace: true` to `$this->stream()` or using `wire:stream.replace` replaces the target contents instead of appending.
- `wire:text="expression"` updates an element's text content based on a component property or expression without requiring a network roundtrip to re-render the component.
- `wire:text` has no modifiers.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact directive topic.
- The answer does not include DOM diffing behavior, ref behavior, sorting behavior, streaming behavior, text-update behavior, modifiers, or caveats absent from the retrieved Livewire 4.x docs.
- Third-party JavaScript guidance distinguishes `wire:ignore` from `wire:replace` according to documented behavior.
- Sorting guidance includes the documented handler parameters and states that persisting order is the developer's responsibility.
- Streaming guidance distinguishes append, replace, ref targeting, and the documented Laravel Octane caveat.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
