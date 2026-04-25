---
name: filament-5-notifications
description: 'Use when: working with Filament 5 Notifications, Notification::make(), title(), body(), send(), status(), success(), warning(), danger(), info(), icon(), iconColor(), color(), duration(), seconds(), persistent(), notification actions, FilamentNotification, close-notification, positioning, databaseNotifications(), sendToDatabase(), toDatabase(), markAsRead(), markAsUnread(), broadcast(), toBroadcast(), Echo, and websocket setup. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Notification task, toast, action, JavaScript notification, database notification, broadcast notification, or code to review'
---

# Filament 5 Notifications

## Purpose
Use this skill to create, review, or explain Filament 5 Notifications using only details confirmed in the Filament 5.x documentation from Context7 or the official Filament 5.x notification documentation.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Notifications topic.
2. Do not add behavior, APIs, options, namespaces, commands, events, security guidance, queue behavior, broadcasting behavior, or conventions unless they appear in the retrieved documentation.
3. If a requested Notifications topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Notifications tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, event names, enum names, and class names.

## Reference Map
- Toast notifications, styling, duration, actions, JavaScript objects, closing notifications, and positioning: [overview-actions.md](./references/overview-actions.md)
- Database notification table setup, panel setup, sending, polling, read/unread actions, and modal opening: [database-notifications.md](./references/database-notifications.md)
- Broadcast notification sending and panel websocket setup: [broadcast-notifications.md](./references/broadcast-notifications.md)

## Workflow
1. Identify the notification context: session flash/toast notification, notification action, JavaScript notification, close event, positioning, database notification, database notification polling, or broadcast notification.
2. Run a narrow Context7 query for the exact Notifications topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented notification entry points confirmed for the task: `Notification::make()`, `send()`, `title()`, `body()`, `icon()`, `iconColor()`, `status()`, `success()`, `warning()`, `danger()`, `info()`, `color()`, `duration()`, `seconds()`, `persistent()`, `actions()`, `sendToDatabase()`, `toDatabase()`, `broadcast()`, and `toBroadcast()`.
5. For notification actions, use only documented `Filament\Actions\Action` methods confirmed by the lookup, such as `button()`, `color()`, `url()`, `dispatch()`, `dispatchSelf()`, `dispatchTo()`, `close()`, `markAsRead()`, and `markAsUnread()`.
6. For JavaScript notifications, use only documented `FilamentNotification`, `FilamentNotificationAction`, `window.FilamentNotification`, `window.FilamentNotificationAction`, import, and `close-notification` event patterns confirmed by the lookup.
7. For database notifications, include the notifications table, `databaseNotifications()`, `sendToDatabase()`, `toDatabase()`, `getDatabaseMessage()`, queue note, polling, sidebar position, read/unread actions, and modal opening only when the current lookup confirms them.
8. For broadcast notifications, include `broadcast()`, `toBroadcast()`, `getBroadcastMessage()`, Laravel Echo, server-side websockets, Filament config publishing, `broadcasting.echo`, `VITE_*` environment entries, and cache clearing only when the current lookup confirms them.
9. Finish by checking that every class, method, import, event name, enum, command, callback argument, and security warning in the answer is present in the Context7 result or loaded reference used for the task.

## Confirmed Core Patterns
- Notifications are sent with a `Notification` object built through a fluent API, and `send()` dispatches the notification and displays it in the application.
- The docs state that session flash notifications can be sent from anywhere in code, including JavaScript, not just Livewire components.
- Confirmed PHP namespace for notifications is `Filament\Notifications\Notification`.
- Confirmed status helpers are `status()`, `success()`, `warning()`, `danger()`, and `info()`.
- Confirmed display methods include `title()`, `body()`, `icon()`, `iconColor()`, `color()`, `duration()`, `seconds()`, and `persistent()`.
- Confirmed notification action class is `Filament\Actions\Action`.
- Confirmed notification action behavior includes opening URLs, dispatching Livewire events, closing notifications, and marking database notifications read or unread.
- Confirmed JavaScript objects are `FilamentNotification` and `FilamentNotificationAction`.
- Confirmed close event name is `close-notification` and documented database modal event uses `open-modal` with ID `database-notifications`.
- Confirmed panel methods include `databaseNotifications()` and `databaseNotificationsPolling()`.
- Confirmed database sending methods include `sendToDatabase()`, `toDatabase()`, and `getDatabaseMessage()`.
- Confirmed broadcast sending methods include `broadcast()`, `toBroadcast()`, and `getBroadcastMessage()`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup or the loaded official-doc reference file.
- Each class, method, command, event name, enum, import, and option is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, Laravel habits, or package source code.
- If the user asks for a Notifications topic not present in the current docs, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, event names, enum names, and configuration method names intact.