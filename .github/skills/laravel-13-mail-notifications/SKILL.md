---
name: laravel-13-mail-notifications
description: 'Use when: working with Laravel 13 mail, mailables, app/Mail, make:mail, Mailable classes, envelope(), content(), attachments(), Content view, attachable objects, mailable browser previews, notifications, app/Notifications, make:notification, via(), toMail(), MailMessage, toDatabase(), Notification facade, on-demand notifications, notification channels, queued notifications, ShouldQueue, Queueable, Mail::fake(), Mail::assertSent(), Mail::assertQueued(), Notification::fake(), Notification::assertSentTo(), and Laravel 13 mail/notification code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 mailable, notification, mail fake, notification fake, queued notification, or review task'
---

# Laravel 13 Mail And Notifications

## Purpose
Use this skill to create, review, or explain Laravel 13 mailables, notifications, queued notification delivery, and mail/notification tests using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, testing guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact mail or notification topic.
2. Do not add mail config keys, mailer names, exact `make:mail` shell syntax, mailable methods, envelope options, content options, attachment APIs, notification channels, notification message methods, queue behavior, fakes, assertions, commands, classes, namespaces, or generated paths unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, class names, facade names, channels, paths, and assertion names.
5. Do not infer behavior from older Laravel versions, mail provider docs, notification channel packages, queue docs beyond returned snippets, blog posts, source code, or general Laravel memory.

## Reference Map
- Mailables, `app/Mail`, `make:mail` command boundary, `content()`, `attachments()`, attachable objects, and browser previews: [mailables.md](./references/mailables.md)
- Notification generation, `app/Notifications`, `via()`, channels, `toMail()`, `MailMessage`, and on-demand notifications: [notifications.md](./references/notifications.md)
- `Mail::fake()`, mail assertions, queued mail assertions, `Notification::fake()`, notification assertions, and queued notifications with `ShouldQueue`: [testing-queues.md](./references/testing-queues.md)

## Workflow
1. Identify the exact surface: mailable generation, mailable content, mailable attachments, browser preview, notification generation, delivery channels, mail notification formatting, on-demand notification routes, queued notification, mail fake, notification fake, queued mail assertion, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented methods, facades, classes, paths, channel names, assertions, interfaces, traits, and examples.
5. For mailable topics not in the references, such as exact `make:mail` syntax, `envelope()` examples, recipients, from/reply-to, Markdown mail, attachments from storage/path/data, inline attachments, tags, metadata, queueing mailables, local development mail drivers, or mail configuration, rely on the fresh Context7 lookup.
6. For notification topics not in the references, such as database payload methods, broadcast formatting, Slack/Vonage details, mail customization, notification routing on notifiable models, notification localization, delays, middleware, after-commit behavior, or notification database table setup, rely on the fresh Context7 lookup.
7. For tests not in the references, such as closure-based mail assertions, notification channel-specific assertions, mail content assertions, or queued notification assertions beyond returned snippets, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unsupported method, unconfirmed channel, unconfirmed mailable/notification path, wrong facade assertion, missing documented interface/trait for queued notifications, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Each type of email is represented by a mailable class typically stored in `app/Mail`.
- The docs state the `app/Mail` directory is generated automatically when the first mailable is created with the `make:mail` Artisan command.
- Mailable classes are configured through methods including `envelope`, `content`, and `attachments`.
- The docs say `envelope` defines the email subject and recipients, while `content` specifies the Blade template for the message HTML content.
- `content(): Content` may return `new Content(view: 'mail.orders.shipped')`.
- `attachments(): array` may return attachable objects such as `[$this->photo]`.
- A mailable may be returned directly from a route closure or controller to preview rendered output in the browser.
- Notifications are represented by individual classes typically stored in `app/Notifications`.
- `php artisan make:notification InvoicePaid` is documented for generating a notification class.
- Notification classes define `via(...)` to specify delivery channels and channel-specific methods such as `toMail` or `toDatabase`.
- The docs show `via(object $notifiable): array` returning channels such as `mail`, `database`, and `vonage`.
- `toMail(object $notifiable): MailMessage` may return a `MailMessage` with `greeting()`, `line()`, `lineIf()`, `action()`, and `line()` calls.
- The `Notification` facade can send on-demand notifications using chained `route(...)` calls followed by `notify(...)`.
- The docs show on-demand routes for `mail`, `vonage`, `slack`, and `broadcast`.
- `Mail::fake()` prevents mail from being sent in tests, and the docs confirm assertions such as `assertNothingSent()`, `assertSent()`, `assertNotSent()`, `assertSentTimes()`, and `assertSentCount()`.
- Queued mailable assertions include `assertQueued()`, `assertNotQueued()`, `assertNothingQueued()`, and `assertQueuedCount()`.
- `Notification::fake()` prevents notifications from being sent in tests, and the docs confirm assertions such as `assertNothingSent()`, `assertSentTo()`, `assertNotSentTo()`, `assertSentTimes()`, and `assertCount()`.
- Queued notifications are documented by implementing `ShouldQueue` and using the `Queueable` trait on a notification class.

## Completion Check
- A fresh Context7 lookup was performed for the exact mail or notification topic.
- Every command, path, class, facade, method, channel, interface, trait, assertion, and queue behavior is traceable to the lookup or references.
- Exact mailable generation commands and mail configuration are not inferred when the current lookup did not return them.
- Unconfirmed mail/notification features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
