---
name: livewire-4-action-form-directives
description: 'Use when: working with Livewire 4 HTML directives for actions, forms, reactive attributes, and request feedback, including wire:bind, wire:click, wire:submit, wire:model, wire:loading, wire:dirty, wire:confirm, wire:target, data-loading, $dirty, action modifiers, form binding, and confirmation prompts. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 action, form, binding, loading, dirty, or confirmation directive concern'
---

# Livewire 4 Action And Form Directives

## Purpose
Use this skill to create, review, or explain Livewire 4 HTML directives that trigger actions, bind form state, bind client-side attributes, or show request and dirty-state feedback using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact directive topic.
2. Do not add directive behavior, modifiers, JavaScript expressions, action rules, validation habits, security guidance, or examples unless they appear in the retrieved documentation.
3. If a requested detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve directive names, modifier names, method names, parameter formats, attribute names, and value strings.
5. Do not infer behavior from Livewire 3, Alpine habits outside the Livewire docs, Laravel controller habits, package source code, or memory.

## Covered Directives
- `wire:click`
- `wire:submit`
- `wire:model`
- `wire:bind`
- `wire:loading`
- `wire:dirty`
- `wire:confirm`

## Workflow
1. Identify whether the task is about an action trigger, form submission, input binding, client-side attribute binding, loading feedback, dirty-state feedback, or action confirmation.
2. Run a narrow Context7 query for the exact Livewire 4 directive before producing code or review findings.
3. For `wire:click`, call a component method using `wire:click="methodName"` or pass documented parameters with `wire:click="methodName(param1, param2)"`.
4. Treat `wire:click` parameters as untrusted input. The docs warn to authorize ownership before updating data.
5. When placing `wire:click` on an anchor tag, add `.prevent` to prevent the browser from following the `href`.
6. For `wire:submit`, place the directive on a `<form>` and call the desired component method. Livewire prevents the default browser submission automatically.
7. Account for documented form submission behavior: Livewire disables submit buttons and marks inputs as `readonly` while a form submission is being sent.
8. For action modifiers, use only documented event modifiers such as `.prevent`, `.stop`, `.self`, `.once`, `.debounce`, `.throttle`, `.window`, `.document`, `.outside`, `.passive`, `.capture`, `.camel`, `.dot`, `.renderless`, `.preserve-scroll`, and `.async` when the current directive docs confirm them.
9. For `wire:model`, bind native inputs to component properties and remember that model updates do not send network requests by default until an action occurs.
10. Use `wire:model.live` when the docs-confirmed task needs live server updates. The default live debounce is 150ms, and `.debounce.Xms` customizes that timing.
11. Choose `wire:model.blur`, `wire:model.change`, `wire:model.enter`, `.lazy`, `.throttle.Xms`, `.number`, `.boolean`, `.fill`, `.deep`, or `.preserve-scroll` only when the documented behavior matches the task.
12. For dependent select inputs, add `wire:key` to the changing select so Livewire refreshes its value when the options change.
13. For `wire:model.deep`, use it sparingly and only when the task specifically needs the directive to listen to input or change events from descendant elements.
14. For `wire:bind`, bind HTML attributes with `wire:bind:{attribute}="expression"`. Valid documented examples include `class`, `style`, `href`, `disabled`, and `data-*` attributes.
15. Use `wire:bind` for client-side reactive attribute updates without a full server-side re-render. This directive has no modifiers.
16. For `wire:loading`, use the directive to hide an element by default and show it while a Livewire request is in flight.
17. Use `wire:loading.remove`, `.class`, `.class.remove`, `.attr`, display modifiers, and delay aliases only as documented.
18. Scope loading indicators with `wire:target="action"`, `wire:target="property"`, comma-separated targets, action parameters, or `wire:target.except="action"` when the page has multiple request sources.
19. Prefer documented `data-loading` styling when direct CSS or Tailwind data variants fit better than `wire:loading` show/hide behavior.
20. For `wire:dirty`, show feedback only while client-side state diverges from server-side state. Use `wire:target="property"` for property-specific dirty indicators.
21. For dirty-state styling, use only documented `.remove`, `.class`, `$dirty`, `$dirty('property')`, `$dirty(['title', 'description'])`, or Alpine `$wire.$dirty()` patterns.
22. For `wire:confirm`, attach the directive to an action such as `wire:click` or `wire:submit`. The default browser confirmation alert controls whether the action runs.
23. For more dangerous actions, use `wire:confirm.prompt="message|expected-input"` only when a case-sensitive typed confirmation is desired.
24. Finish by checking that every directive, modifier, related attribute, JavaScript expression, and caveat is traceable to the current Context7 result.

