---
name: livewire-4-advanced-state-hydration
description: 'Use when: working with Livewire 4 advanced state hydration, custom property types, primitive and Laravel property types, Wireable, toLivewire(), fromLivewire(), Synthesizers, Synth classes, match(), dehydrate(), hydrate(), static $key, tuple metadata, DTO state, and custom serialization. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 custom property type, Wireable, Synthesizer, tuple metadata, or state serialization concern'
---

# Livewire 4 Advanced State Hydration

## Purpose
Use this skill to create, review, or explain Livewire 4 custom state serialization, Wireables, Synthesizers, and hydration metadata using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact property type, Wireable, Synthesizer, or hydration topic.
2. Do not add supported types, method signatures, Synthesizer class structure, tuple shapes, registration details, metadata keys, or custom serialization behavior unless they appear in the retrieved documentation.
3. If a requested custom-state detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the detail out.
4. Preserve documented class names, interface names, method names, static property names, return shapes, namespaces, and example value keys exactly.
5. Do not infer behavior from Livewire 3, Laravel casting, Eloquent serialization habits, package source code, or memory.

## Covered Topics
- Primitive property dehydration to JSON
- Common PHP and Laravel property types
- Advanced hydration tuple metadata
- `Livewire\Wireable`
- `toLivewire()` and `fromLivewire($value)`
- Synthesizers for custom property types
- `static $key`, `match($target)`, `dehydrate($target)`, and `hydrate($value)`
- DTO transformation with lifecycle hooks and when to prefer Wireables or Synthesizers

## Workflow
1. Identify the state concern: primitive value, supported PHP or Laravel type, Eloquent model or collection property, custom DTO, Wireable object, Synthesizer, tuple metadata, or public-property exposure.
2. Run a narrow Context7 query for the exact Livewire 4 state hydration topic before producing code or review findings.
3. For primitive properties, describe JSON serialization only for documented primitive types such as `array`, `string`, `int`, `float`, `bool`, and `null`.
4. For common PHP and Laravel property types, confirm the current documented type list before naming specific supported classes.
5. For `Livewire\Wireable`, implement only the documented `toLivewire()` and `fromLivewire($value)` contract.
6. For Synthesizers, use the documented Synthesizer shape only after the docs confirm the target type and methods.
7. For a custom Synthesizer, include `static $key`, `match($target)`, `dehydrate($target)`, and `hydrate($value)` only when the current docs confirm them.
8. In `dehydrate($target)`, preserve the documented return shape of an array containing data and metadata, such as `[data, metadata]`, when showing examples.
9. In `hydrate($value)`, reconstruct the custom object only from documented values returned by `dehydrate($target)`.
10. For lifecycle `hydrate()` and `dehydrate()` DTO transformations, include the docs note that Wireables or Synthesizers are recommended for custom types.
11. For public property security, treat dehydrated values as client-visible state and confirm any locking, validation, authorization, or Eloquent-property behavior in the current lookup before mentioning it.
12. Finish by checking that every interface, method, tuple shape, metadata claim, supported type, and security statement is traceable to the current Context7 result.

## Decision Points
- Use primitive properties when JSON serialization is sufficient and the documented primitive type fits.
- Use documented common PHP or Laravel property types only when the current docs confirm the type.
- Use `Livewire\Wireable` when a custom class can own its own `toLivewire()` and `fromLivewire($value)` conversion.
- Use a Synthesizer when the docs-confirmed task needs Livewire's advanced custom property type mechanism.
- Use lifecycle `hydrate()` and `dehydrate()` for the documented hook demonstration or narrow transformation needs, but prefer Wireables or Synthesizers for custom types when the docs recommend them.

## Confirmed Core Patterns
- Livewire properties store component state and public properties are accessible on both the server and client side.
- Primitive property values are serialized to JSON between requests.
- Livewire documents `Livewire\Wireable` for custom property types with `toLivewire()` and static `fromLivewire($value)`.
- Livewire documents Synthesizers as the advanced mechanism for supporting different property types.
- A documented Synthesizer example uses a class extending `Synth` with `static $key`, `match($target)`, `dehydrate($target)`, and `hydrate($value)`.
- Advanced hydration can associate metadata with raw data in a tuple so Livewire can reconstruct PHP types that JSON cannot represent by itself.
- `hydrate()` and `dehydrate()` can transform state at request boundaries, but the lifecycle docs recommend Wireables or Synthesizers for custom types.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact state hydration, Wireable, or Synthesizer topic.
- No supported type, custom serialization API, metadata structure, registration rule, or security claim absent from the retrieved Livewire 4.x docs was added.
- Examples preserve documented method names, static property names, array shapes, value keys, and namespaces.
- Public-property guidance accounts for documented client-side visibility and modification.
- Unconfirmed custom-state behavior is explicitly left out or followed by a narrower Context7 lookup.
