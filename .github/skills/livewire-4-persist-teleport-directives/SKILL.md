---
name: livewire-4-persist-teleport-directives
description: 'Use when: working with Livewire 4 Blade directives @persist and @teleport, persisted UI during wire:navigate, matching persist keys, media players across page visits, chat or third-party widgets, layout placement, preserved DOM state, preserved event listeners, preserved Alpine data, persisted scroll with wire:navigate:scroll, active links in persisted navigation, teleporting modals or overlays, teleport selectors, outside-component targets, and single-root teleport content. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 @persist, @teleport, persisted UI, navigate persistence, modal teleport, or DOM target concern'
---

# Livewire 4 Persist And Teleport Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 Blade directives for persisting UI across Livewire navigation and teleporting template content elsewhere in the DOM using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact `@persist` or `@teleport` topic.
2. Do not add persistence behavior, navigation requirements, preserved state claims, teleport target rules, selector rules, root-element rules, caveats, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, key names, selector strings, attribute names, and value strings.
5. Do not infer behavior from Livewire 3, Alpine teleport habits, browser DOM habits beyond the retrieved docs, package source code, or memory.

## Covered Directives
- `@persist('key') ... @endpersist`
- `@teleport('selector') ... @endteleport`

## Workflow
1. Identify whether the task is about keeping an element alive across `wire:navigate` visits or rendering Livewire template content in another DOM location.
2. Run a narrow Context7 query for the exact Livewire 4 directive before producing code or review findings.
3. For `@persist`, wrap the content with `@persist('key') ... @endpersist` using a required string key.
4. Use `@persist` for documented navigation scenarios such as audio or video players, chat widgets, or third-party widgets that should continue across page visits.
5. Place persisted elements in the main application layout and typically outside individual Livewire components when the task matches the documented placement guidance.
6. Ensure the persisted element has a matching `@persist` name on the next page. Livewire scans the new page for matching names during navigation.
7. Use `@persist` only with `wire:navigate` behavior. Standard browser page loads re-initialize the element as usual according to the docs.
8. When relevant, account for the documented preserved DOM state: Livewire moves the existing DOM element to the new page, preserving internal state, active event listeners, and Alpine.js data.
9. For scrollable persisted elements, add `wire:navigate:scroll` to the element containing a scrollbar when the docs-confirmed task needs scroll position preserved.
10. For active links inside persisted elements, do not rely on server-side Blade conditionals. Use documented `data-current` styling or `wire:current` behavior when the current docs confirm the chosen approach.
11. For `@teleport`, wrap the content with `@teleport('selector') ... @endteleport`, where the selector is a string accepted by `document.querySelector()`.
12. Use `@teleport` for documented cases such as modals, nested dialogs, backdrops, and overlays that need to break out of a parent stacking context.
13. Ensure the teleport selector resolves to an element that exists in the DOM before the Livewire component is rendered.
14. Teleport content outside the current Livewire component. Teleporting to an element within the same component is not supported according to the docs.
15. Ensure the teleported content has a single root element, because Livewire only supports teleporting one root element.
16. Finish by checking that every directive, key, selector, placement rule, preserved-state claim, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `@persist(string $key) ... @endpersist` is the documented reference form for persisted content.
- `@persist('player')` is documented for an audio player that should continue across page visits.
- Documented `@persist` use cases include audio or video players, chat widgets, and third-party widgets.
- During navigation, Livewire scans the new page for matching `@persist` names.
- If a matching `@persist` name is found, Livewire moves the existing DOM element from the old page to the new page.
- Moving the existing persisted element avoids re-rendering or re-initializing it.
- The docs state this preserves the element's internal state, active event listeners, and Alpine.js data.
- Persisted elements are most effective in the main application layout and typically outside individual Livewire components.
- `@persist` relies entirely on `wire:navigate`; standard browser page loads re-initialize the element as usual.
- Scrollable persisted elements can use `wire:navigate:scroll` to maintain scroll position.
- Inside persisted elements, server-side Blade conditionals for active links will not work because the element is reused between page loads.
- Documented active-link options inside persisted navigation include `data-current` styling and `wire:current`.
- `@teleport('body') ... @endteleport` is documented for rendering modal content at the end of the `body` element.
- `@teleport` renders a portion of a Livewire component template in a different part of the DOM.
- The teleport selector can be any string normally passed to `document.querySelector()`, such as `body`, `#some-id`, or `.some-class`.
- The teleport target must exist in the DOM before the Livewire component is rendered.
- Teleported content must be teleported outside the current Livewire component.
- Teleporting to an element within the same component is not supported.
- The content inside `@teleport` must have a single root element.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact `@persist` or `@teleport` topic.
- The answer does not include persistence behavior, navigation requirements, selector behavior, DOM placement rules, preserved-state claims, or caveats absent from the retrieved Livewire 4.x docs.
- `@persist` guidance includes the required key, matching-name behavior, layout placement guidance, active-link handling, scroll preservation, and `wire:navigate` dependency when relevant.
- `@teleport` guidance includes selector existence, outside-component targeting, and single-root content limitations.
- Examples preserve documented directive names, key strings, selector strings, and structure.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
