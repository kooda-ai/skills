---
name: livewire-4-advanced-dom-runtime
description: 'Use when: working with Livewire 4 advanced DOM runtime, Morphing, DOM morph hooks, morph.updating, morph.updated, morph.removing, morph.removed, morph.adding, morph.added, morph, morphed, Hydration, hydrate(), dehydrate(), snapshots, checksums, CorruptComponentPayloadException, and troubleshooting morph or snapshot issues. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 morphing, hydration, snapshot, DOM hook, or runtime troubleshooting concern'
---

# Livewire 4 Advanced DOM Runtime

## Purpose
Use this skill to create, review, or explain Livewire 4 DOM morphing, hydration, snapshots, and runtime troubleshooting using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Morphing, Hydration, JavaScript hook, snapshot, checksum, or troubleshooting topic.
2. Do not add DOM diffing behavior, hook names, hook parameters, lifecycle timing, snapshot structure, exception behavior, or troubleshooting steps unless they appear in the retrieved documentation.
3. If a requested runtime detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the detail out.
4. Preserve documented hook names, parameter names, method names, exception names, directive names, and configuration keys exactly.
5. Do not infer behavior from Livewire 3, morphdom habits, Alpine habits outside the Livewire docs, package source code, or memory.

## Covered Topics
- DOM Morphing and morph lifecycle hooks
- Component and element JavaScript initialization hooks
- Hydration and dehydration lifecycle hooks
- Advanced hydration tuple metadata
- Snapshot checksums and corrupted payload failures
- Runtime troubleshooting for morph, hydration, snapshot, root-element, and JavaScript-loading issues

## Workflow
1. Identify the runtime concern: DOM update, morph hook, component initialization hook, lifecycle hydration, custom DTO transform, advanced property hydration, snapshot checksum, corrupt payload, missing root element, non-rendering component, or client JavaScript failure.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. For DOM morphing extension points, use only documented `Livewire.hook(...)` hooks and only the parameters shown by the docs for that hook.
4. For element-level changes, distinguish documented element morph hooks from component morph hooks: element hooks run around individual element updates, removals, and additions; component hooks run around a component morph.
5. For initialization, use `component.init` for new Livewire component initialization and `element.init` for DOM elements inside a Livewire component only when the docs confirm the need.
6. For hydration lifecycle work, use `mount()` for the initial request, `hydrate()` at the beginning of subsequent requests, and `dehydrate()` at the end of every request.
7. For custom DTO transformation with `hydrate()` and `dehydrate()`, include the docs note that this demonstrates the hooks but that Wireables or Synthesizers are recommended for custom types.
8. For advanced hydration explanations, describe the tuple shape only as documented: raw data in the first element and metadata in the second element so Livewire can reconstruct complex PHP types from JSON.
9. For snapshot security, explain that Livewire sends a component snapshot to the browser between requests and validates the next request with a checksum.
10. For `CorruptComponentPayloadException`, state only the documented behavior: checksum mismatch means the snapshot was altered and the request fails.
11. For troubleshooting, use only documented checks such as component file path/name/namespace, `php artisan view:clear`, exactly one root element, PHP syntax errors, Laravel logs, layout `@livewireStyles` and `@livewireScripts`, and browser console JavaScript errors.
12. Finish by checking that every hook, lifecycle method, snapshot claim, exception name, and troubleshooting step is traceable to the current Context7 result.

## Confirmed Core Patterns
- Livewire exposes `Livewire.hook('component.init', ...)` and `Livewire.hook('element.init', ...)` for advanced JavaScript initialization behavior.
- Livewire exposes DOM morph hooks including `morph.updating`, `morph.updated`, `morph.removing`, `morph.removed`, `morph.adding`, and `morph.added`.
- Livewire exposes component morph hooks named `morph` and `morphed`.
- `hydrate()` runs at the beginning of every subsequent request and does not run on the initial request.
- `dehydrate()` runs at the end of every component request.
- Hydration and dehydration refer to serializing component state to JSON for the client side and unserializing that JSON back into PHP on a later request.
- Complex property types can use tuple metadata during hydration because JSON alone cannot represent PHP objects such as Laravel collections.
- Livewire snapshots are sent to the browser between requests so the component can be rebuilt on the next server round trip.
- Snapshot checksums are used to detect browser-side snapshot tampering.
- A checksum mismatch throws `CorruptComponentPayloadException` and the request fails.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact DOM runtime topic.
- No morph hook, lifecycle hook, hydration behavior, snapshot behavior, exception behavior, or troubleshooting step absent from the retrieved Livewire 4.x docs was added.
- Examples preserve documented hook names, parameter names, method names, directive names, and exception names.
- Custom type guidance routes to Wireables or Synthesizers unless the task specifically asks to demonstrate `hydrate()` and `dehydrate()`.
- Troubleshooting output separates documented checks from unconfirmed guesses.
