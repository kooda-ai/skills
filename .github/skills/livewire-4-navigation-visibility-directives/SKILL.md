---
name: livewire-4-navigation-visibility-directives
description: 'Use when: working with Livewire 4 HTML directives for navigation, active links, visibility, initialization hiding, transitions, and offline state, including wire:navigate, wire:current, wire:cloak, wire:show, wire:transition, wire:offline, data-current, View Transitions, and active-link matching. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 navigation, active link, visibility, transition, cloak, show, or offline directive concern'
---

# Livewire 4 Navigation And Visibility Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 HTML directives that control SPA-style navigation, active-link styling, visibility, initialization hiding, view transitions, and offline indicators using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact directive topic.
2. Do not add navigation behavior, matching rules, visibility rules, transition APIs, browser support notes, modifiers, attributes, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, modifier names, method names, attribute names, CSS pseudo-elements, and value strings.
5. Do not infer behavior from Livewire 3, Alpine habits outside the Livewire docs, browser APIs beyond the retrieved docs, package source code, or memory.

## Covered Directives
- `wire:navigate`
- `wire:current`
- `wire:cloak`
- `wire:show`
- `wire:transition`
- `wire:offline`

## Workflow
1. Identify whether the task is about SPA navigation, active-link styling, page-load cloaking, CSS-display visibility, view transitions, or offline feedback.
2. Run a narrow Context7 query for the exact Livewire 4 directive before producing code or review findings.
3. For `wire:navigate`, use anchor tags with `href` values. Livewire intercepts clicks, fetches the next page in the background, and swaps the current page.
4. Add `wire:navigate.hover` only when documented hover prefetching is desired.
5. For active links on `wire:navigate` anchors, prefer documented `data-current` styling when CSS or Tailwind data variants are enough.
6. Use `wire:current="classes"` when the task specifically needs class injection for active links.
7. For `wire:current`, account for documented partial matching by default, `.exact` matching when the paths must match exactly, and `.strict` matching when trailing slashes must be compared strictly.
8. If `wire:current` is not working, check the documented troubleshooting points: the page needs at least one Livewire component or hardcoded `@livewireScripts`, and the link needs an `href` attribute.
9. For `wire:cloak`, add the directive to elements that must stay hidden until Livewire finishes initializing. This directive has no modifiers.
10. Combine `wire:cloak` with `wire:show` for dynamic content that would otherwise flash both initial states before Livewire initializes.
11. For `wire:show`, use a documented expression to toggle an element's CSS `display` state without removing the element from the DOM.
12. Combine `wire:show` with Alpine `x-transition` only as documented for show/hide animations.
13. For `wire:transition`, add it to elements that may be added, removed, or changed during a Livewire update.
14. Use no value for the documented default `view-transition-name` of `match-element`, or pass a string such as `wire:transition="sidebar"` to set a custom `view-transition-name`.
15. Customize transitions with documented View Transition pseudo-elements such as `::view-transition-old(name)`, `::view-transition-new(name)`, and `::view-transition-group(name)`.
16. Use `$this->transition(type: '...')`, `#[Transition(type: '...')]`, `$this->skipTransition()`, or `#[Transition(skip: true)]` only when the current docs confirm action-specific transition behavior.
17. Include documented transition caveats when relevant: Livewire respects `prefers-reduced-motion`, unsupported browsers still function without the visual transition, and Firefox supports basic view transitions but not transition types according to the docs.
18. For `wire:offline`, show an element when the user's device loses connection, or toggle documented classes and attributes while offline.
19. Finish by checking that every directive, modifier, matching rule, CSS pseudo-element, transition method, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `wire:navigate` gives links an SPA-like navigation experience by intercepting clicks, fetching the page in the background, and swapping it with the current page.
- `wire:navigate.hover` prefetches a page when the user hovers over the link.
- Livewire automatically adds `data-current` to matching `wire:navigate` links so CSS or Tailwind can style active links.
- `wire:current="font-bold text-zinc-800"` applies classes to active links.
- `wire:current` works with `wire:navigate` links and page changes, and it adds `data-current` to matching links in addition to the specified classes.
- `wire:current` uses partial path matching by default.
- `wire:current.exact` uses exact path matching, and `wire:current.strict` forces strict path comparison including trailing slashes.
- `wire:cloak` hides elements on page load until Livewire is fully initialized and has no modifiers.
- `wire:cloak` is documented for preventing flashes of uninitialized dynamic content such as alternate `wire:show` states.
- `wire:show="expression"` shows or hides an element based on an expression.
- `wire:show` toggles CSS `display: none` rather than removing the element from the DOM.
- `wire:show` has no modifiers.
- `wire:transition` uses the browser View Transitions API for elements that appear, disappear, or change during a Livewire update.
- `wire:transition` without a value uses `match-element` as the `view-transition-name`.
- `wire:transition="name"` uses the provided string as the `view-transition-name`.
- View Transition CSS customization uses documented pseudo-elements for old, new, and group snapshots.
- Transition types can be set with `$this->transition(type: ...)` or `#[Transition(type: ...)]` in documented examples.
- Transitions can be skipped for a request with `$this->skipTransition()` or `#[Transition(skip: true)]` in documented examples.
- Livewire disables transitions when `prefers-reduced-motion` is enabled.
- The docs list Chrome 111+, Edge 111+, and Safari 18+ as supporting View Transitions, with Firefox 144+ supporting basic view transitions but not transition types.
- `wire:offline` is hidden by default and becomes visible when the user loses connection.
- `wire:offline.class`, `wire:offline.class.remove`, and `wire:offline.attr` toggle classes or attributes when offline.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact directive topic.
- The answer does not include navigation behavior, active-link rules, visibility behavior, transition APIs, browser support notes, or modifiers absent from the retrieved Livewire 4.x docs.
- Active-link guidance distinguishes automatic `data-current` from `wire:current` class injection.
- Visibility guidance distinguishes `wire:show` CSS display toggling from DOM removal.
- Transition guidance includes documented browser and reduced-motion caveats when relevant.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
