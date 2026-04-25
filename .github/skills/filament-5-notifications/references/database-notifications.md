# Filament 5 Notifications: Database Notifications

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant database notifications topic.

## Notifications Table
The docs state that the Laravel notifications table must be added before using database notifications.

```bash
php artisan make:notifications-table
```

The docs note that PostgreSQL users should make sure the `data` column in the migration uses `json()`: `$table->json('data')`. For UUID user models, the docs say the `notifiable` column should use `uuidMorphs()`: `$table->uuidMorphs('notifiable')`.

## Enabling Database Notifications In A Panel
The docs confirm `databaseNotifications()` in panel configuration.

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->databaseNotifications();
}
```

## Sending Database Notifications
The docs confirm sending database notifications through the fluent API with `sendToDatabase($recipient)`.

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

Notification::make()
    ->title('Saved successfully')
    ->sendToDatabase($recipient);
```

The docs also confirm using `notify()` on the recipient model with `toDatabase()`.

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

$recipient->notify(
    Notification::make()
        ->title('Saved successfully')
        ->toDatabase(),
);
```

The docs state that Laravel sends database notifications using the queue, so the queue must be running to receive the notifications.

The docs also confirm returning the notification from a traditional Laravel notification class `toDatabase()` method with `getDatabaseMessage()`.

```php
use App\Models\User;
use Filament\Notifications\Notification;

public function toDatabase(User $notifiable): array
{
    return Notification::make()
        ->title('Saved successfully')
        ->getDatabaseMessage();
}
```

## Sidebar Position
By default, the database notifications trigger is positioned in the topbar. If the topbar is disabled, it is added to the sidebar. The docs confirm moving it to the sidebar by passing a `position` argument to `databaseNotifications()`.

```php
use Filament\Enums\DatabaseNotificationsPosition;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->databaseNotifications(position: DatabaseNotificationsPosition::Sidebar);
}
```

## Receiving Database Notifications
The docs state that, without setup, new database notifications are only received when the page is first loaded.

## Polling
The docs state that Livewire polls for new notifications every 30 seconds by default. The docs confirm `databaseNotificationsPolling('30s')` and `databaseNotificationsPolling(null)`.

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->databaseNotifications()
        ->databaseNotificationsPolling('30s');
}
```

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->databaseNotifications()
        ->databaseNotificationsPolling(null);
}
```

## Websocket Event For Database Notifications
The docs state that websockets must be configured in the panel first. Once websockets are set up, setting `isEventDispatched: true` when sending the notification automatically dispatches a `DatabaseNotificationsSent` event and triggers immediate fetching of new notifications for the user.

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

Notification::make()
    ->title('Saved successfully')
    ->sendToDatabase($recipient, isEventDispatched: true);
```

## Marking Database Notifications As Read Or Unread
The docs state that there is a button at the top of the modal to mark all notifications as read at once. They also confirm adding notification actions to mark individual notifications as read with `markAsRead()` or unread with `markAsUnread()`.

```php
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button()
            ->markAsRead(),
    ])
    ->send();
```

```php
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('markAsUnread')
            ->button()
            ->markAsUnread(),
    ])
    ->send();
```

## Opening The Database Notifications Modal
The docs confirm opening the database notifications modal by dispatching an `open-modal` browser event with the ID `database-notifications`.

```html
<button
    x-data="{}"
    x-on:click="$dispatch('open-modal', { id: 'database-notifications' })"
    type="button"
>
    Notifications
</button>
```