# Channel Authorization

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x channel authorization.

## Defining Authorization Callbacks
The docs show defining channel authorization in `routes/channels.php` with `Broadcast::channel(...)`:

```php
use App\Models\Order;
use App\Models\User;

Broadcast::channel('orders.{orderId}', function (User $user, int $orderId) {
    return $user->id === Order::findOrNew($orderId)->user_id;
});
```

The docs state channel callbacks receive the authenticated user and any wildcard parameters from the channel name.

## Model Binding In Channel Callbacks
The docs show model binding in channel authorization:

```php
use App\Models\Order;
use App\Models\User;

Broadcast::channel('orders.{order}', function (User $user, Order $order) {
    return $user->id === $order->user_id;
});
```

The docs state channel callbacks support model binding similar to HTTP routes, but implicit model binding scoping is not supported for channel model binding.

## Presence Channel Authorization Data
The docs show returning user data from a presence channel authorization callback:

```php
use App\Models\User;

Broadcast::channel('chat.{roomId}', function (User $user, int $roomId) {
    if ($user->canJoinRoom($roomId)) {
        return ['id' => $user->id, 'name' => $user->name];
    }
});
```

The docs state the returned array is available to JavaScript event listeners.

## Channel Classes
The docs show generating a channel class:

```shell
php artisan make:channel OrderChannel
```

The docs state the class is created in `App/Broadcasting`.

The docs show registering the channel class in `routes/channels.php`:

```php
Broadcast::channel('orders.{order}', OrderChannel::class);
```

The docs show authorization logic in the `join(...)` method:

```php
<?php

namespace App\Broadcasting;

use App\Models\Order;
use App\Models\User;

class OrderChannel
{
    /**
     * Create a new channel instance.
     */
    public function __construct() {}

    /**
     * Authenticate the user's access to the channel.
     */
    public function join(User $user, Order $order): array|bool
    {
        return $user->id === $order->user_id;
    }
}
```

The docs state channel classes may leverage the service container for dependency injection.

## Route Bootstrap And Inspection
The docs show registering channel routes through routing bootstrap when needed:

```php
->withRouting(
    web: __DIR__.'/../routes/web.php',
    channels: __DIR__.'/../routes/channels.php',
    health: '/up',
)
```

The docs show listing broadcast authorization callbacks:

```shell
php artisan channel:list
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using custom broadcasting auth endpoints, middleware customization for broadcasting routes, channel authorization tests, presence-channel membership lifecycle APIs, or imports that were malformed in the returned docs.