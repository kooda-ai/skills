---
name: livewire-4-lifecycle-observation-directives
description: 'Use when: working with Livewire 4 HTML directives that trigger actions from component render, viewport intersection, or polling, including wire:init, wire:intersect, wire:poll, intersection enter/leave, polling intervals, keep-alive polling, visible polling, lazy loading alternatives, and scroll-triggered actions. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 init, intersect, poll, lazy-load, viewport, or polling directive concern'
---

# Livewire 4 Lifecycle And Observation Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 HTML directives that run actions after render, when elements enter or leave the viewport, or at polling intervals using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact directive topic.
2. Do not add lifecycle behavior, polling behavior, viewport thresholds, modifiers, performance guidance, alternatives, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, modifier names, method names, interval formats, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Alpine habits outside the Livewire docs, browser APIs beyond the retrieved docs, package source code, or memory.

## Covered Directives
- `wire:init`
- `wire:intersect`
- `wire:poll`

## Workflow
1. Identify whether the task needs an action immediately after render, an action when an element intersects the viewport, or repeated polling.
2. Run a narrow Context7 query for the exact Livewire 4 directive before producing code or review findings.
3. For `wire:init`, call an action with `wire:init="action"` when data should load immediately after the Livewire component renders.
4. Prefer Livewire lazy loading over `wire:init` only when the current docs-confirmed task matches the documented guidance that lazy loading is preferable in most cases.
5. For `wire:intersect`, call an action when an element enters the viewport using `wire:intersect="action"`.
6. Use `wire:intersect:enter="action"` for explicit enter behavior and `wire:intersect:leave="action"` for leave behavior.
7. Choose documented visibility modifiers only when needed: `.half`, `.full`, or `.threshold.[0-100]`.
8. Use `.margin.[value]` to trigger before or after the viewport boundary only with documented formats such as pixels, percentages, or four-side margin values.
9. Add `.once` when the action should fire only on the first intersection.
10. Combine `wire:intersect` modifiers only in documented patterns such as `.once.half.margin.100px`.
11. For `wire:poll`, place the directive on an element to refresh the component on an interval, or pass an action name with `wire:poll="action"`.
12. Remember the documented default polling interval is every 2.5 seconds.
13. Use interval modifiers such as `.15s` or `.15000ms` to reduce request frequency when polling could be resource intensive.
14. Account for documented background throttling: Livewire reduces polling requests by 95% when the page is in a background tab.
15. Use `.keep-alive` only when polling should continue in a background tab.
16. Use `.visible` only when polling should happen while the element is visible in the viewport.
17. Finish by checking that every directive, modifier, interval, threshold, and performance caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `wire:init="loadPosts"` runs the `loadPosts` action immediately after the Livewire component renders on the page.
- The docs say Livewire lazy loading is preferable to `wire:init` in most cases.
- `wire:init` has no modifiers.
- `wire:intersect="loadMore"` calls the action when the element enters the viewport.
- `wire:intersect:enter="trackView"` runs on enter, and `wire:intersect:leave="pauseVideo"` runs on leave.
- `wire:intersect` defaults to triggering when any part of the element is visible.
- `wire:intersect.half` triggers when half of the element is visible.
- `wire:intersect.full` triggers when the entire element is visible.
- `wire:intersect.threshold.25` uses a custom visibility threshold percentage.
- `wire:intersect.margin.200px`, `.margin.10%`, and four-side margin examples are documented.
- `wire:intersect.once` fires the action only on the first intersection.
- Documented `wire:intersect` use cases include infinite scroll, lazy loading images, and tracking visibility.
- `wire:poll` refreshes the component every 2.5 seconds by default.
- `wire:poll="refreshSubscribers"` calls the named action every 2.5 seconds.
- `wire:poll.15s` and `wire:poll.15000ms` customize polling intervals.
- Polling can be resource intensive, and the docs recommend longer polling intervals to reduce requests.
- Livewire throttles polling by 95% while the page is in a background tab.
- `wire:poll.keep-alive` opts out of background throttling.
- `wire:poll.visible` only polls when the element is visible in the viewport.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact directive topic.
- The answer does not include lifecycle behavior, viewport behavior, polling behavior, modifiers, thresholds, intervals, or performance guidance absent from the retrieved Livewire 4.x docs.
- `wire:init` guidance includes the documented lazy loading preference when relevant.
- `wire:intersect` guidance distinguishes enter, leave, visibility threshold, margin, and once behavior.
- `wire:poll` guidance includes default interval, custom intervals, background throttling, `.keep-alive`, and `.visible` when relevant.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
