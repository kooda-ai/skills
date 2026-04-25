# Filament 5 Notifications: Broadcast Notifications

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant broadcast notifications topic.

## Introduction
The docs state that Filament sends flash notifications through the Laravel session by default. Broadcast notifications can be used to send notifications to a user in real time, such as a temporary success notification from a queued job after processing finishes.

The docs state that Filament has a native integration with Laravel Echo. Echo must be installed, along with a server-side websockets integration such as Pusher.

## Sending Broadcast Notifications
The docs confirm sending broadcast notifications through the fluent API with `broadcast($recipient)`.

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

Notification::make()
    ->title('Saved successfully')
    ->broadcast($recipient);
```

The docs also confirm using `notify()` on the recipient model with `toBroadcast()`.

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

$recipient->notify(
    Notification::make()
        ->title('Saved successfully')
        ->toBroadcast(),
)
```

The docs confirm returning the notification from a traditional Laravel notification class `toBroadcast()` method with `getBroadcastMessage()`.

```php
use App\Models\User;
use Filament\Notifications\Notification;
use Illuminate\Notifications\Messages\BroadcastMessage;

public function toBroadcast(User $notifiable): BroadcastMessage
{
    return Notification::make()
        ->title('Saved successfully')
        ->getBroadcastMessage();
}
```

## Setting Up Websockets In A Panel
The docs state that the Panel Builder has built-in support for real-time broadcast and database notifications, but several setup steps are required.

Confirmed setup steps from the docs:

1. Read Laravel broadcasting documentation if needed.
2. Install and configure broadcasting to use a server-side websockets integration such as Pusher.
3. Publish the Filament package configuration.

```bash
php artisan vendor:publish --tag=filament-config
```

4. Edit `config/filament.php` and uncomment the `broadcasting.echo` section, making sure the settings are configured for the broadcasting installation.
5. Ensure the relevant `VITE_*` entries exist in the `.env` file.
6. Clear relevant caches so the new configuration takes effect.

```bash
php artisan route:clear
php artisan config:clear
```

The docs state that the panel should then connect to the broadcasting service, and Pusher debug console should show an incoming connection each time a page loads when Pusher is used.