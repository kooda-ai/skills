# Mailables

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x mailables.

## Mailable Classes
The docs state each type of email in a Laravel application is represented by a mailable class, typically stored in the `app/Mail` directory.

The docs state that if `app/Mail` does not exist, it is automatically generated when the first mailable is created using the `make:mail` Artisan command.

The current lookup confirmed the `make:mail` command name in prose but did not return an exact shell snippet. Run a narrower Context7 lookup before writing exact `php artisan make:mail ...` commands or flags.

## Writing Mailables
The docs state mailable classes are configured through several methods, including `envelope`, `content`, and `attachments`.

The docs state:

- `envelope` defines the email subject and recipients.
- `content` specifies the Blade template used for generating the message's HTML content.
- `attachments` defines message attachments.

Run a narrower lookup before using exact `envelope()` examples, recipient APIs, sender APIs, reply-to APIs, tags, metadata, or queueing mailables.

## Content View
The docs show the `content()` method returning `Content` with a Blade view name:

```php
/**
 * Get the message content definition.
 */
public function content(): Content
{
    return new Content(
        view: 'mail.orders.shipped',
    );
}
```

Confirmed method and class names from this snippet: `content(): Content` and `new Content(view: ...)`.

## Attachments
The docs show returning attachable objects from the `attachments()` method:

```php
/**
 * Get the attachments for the message.
 *
 * @return array<int, \Illuminate\Mail\Mailables\Attachment>
 */
public function attachments(): array
{
    return [$this->photo];
}
```

Confirmed details: `attachments(): array`, `Illuminate\Mail\Mailables\Attachment`, and returning attachable objects such as `$this->photo`.

## Browser Preview
The docs show returning a mailable directly from a route closure or controller to preview rendered output in the browser:

```php
Route::get('/mailable', function () {
    $invoice = App\Models\Invoice::find(1);

    return new App\Mail\InvoicePaid($invoice);
});
```

Confirmed classes and methods from this snippet: `App\Models\Invoice::find(1)` and `new App\Mail\InvoicePaid($invoice)`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using exact `make:mail` command syntax, `Envelope` examples, subject/from/to/cc/bcc/reply-to APIs, Markdown mailables, text views, attachments from path/storage/data, inline attachments, rendering mailables, sending mail with the `Mail` facade, queueing mailables, mail configuration, mail transports, or local mail development tools.
