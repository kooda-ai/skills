---
name: livewire-4-events
description: 'Use when: working with Livewire 4 Events, dispatch(), #[On], event parameters, dynamic event names, child component listeners, $dispatch, $dispatchTo, dispatch()->to(), dispatch()->self(), Alpine event interop, JavaScript Livewire.on, $wire.$on, $wire.$dispatch, event tests, assertDispatched, assertNotDispatched, Laravel Echo listeners, private channels, presence channels, broadcastAs(), and event communication tradeoffs. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 event dispatch, listener, JavaScript/Alpine interop, test, Echo, or component communication concern'
---

# Livewire 4 Events

## Purpose
Use this skill to create, review, or explain Livewire 4 Events using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 Events topic.
2. Do not add event APIs, method names, attribute names, directive syntax, JavaScript APIs, Echo listener formats, testing helpers, or behavior unless they appear in the retrieved documentation.
3. If a requested Events detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented event names, parameter names, namespaces, method names, attribute names, directive syntax, and value strings.
5. Do not infer behavior from Livewire 3, Laravel event habits, Alpine habits, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- PHP dispatching, `#[On]`, parameters, dynamic names, targeted events, self events, child listeners, and Blade dispatch helpers: [dispatch-listen.md](./references/dispatch-listen.md)
- Component scripts, global JavaScript, `$wire` event methods, Alpine listening, and Alpine dispatching: [client-events.md](./references/client-events.md)
- Parent-child event communication, testing helpers, and Laravel Echo listener formats: [nesting-testing-echo.md](./references/nesting-testing-echo.md)

## Workflow
1. Identify the Events concern: PHP dispatch, PHP listener, event payload, dynamic event name, child component listener, Blade dispatch helper, targeted dispatch, self dispatch, JavaScript listener, Alpine interop, parent-child communication, testing, or Echo listener.
2. Run a narrow Context7 query for the exact Livewire 4 Events topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For server-side dispatching, use documented `$this->dispatch('event-name')` syntax, with named parameters only when the current lookup confirms payloads.
5. For server-side listening, use the documented `Livewire\Attributes\On` import and place `#[On('event-name')]` above the documented listener method.
6. For dynamic event names, preserve documented placeholder syntax such as `post-updated.{post.id}` or Echo channel placeholders such as `echo:orders.{order.id},OrderShipped`.
7. For events from a specific child component, use documented Blade listener attributes such as `@saved="$refresh"`, `@saved="close"`, or `@saved="close($event.detail.postId)"`.
8. For Blade, component script, Alpine, or plain JavaScript integration, choose only documented helpers such as `$dispatch`, `$dispatchTo`, `this.$on`, `this.$dispatch`, `this.$dispatchSelf`, `Livewire.on`, `Livewire.dispatch`, `Livewire.dispatchTo`, `$wire.$on`, `$wire.$dispatch`, `$wire.$dispatchTo`, and `$wire.$dispatchSelf`.
9. For parent-child communication, consider the documented alternatives: client-side dispatch for fewer requests, `$parent` for direct parent access, or islands when the docs identify event communication overhead.
10. For tests, use documented `Livewire::test(...)->assertDispatched(...)`, `assertNotDispatched(...)`, and `dispatch(...)` patterns only as confirmed by the current lookup.
11. For real-time events, require documented Laravel Echo prerequisites and use only documented `echo:`, `echo-private:`, `echo-presence:`, dynamic channel, custom broadcast name, and presence event formats.
12. Finish by checking that every event name, helper, modifier, attribute, namespace, testing helper, Echo channel prefix, and JavaScript API is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Livewire events communicate between different components on the page and are plain browser events under the hood.
- Components dispatch events with `$this->dispatch('post-created')` and may pass named payload data such as `title: $post->title`.
- Components listen with `#[On('post-created')]` on a method, after importing `Livewire\Attributes\On`.
- Payload data sent with an event is provided to the listener method as its first argument in the documented `#[On]` example.
- Dynamic listener names can use component data placeholders, such as `#[On('post-updated.{post.id}')]`.
- Child component events can be listened to directly in the parent template with `@saved` attributes.
- PHP dispatching can target another component with `$this->dispatch('post-created')->to(component: Dashboard::class)`.
- The Events docs describe self dispatch with `dispatch()->self()` and show `$this->dispatch('post-created')->to(self: true)`.
- Blade templates can dispatch events with `$dispatch(...)` and target a component with `$dispatchTo(...)`.
- Component scripts can listen with `this.$on(...)`, dispatch with `this.$dispatch(...)`, and restrict dispatch with `this.$dispatchSelf(...)`.
- Global JavaScript can listen with `Livewire.on(...)`; the returned cleanup function unregisters the listener.
- Alpine can listen with `x-on:event-name`, use `.window` for page-wide events, access payloads through `$event.detail`, and dispatch Livewire-interceptable events with `$dispatch(...)`.
- Tests can assert dispatched events with `assertDispatched(...)`, assert absence with `assertNotDispatched(...)`, and dispatch events in the test environment with `dispatch(...)`.
- Laravel Echo listeners use `#[On('echo:channel,EventName')]`, `getListeners()`, dynamic channel placeholders, private/presence prefixes, and custom broadcast names prefixed with `.` when `broadcastAs()` is used.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Events topic.
- The answer does not include APIs, helpers, attributes, listener formats, testing methods, Echo prefixes, or behavior absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 namespaces, event names, payload syntax, dynamic placeholder syntax, JavaScript APIs, Blade listener attributes, and testing helpers.
- Parent-child guidance includes documented tradeoffs only: client-side dispatch to avoid an extra request, `$parent` for direct access, and islands when the docs mention event communication overhead.
- Echo guidance includes the documented prerequisites when real-time events are used.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.