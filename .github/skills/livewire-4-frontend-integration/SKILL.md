---
name: livewire-4-frontend-integration
description: 'Use when: working with Livewire 4 Alpine, $wire, JavaScript, component scripts, @script, @assets, Styles, scoped CSS, global component CSS, Loading States, data-loading, wire:loading, @teleport, modals, nested dialogs, Tailwind data variants, and plain CSS loading selectors. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 Alpine, JavaScript, styles, loading state, or teleport concern'
---

# Livewire 4 Frontend Integration

## Purpose
Use this skill to create, review, or explain Livewire 4 frontend integration features using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact frontend feature topic.
2. Do not add Alpine behavior, JavaScript APIs, script loading rules, CSS scoping rules, loading-state selectors, teleport caveats, or examples unless they appear in the retrieved documentation.
3. If a detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave it out.
4. Keep examples close to documented snippets and preserve directive names, attributes, method names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Alpine habits outside the Livewire docs, package source code, or memory.

## Covered Topics
- Alpine integration and `$wire`
- Component JavaScript, `@script`, `@assets`, and the `Livewire` global object
- Component Styles and scoped or global CSS
- Loading States with `data-loading`, `wire:loading`, Tailwind variants, and plain CSS
- Teleport with `@teleport`

## Workflow
1. Identify the concern: Alpine-only UI, `$wire` access, component script timing, external assets, scoped CSS, global CSS, loading feedback, or DOM teleporting.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. For Alpine, use it inside Livewire components for client-side interactivity that does not require a Livewire round-trip, and use `$wire` only as documented for accessing or mutating properties, calling actions, refreshing with `$wire.$refresh()`, and passing parameters.
4. For `$wire.entangle()`, only use it when the docs-confirmed task needs rare bidirectional Alpine and Livewire state synchronization. Prefer direct `$wire` access, and do not use the deprecated `@entangle` Blade directive.
5. For JavaScript in components, use component `<script>` tags when the code is component-specific or needs `$wire`; wrap scripts in `@script ... @endscript` for class-based components.
6. For shared scripts or styles loaded with a component, use `@assets ... @endassets`. Confirm that assets are loaded before component scripts and only once per page.
7. For manual Alpine bundling, confirm the layout includes `@livewireScriptConfig`, imports `Livewire` and `Alpine` from `../../vendor/livewire/livewire/dist/livewire.esm`, registers directives or plugins, and calls `Livewire.start()`.
8. For component Styles, use a root-level `<style>` tag in single-file components or a same-name CSS file in multi-file components. Use `<style global>` or `.global.css` only for documented global styling cases.
9. For scoped CSS, account for Livewire's root-element scoping through the `wire:name` attribute, use `&` only when targeting the component root, and remember that component styles are deduplicated across multiple instances.
10. For loading feedback, prefer `data-loading` selectors when the docs confirm they fit the task. Use `wire:loading` for basic show/hide scenarios when appropriate.
11. For Tailwind loading states, choose documented variants such as `data-loading:`, `not-data-loading:hidden`, `in-data-loading:`, `not-in-data-loading:`, `has-data-loading:`, `peer-data-loading:`, or arbitrary variants only when Tailwind v4 support is confirmed for the advanced variants.
12. For plain CSS loading states, target `[data-loading]` or descendants under `[data-loading]` exactly as the docs describe.
13. For Teleport, wrap the content in `@teleport('selector') ... @endteleport`, use a selector accepted by `document.querySelector()`, teleport outside the Livewire component, and include only a single root element inside the teleport block.
14. Finish by checking that every directive, attribute, method, CSS selector, Tailwind variant, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- Livewire ships with Alpine out of the box, so separate Alpine installation is not required for normal Livewire pages.
- Alpine state inside Livewire is maintained across Livewire component updates.
- `$wire` is available inside Alpine expressions in a Livewire component and can access or mutate public properties, call Livewire actions, and refresh the component.
- Mutating `$wire.someProperty` from Alpine updates the client immediately and sends the server update on the next Livewire request.
- `$wire` action calls can pass parameters and can return promises that resolve with backend return values.
- Component `<script>` tags execute when the component loads; lazy or conditional components can execute JavaScript after the page has initialized.
- Class-based components require `@script` around component scripts so Livewire can scope and time script execution correctly.
- `@assets` loads component script or stylesheet assets before component scripts and loads those assets only once per page.
- Component Styles are scoped by default and do not leak to other elements with the same classes elsewhere on the page.
- Global component CSS uses `<style global>` in single-file components or `.global.css` in multi-file components.
- Livewire automatically adds `data-loading` to elements that trigger network requests, including actions, form submissions, `wire:model.live` property updates, and event dispatches.
- The loading-state docs prefer `data-loading` selectors for most cases, while `wire:loading` remains available for basic toggling.
- `@teleport` renders part of a Livewire template elsewhere in the DOM and is useful for nested dialogs, overlays, and modal z-index issues.
- Teleport must target outside the component and the teleported block must contain a single root element.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact frontend feature.
- No Alpine, JavaScript, CSS, loading-state, or teleport behavior absent from the retrieved Livewire 4.x docs was added.
- Class-based script usage includes `@script` when scripts are shown.
- External script or stylesheet usage uses `@assets` only as documented.
- Loading-state guidance distinguishes `data-loading`, `wire:loading`, Tailwind v4 variants, and plain CSS according to the retrieved docs.
- Teleport guidance includes the outside-component and single-root limitations.
