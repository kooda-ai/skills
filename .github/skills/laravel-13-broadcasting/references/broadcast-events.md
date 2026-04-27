# Broadcast Events

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x broadcasting events.

## Implementing Broadcastable Events
The docs show implementing `ShouldBroadcast` on an event class:

```php
<?php

namespace App\Events;

use App\Models\User;
use Illuminate\Broadcasting\Channel;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Broadcasting\PresenceChannel;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Queue\SerializesModels;

class ServerCreated implements ShouldBroadcast
{
    use SerializesModels;

    /**
     * Create a new event instance.
     */
    public function __construct(
        public User $user,
    ) {}

    /**
     * Get the channels the event should broadcast on.
     *
     * @return array<int, \Illuminate\Broadcasting\Channel>
     */
    public function broadcastOn(): array
    {
        return [
            new PrivateChannel('user.'.$this->user->id),
        ];
    }
}
```

Confirmed classes and methods: `ShouldBroadcast`, `PrivateChannel`, `PresenceChannel`, `InteractsWithSockets`, `SerializesModels`, and `broadcastOn(): array`.

## Presence Channels
The docs show returning a `PresenceChannel` from `broadcastOn()`:

```php
/**
 * Get the channels the event should broadcast on.
 *
 * @return array<int, \Illuminate\Broadcasting\Channel>
 */
public function broadcastOn(): array
{
    return [
        new PresenceChannel('chat.'.$this->message->room_id),
    ];
}
```

The docs also show returning multiple channels, including multiple private channels, from `broadcastOn()`.

## Broadcasting Immediately
The docs show implementing `ShouldBroadcastNow` for synchronous broadcasting:

```php
<?php

namespace App\Events;

use Illuminate\Contracts\Broadcasting\ShouldBroadcastNow;

class OrderShipmentStatusUpdated implements ShouldBroadcastNow
{
    // ...
```

## Custom Event Names And Payloads
The docs show overriding the broadcast name:

```php
/**
 * The event's broadcast name.
 */
public function broadcastAs(): string
{
    return 'server.created';
}
```

The docs show overriding the broadcast payload:

```php
/**
 * Get the data to broadcast.
 *
 * @return array<string, mixed>
 */
public function broadcastWith(): array
{
    return ['id' => $this->user->id];
}
```

The docs state `broadcastWith()` returns specific data instead of all public properties.

## Conditional Broadcasting
The docs show `broadcastWhen()`:

```php
/**
 * Determine if this event should broadcast.
 */
public function broadcastWhen(): bool
{
    return $this->order->value > 100;
}
```

## Excluding The Current User
The docs show excluding the current user with the `broadcast` helper:

```php
broadcast(new NewMessage($message));
```

```php
broadcast(new NewMessage($message))->toOthers();
```

## Selecting A Broadcast Connection
The docs show selecting a broadcast connection at dispatch time:

```php
use App\Events\OrderShipmentStatusUpdated;

broadcast(new OrderShipmentStatusUpdated($update))->via('pusher');
```

The docs also show selecting the connection inside the event class with `InteractsWithBroadcasting`:

```php
<?php

namespace App\Events;

use Illuminate\Broadcasting\Channel;
use Illuminate\Broadcasting\InteractsWithBroadcasting;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Broadcasting\PresenceChannel;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Queue\SerializesModels;

class OrderShipmentStatusUpdated implements ShouldBroadcast
{
    use InteractsWithBroadcasting;

    /**
     * Create a new event instance.
     */
    public function __construct()
    {
        $this->broadcastVia('pusher');
    }
}
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using undocumented queue-selection APIs for broadcast events, additional broadcaster connections, `broadcastQueue` properties, testing helpers, model broadcasting beyond the returned snippets, or `InteractsWithSockets` method calls not shown in the current lookup.