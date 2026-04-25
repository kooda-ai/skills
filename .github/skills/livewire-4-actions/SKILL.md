---
name: livewire-4-actions
description: 'Use when: working with Livewire 4 Actions, component public methods, wire:click, wire:submit, action parameters, Eloquent model parameters, dependency injection, event listener and key modifiers, wire:confirm, wire:loading, data-loading, $refresh, $set, $toggle, $dispatch, $event, $parent, Alpine $wire, JavaScript $js actions, #[Renderless], skipRender(), .renderless, #[Async], .async, .preserve-scroll, action security, and Livewire::test()->call(). Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 action, directive, security, loading, JavaScript action, async/renderless, or action test concern'
---

# Livewire 4 Actions

## Purpose
Use this skill to create, review, or explain Livewire 4 Actions using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 Actions topic.
2. Do not add action APIs, directive modifiers, attributes, method names, JavaScript APIs, testing helpers, security guidance, or examples unless they appear in the retrieved documentation.
3. If a requested Actions detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented directive names, method names, attributes, namespaces, modifier names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controller habits, Alpine habits, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Server-side Actions, event listeners, parameters, dependency injection, renderless actions, async actions, preserving scroll, and security: [server-actions.md](./references/server-actions.md)
- Alpine `$wire`, JavaScript `$js` actions, magic actions, and the documented action-related `$wire` API: [client-and-magic-actions.md](./references/client-and-magic-actions.md)
- Form submission, confirmations, loading states, `data-loading`, `wire:target`, and action testing: [forms-loading-testing.md](./references/forms-loading-testing.md)

## Workflow
1. Identify the Actions concern: basic action method, `wire:click`, `wire:submit`, action parameter, model parameter, dependency injection, browser event listener, confirmation, loading state, Alpine `$wire`, JavaScript `$js`, magic action, renderless action, async action, preserving scroll, security, or testing.
2. Run a narrow Context7 query for the exact Livewire 4 Actions topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For server-side behavior, choose documented public component methods and documented directives such as `wire:click="methodName"` or `wire:submit="methodName"`.
5. For parameters, treat values from the frontend as untrusted input and include documented authorization checks before mutating or deleting database records.
6. For model or service parameters, use documented Eloquent model action parameters and Laravel dependency injection only when the current lookup confirms them.
7. For event listeners, use documented `wire:` event names, key modifiers, event handler modifiers, `$event`, and custom-event patterns only as returned by the current lookup.
8. For confirmations and user feedback, choose documented `wire:confirm`, `wire:confirm.prompt`, `wire:loading`, `data-loading`, and `wire:target` patterns.
9. For client-side integration, choose documented Alpine `$wire` action calls, `$wire` return promises, `$js()` JavaScript actions, `$wire.$js...`, or `$this->js(...)` only when relevant.
10. For render and request behavior, choose documented `#[Renderless]`, `$this->skipRender()`, `.renderless`, `.preserve-scroll`, `wire:click.async`, or `#[Async]` according to the docs.
11. For tests, use documented Livewire testing methods such as `Livewire::test(...)->set(...)->call(...)` and the relevant assertions returned by the lookup.
12. Finish by checking that every directive, modifier, attribute, namespace, method, helper, JavaScript API, testing helper, and security claim is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Livewire actions are component methods triggered by frontend interactions such as clicking a button or submitting a form.
- `wire:submit="save"` intercepts a form submit event, prevents the default browser submission, and calls the `save()` action on the server.
- `wire:click="download"` or `wire:click="delete({{ $post->id }})"` calls a component method when an element is clicked.
- Action parameters are arbitrary user input and must be authorized before sensitive updates or deletes.
- Eloquent model action parameters can be automatically resolved from a corresponding model ID when the action parameter is type-hinted with a model class.
- Laravel dependency injection is supported by type-hinting dependencies in an action signature.
- Event listeners can use `wire:click`, `wire:submit`, `wire:keydown`, `wire:keyup`, `wire:mouseenter`, or a custom `wire:*` browser event name.
- `$refresh` triggers a server roundtrip and re-renders the component without calling a custom method; pending data updates are applied on the server when refreshed.
- `wire:confirm` shows a browser confirmation dialog before an action, and `wire:confirm.prompt` requires matching typed input before the action runs.
- Alpine can call PHP actions with `$wire.actionName(...)`; returned values resolve from the `$wire` promise when the server response is received.
- JavaScript actions defined with `$js()` run client-side without a server request and can be called from Blade, Alpine, or PHP with documented APIs.
- Magic actions documented for templates include `$parent`, `$set`, `$refresh`, `$toggle`, `$dispatch`, and `$event`.
- `#[Renderless]`, `$this->skipRender()`, and `.renderless` are documented ways to skip rendering after an action.
- Livewire serializes actions within the same component by default; `wire:click.async` and `#[Async]` run actions in parallel.
- Async actions are documented for fire-and-forget work, background operations, analytics, logging, and JavaScript-only results; the docs warn against using them for UI-reflected state mutations.
- `.preserve-scroll` maintains scroll position during updates.
- `wire:loading` and automatic `data-loading` attributes are documented ways to show action progress; `wire:target` scopes loading indicators to actions, parameters, or properties.
- Testing uses `Livewire::test(...)->call(...)` for action calls and documented assertions for validation, authorization, redirects, events, and JavaScript evaluation.
- Every public method in a Livewire component is callable from the client; dangerous helper methods should be `protected` or `private`.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Actions topic.
- The answer does not include APIs, modifiers, attributes, testing helpers, JavaScript APIs, or behavior absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 namespaces, directives, modifiers, attributes, method signatures, action names, and testing helpers.
- Security guidance treats public methods and action parameters according to the documented Livewire Actions security notes.
- Async guidance includes the documented race-condition warning when UI-reflected component state would be mutated.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.