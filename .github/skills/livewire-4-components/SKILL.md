---
name: livewire-4-components
description: 'Use when: working with Livewire 4 Components, single-file components, multi-file components, class-based components, make:livewire, livewire:convert, rendering <livewire:...>, Route::livewire(), pages:: components, properties, actions, lifecycle hooks, nesting, events, forms, validation, computed properties, #[Url], #[Locked], #[Reactive], #[Modelable], #[On], #[Validate], and #[Computed]. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 component task, component API lookup, component code review, form/action/event/nesting/page concern'
---

# Livewire 4 Components

## Purpose
Use this skill to create, review, or explain Livewire 4 components using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 component topic.
2. Do not add component formats, file paths, commands, attributes, method names, directive modifiers, lifecycle hooks, security advice, testing helpers, or JavaScript APIs unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented command flags, namespaces, attributes, directive names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controllers, Alpine habits, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Component creation, formats, rendering, props, organization, stubs, and troubleshooting: [component-creation-rendering.md](./references/component-creation-rendering.md)
- Public properties, state helpers, `wire:model`, supported types, JavaScript access, URL properties, and security: [state-properties.md](./references/state-properties.md)
- Actions, event listeners, JavaScript actions, magic actions, render skipping, async actions, lifecycle hooks, and action security: [actions-lifecycle.md](./references/actions-lifecycle.md)
- Nested components, props, keys, reactive/modelable props, slots, attributes, islands, dynamic children, and events: [nesting-events.md](./references/nesting-events.md)
- Forms, validation, form objects, real-time validation, dirty/loading states, custom inputs, and validation testing: [forms-validation.md](./references/forms-validation.md)
- Page components, layouts, titles, route parameters, route model binding, and computed properties: [pages-computed.md](./references/pages-computed.md)

## Workflow
1. Identify the component concern: creation format, rendering, state, action, lifecycle, nesting, event, form, validation, page routing, computed value, JavaScript integration, or testing.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. Choose the documented component format: single-file component, multi-file component, or class-based component.
5. Use documented Livewire 4 commands and flags only, such as `make:livewire`, `livewire:convert`, `livewire:form`, `livewire:layout`, `livewire:stubs`, `--sfc`, `--mfc`, `--class`, `--type=sfc|mfc|class`, `--test`, `--js`, and `--css` when confirmed by the current lookup.
6. For component state, confirm whether the task needs public properties, protected properties, `mount()`, `fill()`, `reset()`, `pull()`, `wire:model`, `#[Url]`, `#[Locked]`, `#[Computed]`, `#[Session]`, or JavaScript `$wire` access.
7. For interactions, confirm whether the task needs a PHP action, magic action, JavaScript action, event listener, lifecycle hook, renderless action, async action, confirmation, loading state, dirty state, or Alpine integration.
8. For nested components, require documented keys in loops, confirm whether props should be static, dynamic, reactive, modelable, slotted, forwarded as attributes, or replaced with an island.
9. For forms and validation, use only documented `wire:submit`, `wire:model` modifiers, `#[Validate]`, `rules()`, form objects, validation helper methods, and error-display patterns.
10. For page components, confirm `Route::livewire()`, `pages::` naming, layout, title, route parameter, and route model binding details from the current lookup.
11. Finish by checking that every class, method, attribute, command, flag, directive, modifier, and security claim in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Livewire 4 components are PHP classes with properties and methods that can be called directly from Blade templates.
- The default `make:livewire` output is a single-file component; Livewire 4 also documents multi-file and class-based components.
- Components render with `<livewire:component-name />`; subdirectories use dot notation, and namespaced components use prefixes such as `pages::`.
- Data passed into components is received through `mount()` or automatically assigned when public property names match passed values.
- Passed props are not reactive by default; `#[Reactive]` opts a child prop into reactive behavior.
- Public properties are available to the browser, persist across requests, and must be treated like user input.
- Eloquent model properties are automatically locked; `#[Locked]` prevents client-side modification of other public properties.
- Actions are public component methods callable from the frontend; every public method can be called from the client, so sensitive helper methods should be protected or private.
- Nested components are independent after initial render; child components in loops require unique keys.
- Forms use `wire:model` for property binding and `wire:submit` for action submission; `#[Validate]` and `$this->validate()` are documented validation entry points.
- Computed properties use `#[Computed]`, must be accessed as `$this->name` in templates, and are memoized only for a single request unless documented caching options are used.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact topic.
- The answer does not include APIs or behavior absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 component paths, command flags, directive names, modifier names, attributes, and method signatures.
- Security guidance treats public properties, action parameters, and public methods according to the documented Livewire security notes.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.