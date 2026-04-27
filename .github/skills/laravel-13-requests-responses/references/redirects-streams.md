# Redirects And Streams

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x redirects with flashed data/input, URI redirects, and frontend stream consumption packages.

## Redirect With Flashed Session Data
The docs show flashing data to the session and redirecting in one fluent chain:

```php
Route::post('/user/profile', function () {
    // ...

    return redirect('/dashboard')->with('status', 'Profile updated!');
});
```

The docs show retrieving the flashed session value in Blade:

```blade
@if (session('status'))
    <div class="alert alert-success">
        {{ session('status') }}
    </div>
@endif
```

Confirmed helpers and methods: `redirect(...)`, `with(...)`, and `session(...)`.

## Redirect With Input
The docs show using `withInput()` to flash the current request's input data to the session before redirecting:

```php
return back()->withInput();
```

The docs describe this as useful for repopulating form fields after a validation error.

## URI Redirects
The docs show creating a `RedirectResponse` from a `Uri` object:

```php
$uri = Uri::of('https://example.com');

return $uri->redirect();
```

The docs show returning a `Uri` instance directly from a route or controller action:

```php
use Illuminate\Support\Facades\Route;
use Illuminate\Support\Uri;

Route::get('/redirect', function () {
    return Uri::to('/index')
        ->withQuery(['sort' => 'name']);
});
```

Confirmed classes and methods: `Illuminate\Support\Uri`, `Uri::of(...)`, `Uri::to(...)`, `withQuery(...)`, and `redirect()`.

## Event Stream Frontend Packages
The docs say event streams can be consumed using Laravel stream npm packages:

```shell
npm install @laravel/stream-react
npm install @laravel/stream-vue
npm install @laravel/stream-svelte
```

The docs show `useEventStream(...)` in React:

```jsx
import { useEventStream } from "@laravel/stream-react";

function App() {
  const { message } = useEventStream("/chat");

  return <div>{message}</div>;
}
```

The docs show `useEventStream(...)` in Vue:

```vue
<script setup lang="ts">
import { useEventStream } from "@laravel/stream-vue";

const { message } = useEventStream("/chat");
</script>

<template>
  <div>{{ message }}</div>
</template>
```

The docs show `useEventStream(...)` in Svelte:

```svelte
<script>
import { useEventStream } from "@laravel/stream-svelte";

const eventStream = useEventStream("/chat");
</script>

<div>{$eventStream.message}</div>
```

The docs list advanced `useEventStream` options: `eventName`, `onMessage`, `onError`, `onComplete`, `endSignal`, `glue`, and `replace`. The docs state defaults for `eventName` as `'message'`, `endSignal` as `'</stream>'`, `glue` as `' '`, and `replace` as `true`.

## JSON Stream Frontend Packages
The docs show `useJsonStream(...)` in React:

```tsx
import { useJsonStream } from "@laravel/stream-react";

type User = {
    id: number;
    name: string;
    email: string;
};

function App() {
    const { data, send } = useJsonStream<{ users: User[] }>("users");

    const loadUsers = () => {
        send({
            query: "taylor",
        });
    };
}
```

The docs show `useJsonStream(...)` in Vue and Svelte as well. Confirm exact Vue/Svelte snippets with a fresh lookup before using them in final code.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using route redirects, action redirects, external redirects, intended redirects, redirect status codes, server-side `stream`, `streamJson`, `eventStream`, `streamDownload`, frontend stream package advanced examples, stream authentication, stream error handling beyond listed option names, or server routes that produce stream responses.
