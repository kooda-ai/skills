# Context7 Query Shapes

Use `/websites/livewire_laravel_4_x` for Livewire 4.x lookups unless Context7 resolves a newer matching Livewire 4 documentation library.

## Broad Events Refresh
Use this when starting any Livewire Events task:

```text
Livewire 4 events documentation. Cover dispatching events from component actions, listening with #[On], event parameters, dynamic event names, dispatching directly to another component, dispatching to self, dispatching from Blade templates, Alpine integration, JavaScript listeners, testing events, and Laravel Echo event listeners. Include exact method names, directives, attributes, namespaces, and examples only from docs.
```

## Server-Side Dispatch And Listening
Use this when editing PHP component code:

```text
From Livewire 4.x events docs only, summarize dispatch(), named event payloads, #[On], Livewire\Attributes\On imports, listener method parameters, dynamic event names, dispatch()->to(), dispatch()->self(), child component @saved listeners, and Blade $dispatch or $dispatchTo syntax.
```

## Client-Side Events
Use this when the task involves component scripts, Alpine, or external JavaScript:

```text
Livewire 4.x JavaScript and Alpine event APIs from events and JavaScript docs: this.$on, this.$dispatch, this.$dispatchSelf, Livewire.on cleanup, Livewire.dispatch, Livewire.dispatchTo, $wire.$on, $wire.$dispatch, $wire.$dispatchTo, $wire.$dispatchSelf, x-on:event, x-on:event.window, $event.detail, and Alpine $dispatch.
```

## Tests And Echo
Use this when writing tests or real-time event listeners:

```text
Livewire 4.x testing and Echo event docs: assertDispatched, assertNotDispatched, dispatch() in tests, parameter assertions, closure assertions, #[On('echo:...')], getListeners() dynamic Echo channels, echo-private, echo-presence, here, joining, leaving, broadcastAs() custom names with dot prefix, and Echo prerequisites.
```

## Source Discipline
- Query narrowly before final code or review guidance.
- If Context7 does not confirm a detail, run one narrower lookup or omit the detail.
- Preserve documented syntax exactly when examples are needed.