# Notifications

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x notifications.

## Notification Classes
The docs state notifications are represented by individual classes typically stored in the `app/Notifications` directory.

The docs confirm this Artisan command:

```shell
php artisan make:notification InvoicePaid
```

The docs state each notification class defines a `via` method to specify delivery channels and specific message-building methods for each channel, such as `toMail` or `toDatabase`.

## Delivery Channels
The docs show a `via(...)` method:

```php
/**
 * Get the notification's delivery channels.
 *
 * @return array<int, string>
 */
public function via(object $notifiable): array
{
    return $notifiable->prefers_sms ? ['vonage'] : ['mail', 'database'];
}
```

Confirmed channels from this snippet: `vonage`, `mail`, and `database`.

## Mail Notifications
The docs show a `toMail(...)` method returning `MailMessage`:

```php
/**
 * Get the mail representation of the notification.
 */
public function toMail(object $notifiable): MailMessage
{
    $url = url('/invoice/'.$this->invoice->id);

    return (new MailMessage)
        ->greeting('Hello!')
        ->line('One of your invoices has been paid!')
        ->lineIf($this->amount > 0, "Amount paid: {$this->amount}")
        ->action('View Invoice', $url)
        ->line('Thank you for using our application!');
}
```

Confirmed methods and helpers from this snippet: `toMail(object $notifiable): MailMessage`, `url(...)`, `greeting(...)`, `line(...)`, `lineIf(...)`, and `action(...)`.

## On-Demand Notifications
The docs show sending on-demand notifications through multiple channels with the `Notification` facade:

```php
use Illuminate\Broadcasting\Channel;
use Illuminate\Support\Facades\Notification;

Notification::route('mail', 'taylor@example.com')
    ->route('vonage', '5555555555')
    ->route('slack', '#slack-channel')
    ->route('broadcast', [new Channel('channel-name')])
    ->notify(new InvoicePaid($invoice));
```

Confirmed classes, channels, and methods from this snippet: `Illuminate\Support\Facades\Notification`, `Illuminate\Broadcasting\Channel`, `route(...)`, `notify(...)`, `mail`, `vonage`, `slack`, and `broadcast`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using notification sending via notifiable models, `notify()` on users, `Notification::send(...)`, database notification payloads, `toDatabase`, `toArray`, broadcast notification formatting, Slack/Vonage setup, notification routing methods on notifiable models, localization, delays, queues beyond the queued notification reference, middleware, after-commit behavior, database table migrations, or notification mail customization.
