# Testing And Queues

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x mail testing, queued mail assertions, notification testing, and queued notifications.

## Mail Fakes And Sent Assertions
The docs show `Mail::fake()` preventing mail from being sent and then asserting mailables were instructed to be sent:

```php
<?php

use App\Mail\OrderShipped;
use Illuminate\Support\Facades\Mail;

test('orders can be shipped', function () {
    Mail::fake();

    // Perform order shipping...

    // Assert that no mailables were sent...
    Mail::assertNothingSent();

    // Assert that a mailable was sent...
    Mail::assertSent(OrderShipped::class);

    // Assert a mailable was sent twice...
    Mail::assertSent(OrderShipped::class, 2);

    // Assert a mailable was sent to an email address...
    Mail::assertSent(OrderShipped::class, 'example@laravel.com');

    // Assert a mailable was sent to multiple email addresses...
    Mail::assertSent(OrderShipped::class, ['example@laravel.com', '...']);

    // Assert a mailable was not sent...
    Mail::assertNotSent(AnotherMailable::class);

    // Assert a mailable was sent twice...
    Mail::assertSentTimes(OrderShipped::class, 2);

    // Assert 3 total mailables were sent...
    Mail::assertSentCount(3);
});
```

Confirmed facade and assertions: `Illuminate\Support\Facades\Mail`, `Mail::fake()`, `Mail::assertNothingSent()`, `Mail::assertSent(...)`, `Mail::assertNotSent(...)`, `Mail::assertSentTimes(...)`, and `Mail::assertSentCount(...)`.

## Queued Mailable Assertions
The docs show queued mailable assertions:

```php
Mail::assertQueued(OrderShipped::class);
Mail::assertNotQueued(OrderShipped::class);
Mail::assertNothingQueued();
Mail::assertQueuedCount(3);
```

Use these instead of `assertSent` when mailables are queued for background delivery according to the docs.

## Notification Fakes And Assertions
The docs show `Notification::fake()` in a PHPUnit test:

```php
<?php

namespace Tests\Feature;

use App\Notifications\OrderShipped;
use Illuminate\Support\Facades\Notification;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function test_orders_can_be_shipped(): void
    {
        Notification::fake();

        // Perform order shipping...

        // Assert that no notifications were sent...
        Notification::assertNothingSent();

        // Assert a notification was sent to the given users...
        Notification::assertSentTo(
            [$user], OrderShipped::class
        );

        // Assert a notification was not sent...
        Notification::assertNotSentTo(
            [$user], AnotherNotification::class
        );

        // Assert a notification was sent twice...
        Notification::assertSentTimes(WeeklyReminder::class, 2);

        // Assert that a given number of notifications were sent...
        Notification::assertCount(3);
    }
}
```

Confirmed facade and assertions: `Illuminate\Support\Facades\Notification`, `Notification::fake()`, `Notification::assertNothingSent()`, `Notification::assertSentTo(...)`, `Notification::assertNotSentTo(...)`, `Notification::assertSentTimes(...)`, and `Notification::assertCount(...)`.

## Queued Notifications
The docs show enabling asynchronous notification delivery by implementing `ShouldQueue` and using the `Queueable` trait:

```php
<?php

namespace App\Notifications;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Notifications\Notification;

class InvoicePaid extends Notification implements ShouldQueue
{
    use Queueable;

    // ...
}
```

Confirmed classes and interfaces: `Illuminate\Bus\Queueable`, `Illuminate\Contracts\Queue\ShouldQueue`, and `Illuminate\Notifications\Notification`.

## MCP Notification Assertion Boundary
The current Context7 result returned `assertSentNotification(...)` and `assertNotificationCount(...)` from the Laravel MCP docs. Do not apply those to ordinary Laravel notification tests unless the user's task is specifically about Laravel MCP or a fresh lookup confirms the context.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using mail content assertions, closure-based mail assertions, queued mailable metadata assertions, notification channel assertions, notification closures, anonymous notifiables in tests, database notification assertions, broadcast notification assertions, queued notification assertions beyond implementing `ShouldQueue`, delays, or queue interaction assertions.
