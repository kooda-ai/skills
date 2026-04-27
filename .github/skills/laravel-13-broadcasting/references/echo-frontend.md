# Echo And Frontend Consumers

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x broadcasting and notifications.

## Enabling Broadcasting With Reverb
The docs show enabling broadcasting with Laravel Reverb:

```shell
php artisan install:broadcasting --reverb
```

## Echo Configuration
The docs show configuring Echo for Reverb:

```javascript
import Echo from 'laravel-echo';

import Pusher from 'pusher-js';
window.Pusher = Pusher;

window.Echo = new Echo({
    broadcaster: 'reverb',
    key: import.meta.env.VITE_REVERB_APP_KEY,
    wsHost: import.meta.env.VITE_REVERB_HOST,
    wsPort: import.meta.env.VITE_REVERB_PORT ?? 80,
    wssPort: import.meta.env.VITE_REVERB_PORT ?? 443,
    forceTLS: (import.meta.env.VITE_REVERB_SCHEME ?? 'https') === 'https',
    enabledTransports: ['ws', 'wss'],
});
```

The docs also show configuring Echo for Pusher:

```javascript
import Echo from 'laravel-echo';

import Pusher from 'pusher-js';
window.Pusher = Pusher;

window.Echo = new Echo({
    broadcaster: 'pusher',
    key: import.meta.env.VITE_PUSHER_APP_KEY,
    cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
    forceTLS: true
});
```

The docs also show `configureEcho(...)` helpers for `@laravel/echo-react`, `@laravel/echo-vue`, and `@laravel/echo-svelte` with `broadcaster: 'reverb'`.

## Listening For Events
The docs show listening to a channel with Echo:

```javascript
Echo.channel(`orders.${this.order.id}`)
    .listen('OrderShipmentStatusUpdated', (e) => {
        console.log(e.order.name);
    });
```

The docs show `useEcho(...)` for React:

```javascript
import { useEcho } from "@laravel/echo-react";

useEcho(
    `orders.${orderId}`,
    "OrderShipmentStatusUpdated",
    (e) => {
        console.log(e.order);
    },
);
```

The docs also show `useEcho(...)` for Vue and Svelte.

## Notifications And Client Events
The docs show listening for notifications:

```javascript
Echo.private('App.Models.User.' + userId)
    .notification((notification) => {
        console.log(notification.type);
    });
```

The docs show `useEchoModel(...)` in React for notification listening.

The docs show client whisper events with `useEcho(...)`:

```javascript
import { useEcho } from "@laravel/echo-react";

const { channel } = useEcho(`chat.${roomId}`, ['update'], (e) => {
    console.log('Chat event received:', e);
});

channel().whisper('typing', { name: user.name });
```

The docs also show equivalent `whisper(...)` patterns for Vue and Svelte.

## Manual Channel Control
The docs show manual channel controls from Svelte `useEcho(...)`:

```svelte
<script>
import { useEcho } from "@laravel/echo-svelte";

const { leaveChannel, leave, stopListening, listen } = useEcho(
    `orders.${orderId}`,
    "OrderShipmentStatusUpdated",
    (e) => {
        console.log(e.order);
    },
);

// Stop listening without leaving channel...
stopListening();

// Start listening again...
listen();

// Leave channel...
leaveChannel();

// Leave a channel and also its associated private and presence channels...
leave();
</script>
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using custom Echo authorizers, Sanctum broadcasting authentication, presence join/here/leaving helpers, server-side Reverb operations, Ably configuration, auth endpoint customization, or frontend framework helpers not shown in the current Laravel 13 docs.