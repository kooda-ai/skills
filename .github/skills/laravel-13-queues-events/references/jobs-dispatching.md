# Jobs And Dispatching

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x queues and jobs.

## Generating Queueable Jobs
The docs confirm this Artisan command:

```shell
php artisan make:job ProcessPodcast
```

The docs state the generated class automatically implements `ShouldQueue`.

Run a narrower Context7 lookup before using the exact generated class body, namespace, traits, job properties, constructor shape, or `handle()` method body.

## Dispatching Jobs
The docs show dispatching a job to the default queue:

```php
use App\Jobs\ProcessPodcast;

// This job is sent to the default connection's default queue...
ProcessPodcast::dispatch();
```

The docs show dispatching to a specific named queue:

```php
// This job is sent to the default connection's "emails" queue...
ProcessPodcast::dispatch()->onQueue('emails');
```

Confirmed methods: `dispatch()` and `onQueue(...)`.

## Dispatching With Constructor Arguments
The docs show passing a model to a job constructor through the static `dispatch` method:

```php
<?php

namespace App\Http\Controllers;

use App\Jobs\ProcessPodcast;
use App\Models\Podcast;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;

class PodcastController extends Controller
{
    /**
     * Store a new podcast.
     */
    public function store(Request $request): RedirectResponse
    {
        $podcast = Podcast::create(/* ... */);

        // ...

        ProcessPodcast::dispatch($podcast);

        return redirect('/podcasts');
    }
}
```

Confirmed classes and methods: `App\Jobs\ProcessPodcast`, `App\Models\Podcast`, `ProcessPodcast::dispatch($podcast)`, and `Podcast::create(...)`.

## Selecting Connection And Queue
The docs show chaining `onConnection(...)` and `onQueue(...)`:

```php
ProcessPodcast::dispatch($podcast)
    ->onConnection('sqs')
    ->onQueue('processing');
```

Confirmed connection and queue names from this example: `sqs` and `processing`.

## Job Middleware
The docs state job middleware can be generated with:

```shell
php artisan make:job-middleware
```

The docs state job middleware may be attached to a job by returning middleware from the job's `middleware` method. The docs note the method may need to be added manually if it is not present.

Run a narrower Context7 lookup before adding job middleware class names, method signatures, middleware examples, or command arguments.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using queue connection configuration, driver names beyond shown examples, delayed dispatch, synchronous dispatch, dispatch after response, chains, batches, unique jobs, encrypted jobs, job `handle()` injection, job retries, job timeout properties, rate limiting middleware, exception throttling middleware, or job testing helpers.