## Confirmed Core Patterns
- `wire:click` calls a Livewire component method when the element is clicked.
- `wire:click="delete({{ $post->id }})"` passes parameters to the action, and the docs warn not to trust action parameters.
- `wire:click.prevent` is required on anchor tags when browser link navigation should not occur.
- `wire:click.renderless` skips re-rendering after the action completes.
- `wire:click.preserve-scroll` preserves the current scroll position during updates.
- `wire:click.async` allows actions to run in parallel instead of being queued within the same component.
- `wire:submit` intercepts a form submit event, prevents default browser handling, and calls the named Livewire action.
- `wire:submit` automatically prevents default browser submission without needing `.prevent`.
- During form submission, Livewire disables submit buttons and marks form inputs as `readonly`.
- `wire:model` binds component properties to native input elements such as text inputs, textareas, checkboxes, radio buttons, select dropdowns, dependent selects, and multi-selects.
- `wire:model` only sends a network request when an action is performed unless a live-update modifier is used.
- `wire:model.live` sends updates as the user types and applies a 150ms debounce by default.
- `wire:model.blur`, `.change`, and `.enter` customize when syncing occurs.
- `.number` casts the value to an integer on the server, `.boolean` casts to a boolean, and `.fill` uses the initial value from the HTML value attribute.
- `wire:model.deep` also listens to events from child elements and should be used sparingly.
- `wire:bind:{attribute}="expression"` dynamically binds HTML attributes to component properties or expressions on the client.
- `wire:bind` has no modifiers.
- `wire:loading` shows an element during a Livewire request and hides it otherwise.
- `wire:loading.remove` reverses the visibility behavior.
- `wire:loading.class`, `wire:loading.class.remove`, and `wire:loading.attr` toggle classes or attributes during requests.
- `wire:target` can scope loading indicators to actions, properties, multiple targets, action parameters, or all requests except a named target.
- Livewire automatically adds `data-loading` to elements that trigger network requests, and the docs show CSS and Tailwind data-attribute styling patterns.
- `wire:dirty` indicates when client-side state differs from server-side state.
- `wire:dirty.class` adds a class while dirty, and `wire:dirty.remove` hides an element while dirty.
- `$dirty`, `$dirty('property')`, and `$dirty(['title', 'description'])` can be used in Livewire directives; Alpine can call `$wire.$dirty()`.
- `wire:confirm` shows a default browser confirmation dialog before an action runs.
- `wire:confirm.prompt` requires case-sensitive matching input in the documented `message|expected-input` format.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact directive topic.
- The answer does not include directive behavior, modifiers, attributes, JavaScript expressions, or security claims absent from the retrieved Livewire 4.x docs.
- Action parameters are treated according to the documented warning about untrusted input.
- Form submission guidance includes documented automatic `preventDefault()`, disabled submit buttons, and `readonly` input behavior when relevant.
- `wire:model` guidance distinguishes local client updates from server network requests.
- Loading guidance distinguishes `wire:loading`, `wire:target`, and documented `data-loading` styling.
- Unconfirmed directive details are explicitly left out or followed by a narrower Context7 lookup.
