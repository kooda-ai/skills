---
name: laravel-13-queues-events
description: 'Use when: working with Laravel 13 queues, jobs, make:job, ShouldQueue, job handle(), dispatch(), onQueue(), onConnection(), make:job-middleware, queue workers, queue:work, --tries, --backoff, Supervisor worker config, queue:failed, queue:retry, failed jobs, events, listeners, make:event, make:listener, listener handle(), event discovery, event subscribers, and Laravel 13 queue/event code reviews. Use laravel-13-broadcasting for dedicated broadcasting work. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 queue, job, worker, failed job, event, listener, subscriber, broadcast, or review task'
---

# Laravel 13 Queues And Events

## Purpose
Use this skill to create, review, or explain Laravel 13 queue, job, worker, event, listener, and subscriber code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, operations guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact queue, job, worker, event, listener, or subscriber topic.
2. Do not add queue config keys, driver names, worker flags, job properties, retry/backoff behavior, batching/chaining APIs, failed-job tables, event dispatching helpers, listener registration rules, commands, classes, methods, or interfaces unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, flags, interfaces, class names, method names, channels, and package names.
5. Do not infer behavior from older Laravel versions, Horizon docs beyond returned snippets, queue driver docs, broadcasting provider docs, frontend framework docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Job generation, `ShouldQueue`, static `dispatch()`, constructor arguments, `onQueue()`, `onConnection()`, and job middleware generation: [jobs-dispatching.md](./references/jobs-dispatching.md)
- Failed-job commands, queue worker retry backoff option, and Supervisor worker config: [workers-failed-jobs.md](./references/workers-failed-jobs.md)
- Event/listener generation, listener `handle()`, event discovery, subscribers, and broadcasting boundaries: [events-broadcasting.md](./references/events-broadcasting.md)

## Workflow
1. Identify the exact surface: job generation, job dispatch, queue selection, connection selection, job middleware, worker command, retry/backoff option, failed jobs, Supervisor config, event generation, listener generation, listener handle method, event discovery, subscriber mapping, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, imports, interfaces, methods, flags, channel names, and examples.
5. For queue topics not in the references, such as queue connection configuration, `queue:listen`, job classes in full, job `handle()` dependencies, delayed dispatch, chains, batches, unique jobs, rate limiting, manual failed-job setup, pruning failed jobs, worker deployment beyond the shown Supervisor example, or Horizon configuration beyond the returned timeout snippet, rely on the fresh Context7 lookup.
6. For event topics not in the references, such as event dispatch helpers, event classes, queued listeners, listener middleware, wildcard listeners, manual listener registration, subscribers beyond returned array mapping, or testing events, rely on the fresh Context7 lookup.
7. Route dedicated broadcasting work to `laravel-13-broadcasting` when the task is about broadcastable events, channels, Echo consumers, or broadcaster setup.
8. For reviews, flag only documented mismatches: unsupported command, unconfirmed flag, unconfirmed queue or event method, missing documented interface, wrong listener signature, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- `php artisan make:job ProcessPodcast` generates a queueable job class, and the docs say the generated class automatically implements `ShouldQueue`.
- Jobs may be dispatched with `ProcessPodcast::dispatch()` or `ProcessPodcast::dispatch($podcast)`.
- `ProcessPodcast::dispatch()->onQueue('emails')` dispatches to the default connection's `emails` queue in the documented example.
- `ProcessPodcast::dispatch($podcast)->onConnection('sqs')->onQueue('processing')` is documented for selecting connection and queue.
- The docs state job middleware can be generated with `php artisan make:job-middleware` and attached by returning middleware from a job's `middleware` method.
- The docs confirm `php artisan queue:failed`, `php artisan queue:retry <id>`, `php artisan queue:retry --queue=name`, and `php artisan queue:retry all` for failed-job inspection and retry.
- `php artisan queue:work redis --tries=3 --backoff=3` is documented for setting retry backoff delay.
- The docs show a Supervisor program named `laravel-worker` with `queue:work --sleep=3 --tries=3 --max-time=3600`.
- `php artisan make:event PodcastProcessed` and `php artisan make:listener SendPodcastNotification --event=PodcastProcessed` are documented.
- Listener `handle(...)` methods type-hint events such as `OrderShipped` or `PodcastProcessed` and return `void` in the documented examples.
- Event discovery scans the application's `Listeners` directory and registers methods starting with `handle` or `__invoke` based on type-hinted events.
- Listeners may listen to multiple events through PHP union types in the documented example.
- Subscribers may return an array mapping event classes to handler method names from `subscribe(Dispatcher $events): array`.
- Use `laravel-13-broadcasting` when the task needs concrete broadcasting event classes, channel authorization logic, Echo setup, or frontend broadcast consumers.

## Completion Check
- A fresh Context7 lookup was performed for the exact queue, job, worker, event, listener, or subscriber topic.
- Every command, flag, class, interface, method, queue name, connection name, and operational instruction is traceable to the lookup or references.
- Broadcasting provider, Echo setup, and channel authorization details are delegated to `laravel-13-broadcasting`.
- Unconfirmed queue/event features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
