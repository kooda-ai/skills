# Filament 5 Notifications: Overview, Actions, JavaScript, And Positioning

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant notification overview, action, JavaScript, closing, or positioning topic.

## Sending Notifications
The docs state that notifications are sent using a `Notification` object constructed through a fluent API. Calling `send()` dispatches the notification and displays it in the application. Session flash notifications can be sent from anywhere in code, including JavaScript, not just Livewire components.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->send();
```

## Title
The main notification message is shown in the title. The title text can contain basic, safe HTML elements. The docs also show using `Str::markdown()` to generate safe HTML.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->send();
```

```php
title(Str::markdown('Saved **successfully**'))
```

The official docs warn that Filament's built-in HTML sanitizer permits inline `style` attributes for rich text formatting features. If content comes from untrusted users, consider restricting the default sanitizer configuration.

JavaScript equivalent:

```javascript
new FilamentNotification()
    .title('Saved successfully')
    .send()
```

## Icon And Icon Color
Notifications can have an icon displayed in front of the content. The icon color is gray by default and can be set with `iconColor()`.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->icon('heroicon-o-document-text')
    ->iconColor('success')
    ->send();
```

JavaScript equivalent:

```javascript
new FilamentNotification()
    .title('Saved successfully')
    .icon('heroicon-o-document-text')
    .iconColor('success')
    .send()
```

## Status
Notifications often have a status such as `success`, `warning`, `danger`, or `info`. The docs confirm `status()` and the dedicated `success()`, `warning()`, `danger()`, and `info()` methods for setting corresponding icons and colors.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->send();
```

JavaScript equivalent:

```javascript
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .send()
```

## Background Color
Notifications have no background color by default. The docs confirm `color()` for setting one.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->color('success')
    ->send();
```

JavaScript equivalent:

```javascript
new FilamentNotification()
    .title('Saved successfully')
    .color('success')
    .send()
```

## Duration And Persistence
By default, notifications are shown for 6 seconds before automatically closing. The docs confirm custom durations in milliseconds with `duration()` and in seconds with `seconds()`. The docs confirm `persistent()` for notifications that require the user to close them manually.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->duration(5000)
    ->send();
```

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->seconds(5)
    ->send();
```

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->persistent()
    ->send();
```

JavaScript equivalents use `.duration(5000)`, `.seconds(5)`, and `.persistent()`.

## Body Text
Additional notification text can be shown with `body()`. The body text can contain basic, safe HTML elements. The docs also show using `Str::markdown()` to generate safe HTML.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->send();
```

```php
body(Str::markdown('Changes to the **post** have been saved.'))
```

JavaScript equivalent:

```javascript
new FilamentNotification()
    .title('Saved successfully')
    .success()
    .body('Changes to the post have been saved.')
    .send()
```

## Notification Actions
Notifications support actions, which are buttons rendered below the notification content. The docs confirm actions that open URLs, dispatch Livewire events, and close the notification.

```php
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button(),
        Action::make('undo')
            ->color('gray'),
    ])
    ->send();
```

## Opening URLs From Actions
The docs confirm `url()` for opening a URL, optionally in a new tab with `shouldOpenInNewTab: true`.

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
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray'),
    ])
    ->send();
```

The official docs warn that user-controlled data passed to `url()` should be validated so the URL does not use a dangerous scheme such as `javascript:` or `data:`.

JavaScript equivalent uses `new FilamentNotificationAction('view')->button()->url('/view')->openUrlInNewTab()`.

## Dispatching Livewire Events From Actions
The docs confirm `dispatch()` with optional data. They also confirm `dispatchSelf()` and `dispatchTo()`.

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
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray')
            ->dispatch('undoEditingPost', [$post->id]),
    ])
    ->send();
```

```php
Action::make('undo')
    ->color('gray')
    ->dispatchSelf('undoEditingPost', [$post->id])

Action::make('undo')
    ->color('gray')
    ->dispatchTo('another_component', 'undoEditingPost', [$post->id])
```

JavaScript equivalents use `.dispatch('undoEditingPost')`, `.dispatchSelf('undoEditingPost')`, and `.dispatchTo('another_component', 'undoEditingPost')`.

## Closing Notifications From Actions
The docs confirm `close()` for closing a notification after opening a URL or dispatching an event.

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
            ->url(route('posts.show', $post), shouldOpenInNewTab: true),
        Action::make('undo')
            ->color('gray')
            ->dispatch('undoEditingPost', [$post->id])
            ->close(),
    ])
    ->send();
```

JavaScript equivalent chains `.close()` on `FilamentNotificationAction`.

## JavaScript Objects
The docs state that `FilamentNotification` and `FilamentNotificationAction` are assigned to `window.FilamentNotification` and `window.FilamentNotificationAction`, so they are available in on-page scripts. The docs also show importing bundled JavaScript objects:

```javascript
import { Notification, NotificationAction } from '../../vendor/filament/notifications/dist/index.js'
```

## Closing A Notification With JavaScript
The docs confirm dispatching a browser event on `window` called `close-notification`. The event must contain the ID of the notification. The ID can be retrieved with `getId()`.

```php
use Filament\Notifications\Notification;

$notification = Notification::make()
    ->title('Hello')
    ->persistent()
    ->send()

$notificationId = $notification->getId()
```

```php
$this->dispatch('close-notification', id: $notificationId);
```

```html
<button x-on:click="$dispatch('close-notification', { id: notificationId })" type="button">
    Close Notification
</button>
```

The docs recommend using the generated ID when possible. If the random ID cannot be persisted, a custom ID can be passed to `Notification::make()`:

```php
use Filament\Notifications\Notification;

Notification::make('greeting')
    ->title('Hello')
    ->persistent()
    ->send()
```

```html
<button x-on:click="$dispatch('close-notification', { id: 'greeting' })" type="button">
    Close Notification
</button>
```

The docs warn that sending multiple notifications with the same ID may cause unexpected side effects, so random IDs are recommended.

## Positioning Notifications
The docs confirm configuring notification alignment in a service provider or middleware using `Notifications::alignment()` and `Notifications::verticalAlignment()`. Confirmed enum values are `Alignment::Start`, `Alignment::Center`, `Alignment::End`, `VerticalAlignment::Start`, `VerticalAlignment::Center`, and `VerticalAlignment::End`.

```php
use Filament\Notifications\Livewire\Notifications;
use Filament\Support\Enums\Alignment;
use Filament\Support\Enums\VerticalAlignment;

Notifications::alignment(Alignment::Start);
Notifications::verticalAlignment(VerticalAlignment::End);
```