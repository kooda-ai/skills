---
name: laravel-13-broadcasting
description: 'Use when: working with Laravel 13 broadcasting, event broadcasting, ShouldBroadcast, ShouldBroadcastNow, Channel, PrivateChannel, PresenceChannel, broadcastOn(), broadcastAs(), broadcastWith(), broadcastWhen(), InteractsWithSockets, InteractsWithBroadcasting, broadcastVia(), broadcast(...)->toOthers(), routes/channels.php, Broadcast::channel(), make:channel, channel:list, Laravel Echo, Reverb, Pusher, useEcho hooks, notifications over Echo, whisper, leaveChannel(), and Laravel 13 broadcasting code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 broadcasting, Echo, channel authorization, Reverb/Pusher setup, or review task'
---

# Laravel 13 Broadcasting

## Purpose
Use this skill to create, review, or explain Laravel 13 event broadcasting, channel authorization, and Laravel Echo usage using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact broadcasting topic.
2. Do not add broadcaster setup steps, config keys, channel classes, authorization patterns, Echo APIs, hook names, event methods, or queue behavior unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, class names, channel names, methods, hook names, environment variable names, and example values.
5. Do not infer behavior from older Laravel versions, Reverb docs beyond framework-returned snippets, Pusher docs, Ably docs, Sanctum docs, frontend framework docs, blog posts, source code, or general Laravel memory.
6. Keep queue worker, event listener, and failed-job details in `laravel-13-queues-events`; use this slice when the task is specifically about broadcasting events, channel authorization, broadcaster setup, or Echo consumers.

## Reference Map
- Broadcastable event classes, `ShouldBroadcast`, `ShouldBroadcastNow`, channel classes, custom event names and payloads, conditional broadcasting, broadcast connection selection, and excluding the current user: [broadcast-events.md](./references/broadcast-events.md)
- `routes/channels.php`, `Broadcast::channel(...)`, wildcard parameters, model binding, presence authorization payloads, channel classes, route bootstrap, and `channel:list`: [channel-authorization.md](./references/channel-authorization.md)
- `install:broadcasting --reverb`, Echo configuration for Reverb and Pusher, `useEcho`, notifications, `whisper`, and manual leave/listen controls: [echo-frontend.md](./references/echo-frontend.md)

## Workflow
1. Identify the exact surface: broadcastable event class, broadcast channel selection, synchronous broadcasting, custom broadcast name, custom broadcast payload, conditional broadcast, excluding current user, specific broadcaster connection, private or presence channel authorization, channel class, broadcast route bootstrap, channel inspection, Echo setup, Echo listener, notification listener, client whisper event, or broadcasting review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, classes, hooks, methods, route files, bootstrap options, channel names, and examples.
5. For broadcasting topics not in the references, such as `broadcastQueue` properties, presence member lifecycle callbacks beyond documented snippets, custom auth endpoints, Sanctum-powered broadcasting auth, Ably-specific setup, Reverb server operations, `ShouldBroadcastNow` queue internals, or testing broadcast events, rely on the fresh Context7 lookup and package-specific docs when needed.
6. For reviews, flag only documented mismatches: unsupported broadcasting interface, wrong channel class, unconfirmed authorization callback shape, unsupported Echo hook or method, malformed import copied from Context7, package-specific auth behavior claimed from framework docs, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Events are broadcast by implementing `Illuminate\Contracts\Broadcasting\ShouldBroadcast` and defining `broadcastOn(): array`.
- The docs show broadcasting on `PrivateChannel` and `PresenceChannel` instances from `broadcastOn()`.
- The docs show broadcasting immediately by implementing `ShouldBroadcastNow`.
- `broadcastAs(): string` is documented for overriding the default event name.
- `broadcastWith(): array` is documented for broadcasting a custom payload instead of all public properties.
- `broadcastWhen(): bool` is documented for conditionally allowing a broadcast.
- The docs show excluding the current user with `broadcast(new NewMessage($message))->toOthers()`.
- The docs show selecting a specific broadcast connection with `broadcast(new OrderShipmentStatusUpdated($update))->via('pusher')` and also with the `InteractsWithBroadcasting` trait plus `$this->broadcastVia('pusher')` inside the event constructor.
- Channel authorization is documented in `routes/channels.php` using `Broadcast::channel(...)`.
- Channel authorization callbacks receive the authenticated user and wildcard parameters from the channel pattern.
- Channel authorization callbacks support model binding, but the docs state implicit model binding scoping is not supported for channel model binding.
- Presence channel authorization may return an array of user data, and that data is available to JavaScript listeners.
- `php artisan make:channel OrderChannel` is documented for generating a channel class in `App/Broadcasting`.
- The docs show registering a channel class in `routes/channels.php` and authorizing access via a `join(...)` method.
- `php artisan channel:list` is documented for listing registered broadcast authorization callbacks.
- The docs show `php artisan install:broadcasting --reverb` to enable broadcasting with Laravel Reverb.
- The docs show Echo configuration for the `reverb` broadcaster and for the `pusher` broadcaster.
- The docs show `useEcho` hooks for React, Vue, and Svelte.
- The docs show `Echo.channel(...)->listen(...)` for event listeners and `Echo.private(...)->notification(...)` for broadcast notifications.
- The docs show `channel().whisper(...)` with `useEcho(...)` and manual controls such as `stopListening()`, `listen()`, `leaveChannel()`, and `leave()`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 broadcasting topic.
- Every command, class, interface, method, hook, channel pattern, route file, bootstrap option, and broadcaster statement is traceable to the lookup or references.
- Queue internals, broadcaster server setup, auth endpoint customization, and package-specific broadcasting behavior are not inferred when the current Laravel 13 docs did not confirm them.
- Unconfirmed broadcasting features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.