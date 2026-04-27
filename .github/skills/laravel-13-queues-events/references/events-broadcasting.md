# Events And Broadcasting

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x events, listeners, subscribers, broadcasting, channel authorization, Laravel Echo, and notification listening.

## Generating Events And Listeners
The docs confirm these Artisan commands:

```shell
php artisan make:event PodcastProcessed

php artisan make:listener SendPodcastNotification --event=PodcastProcessed
```

The docs also show interactive forms:

```shell
php artisan make:event

php artisan make:listener
```

## Listener `handle()` Methods
The docs show a basic listener:

```php
<?php

namespace App\Listeners;

use App\Events\OrderShipped;

class SendShipmentNotification
{
    /**
     * Create the event listener.
     */
    public function __construct() {}

    /**
     * Handle the event.
     */
    public function handle(OrderShipped $event): void
    {
        // Access the order using $event->order...
    }
}
```

The docs show another listener handle method:

```php
use App\Events\PodcastProcessed;

class SendPodcastNotification
{
    /**
     * Handle the event.
     */
    public function handle(PodcastProcessed $event): void
    {
        // ...
    }
}
```

The docs show a listener handling multiple events with a union type:

```php
/**
 * Handle the event.
 */
public function handle(PodcastProcessed|PodcastPublished $event): void
{
    // ...
}
```

## Event Discovery
The docs state Laravel automatically discovers event listeners by scanning the application's `Listeners` directory. It identifies methods starting with `handle` or `__invoke` and registers them based on the type-hinted event in the method signature.

The docs state multiple events may be listened to simultaneously using PHP union types in the listener method.

## Event Subscribers
The docs show a subscriber returning an event-to-method map from `subscribe(...)`:

```php
<?php

namespace App\Listeners;

use Illuminate\Auth\Events\Login;
use Illuminate\Auth\Events\Logout;
use Illuminate\Events\Dispatcher;

class UserEventSubscriber
{
    /**
     * Handle user login events.
     */
    public function handleUserLogin(Login $event): void {}

    /**
     * Handle user logout events.
     */
    public function handleUserLogout(Logout $event): void {}

    /**
     * Register the listeners for the subscriber.
     *
     * @return array<string, string>
     */
    public function subscribe(Dispatcher $events): array
    {
        return [
            Login::class => 'handleUserLogin',
            Logout::class => 'handleUserLogout',
        ];
    }
}
```

Confirmed classes and methods: `Illuminate\Auth\Events\Login`, `Illuminate\Auth\Events\Logout`, `Illuminate\Events\Dispatcher`, and `subscribe(Dispatcher $events): array`.

## Broadcast Events
The docs state event broadcasting requires an event class to implement `ShouldBroadcast` and define `broadcastOn()`, which returns the channel or array of channels where the event should be broadcast. The docs state channels may be public, private, or presence-based, and private/presence channels require additional authorization.

The docs show:

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

Confirmed classes and methods: `ShouldBroadcast`, `broadcastOn(): array`, `PrivateChannel`, and `SerializesModels`.

## Channel Authorization
The docs show private channel authorization in `routes/channels.php` using `Broadcast::channel(...)`:

```php
use App\Models\User;

Broadcast::channel('orders.{orderId}', function (User $user, int $orderId) {
    return $user->id === Order::findOrNew($orderId)->user_id;
});
```

Run a narrower lookup before adding the import for `Broadcast` or `Order`, since the current returned snippet did not include them.

## Laravel Echo Listening
The docs show listening for broadcast events with Echo:

```javascript
Echo.channel(`orders.${this.order.id}`)
    .listen('OrderShipmentStatusUpdated', (e) => {
        console.log(e.order.name);
    });
```

The docs show listening for notifications with Echo:

```javascript
Echo.private('App.Models.User.' + userId)
    .notification((notification) => {
        console.log(notification.type);
    });
```

Confirmed Echo methods: `channel(...)`, `listen(...)`, `private(...)`, and `notification(...)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using event dispatch helpers, event classes beyond shown snippets, manual event registration, queued listeners, listener middleware, wildcard listeners, subscriber registration, event tests, broadcast routes, broadcasting driver setup, Reverb/Pusher/Ably configuration, Echo installation, presence channel authorization, `broadcastAs()`, `broadcastWith()`, `ShouldBroadcastNow`, notification broadcasting setup, or channel authorization model binding.
