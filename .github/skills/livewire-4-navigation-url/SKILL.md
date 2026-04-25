---
name: livewire-4-navigation-url
description: 'Use when: working with Livewire 4 Navigate, wire:navigate, SPA navigation, redirects, redirectRoute(), redirectIntended(), redirectAction(), navigate: true, @persist, data-current, wire:current, URL Query Parameters, #[Url], query strings, pagination, WithPagination, WithoutUrlPagination, paginator hooks, and pagination views. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 navigation, redirect, URL query parameter, or pagination concern'
---

# Livewire 4 Navigation And URL State

## Purpose
Use this skill to create, review, or explain Livewire 4 navigation, redirect, URL query, and pagination behavior using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact navigation, URL, redirect, or pagination topic.
2. Do not add navigation hooks, redirect helpers, query-string options, pagination methods, configuration keys, script caveats, or examples unless they appear in the retrieved documentation.
3. If a detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave it out.
4. Keep examples close to documented snippets and preserve route syntax, directive names, attributes, method names, parameter names, configuration keys, and value strings.
5. Do not infer behavior from Livewire 3, Laravel routing habits beyond the retrieved docs, package source code, or memory.

## Covered Topics
- Navigate and `wire:navigate`
- Redirecting and SPA redirects
- Persisted elements, active links, scroll preservation, and navigation script evaluation
- URL query parameters with `#[Url]`
- Pagination with `WithPagination`

## Workflow
1. Identify the concern: link navigation, programmatic navigation, redirect, active link styling, persisted UI, script evaluation, URL-backed state, paginator state, multiple paginators, hooks, theme, or custom pagination view.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. For SPA links, use `wire:navigate` on anchor tags. Confirm whether `.hover` prefetching is warranted before adding it.
4. For redirects that should use SPA navigation, use `$this->redirect('/path', navigate: true)` only when the docs-confirmed task calls for Livewire navigation.
5. For redirects, choose among `$this->redirect()`, `$this->redirectRoute()`, `$this->redirectIntended()`, and `$this->redirectAction()` according to the documented target type.
6. For flash messages, use Laravel `session()->flash()` before the Livewire redirect when the destination page reads the flashed session value.
7. For persisted UI across `wire:navigate` visits, use `@persist('name') ... @endpersist`, place persisted elements outside Livewire components, and add `wire:navigate:scroll` to persisted scroll containers when the scroll position must be preserved.
8. For active links under `wire:navigate`, prefer documented `data-current` styling, or use `wire:current` when class injection is the desired approach. Use `wire:current.ignore` only when disabling automatic current-link behavior.
9. For navigation JavaScript, use the documented `livewire:navigate`, `livewire:navigating`, and `livewire:navigated` browser events, and avoid relying on `DOMContentLoaded` for subsequent navigations.
10. For navigation assets and scripts, account for documented rules: existing head scripts run once, new head scripts are evaluated, body scripts are re-evaluated, `data-navigate-track` can trigger a full reload on tracked query-string changes, and `data-navigate-once` runs a body script only on the initial visit.
11. For navigation progress, use the documented `config/livewire.php` `navigate.show_progress_bar` and `navigate.progress_bar_color` keys only when customization is needed.
12. For URL-backed component state, use `#[Url]` on properties and confirm options such as `as`, `except`, `keep`, `history`, and nullable typed properties from the current docs.
13. For pagination, use `Livewire\WithPagination` in any component containing pagination, return a Laravel paginator such as `paginate(10)`, and render links with `$this->posts->links()` or the documented variable name.
14. For paginator URL behavior, keep default query-string tracking unless `Livewire\WithoutUrlPagination` is explicitly needed and the loss of persisted page state is acceptable.
15. For paginator scroll behavior, pass `data: ['scrollTo' => false]` or `data: ['scrollTo' => '#selector']` to `links()` only as documented.
16. For changing filters or sorting, use `$this->resetPage()` when the docs-confirmed workflow should return to page 1.
17. For multiple paginators, use the `pageName` argument in Laravel's `paginate()` call and pass the same `pageName` to Livewire page navigation methods.
18. For paginator hooks, use the documented hook names such as `updatingPage`, `updatedPage`, named paginator hooks like `updatingInvoicesPage`, or generic `updatingPaginators` and `updatedPaginators`.
19. Finish by checking that every route helper, directive, attribute, option, method, config key, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `wire:navigate` intercepts link clicks, requests the next page in the background, and replaces the current URL, `<title>`, and `<body>` with the new page response.
- Livewire shows a top progress bar when a page takes longer than 150ms to load, unless navigation progress is disabled in config.
- `wire:navigate.hover` prefetches after a user hovers over a link for 60 milliseconds and may increase server usage.
- `Livewire.navigate('/new/url')` manually triggers a navigation from JavaScript.
- `@persist` reuses a matching named element across navigation visits, preserving state such as audio playback.
- Persisted elements should be placed outside Livewire components, commonly in the main layout.
- `data-current` is automatically added to `wire:navigate` links matching the current page; `wire:current` can add classes instead.
- `#[Url]` writes property changes to the query string and reads query values into properties on page load.
- `#[Url(as: 'q')]` changes the query parameter name, `except` customizes excluded values, `keep` always includes the parameter, and `history: true` pushes browser history entries.
- Nullable property type hints allow empty query parameters such as `?search=` to become `null` instead of an empty string.
- `WithPagination` is required for Livewire pagination features.
- Livewire's paginator tracks the current page in the URL query string by default, usually as `?page=2`.
- `WithoutUrlPagination` disables paginator URL tracking and also means the current page will not persist across page changes.
- Pagination helpers include `setPage($page)`, `resetPage()`, `nextPage()`, and `previousPage()`.
- Custom pagination views can be supplied through `->links('custom-pagination-links')`, `paginationView()`, or `paginationSimpleView()`.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact navigation, URL, redirect, or pagination feature.
- The answer does not include redirect helpers, URL options, paginator APIs, hooks, configuration keys, or script caveats absent from the retrieved Livewire 4.x docs.
- SPA redirect guidance uses `navigate: true` only where the docs confirm Livewire navigation should be used.
- URL-state guidance distinguishes `#[Url]` options, nullable properties, and paginator URL tracking.
- Pagination guidance includes `WithPagination` before any Livewire pagination behavior is used.
- Navigation script guidance accounts for `livewire:navigated` and documented script re-evaluation rules when relevant.
