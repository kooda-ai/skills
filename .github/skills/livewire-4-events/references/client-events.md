# Client-Side Events

## Component Scripts
Inside a component template script, listen with `this.$on`:

```html
<script>
    this.$on('post-created', () => {
        //
    });
</script>
```

The docs state that this listens from the component it is registered within, and that if the component is no longer on the page, the listener will no longer be triggered.

Dispatch from a component script with `this.$dispatch`:

```html
<script>
    this.$dispatch('post-created');
</script>
```

Dispatch only to the component where the script resides with `this.$dispatchSelf`:

```js
this.$dispatchSelf('post-created');
```

Pass parameters as an object:

```html
<script>
    this.$dispatch('post-created', { refreshPosts: true });
</script>
```

Access those parameters in a Livewire class listener:

```php
use Livewire\Attributes\On;

#[On('post-created')]
public function handleNewPost($refreshPosts = false)
{
    //
}
```

Access those parameters in JavaScript through `event.detail`:

```html
<script>
    this.$on('post-created', (event) => {
        let refreshPosts = event.detail.refreshPosts

        // ...
    })
</script>
```

## Global JavaScript
Register global event listeners inside `livewire:init`:

```html
<script>
    document.addEventListener('livewire:init', () => {
       Livewire.on('post-created', (event) => {
           //
       });
    });
</script>
```

Use the returned cleanup function to unregister the listener:

```html
<script>
    document.addEventListener('livewire:init', () => {
        let cleanup = Livewire.on('post-created', (event) => {
            //
        });

        cleanup();
    });
</script>
```

The JavaScript docs also show the global event APIs:

```js
Livewire.dispatch('post-created', { postId: 2 })

Livewire.dispatchTo('dashboard', 'post-created', { postId: 2 })

Livewire.on('post-created', ({ postId }) => {
    // ...
})
```

For Alpine components used with `wire:navigate`, the JavaScript docs show collecting `Livewire.on(...)` cleanup callbacks and calling them from Alpine `destroy()`.

## `$wire` Event Methods
The JavaScript `$wire` reference documents these event methods:

```js
$wire.$on('post-created', () => { ... })

$wire.$dispatch('post-created', { postId: 2 })

$wire.$dispatchTo('dashboard', 'post-created', { postId: 2 })

$wire.$dispatchSelf('post-created')
```

The `$wire.$on` reference says it listens for an event dispatched from this component or its children.

## Alpine Listening
Livewire events are plain browser events under the hood, so Alpine can listen for them:

```html
<div x-on:post-created="..."></div>
```

The docs state that this listens for `post-created` from Livewire components that are children of the HTML element with the `x-on` directive.

Listen from any Livewire component on the page with `.window`:

```html
<div x-on:post-created.window="..."></div>
```

Access payload data through `$event.detail`:

```html
<div x-on:post-created="notify('New post: ' + $event.detail.title)"></div>
```

## Alpine Dispatching
Any event dispatched from Alpine can be intercepted by a Livewire component:

```html
<button x-on:click="$dispatch('post-created')">...</button>
```

Pass data as the second parameter:

```html
<button x-on:click="$dispatch('post-created', { title: 'Post Title' })">...</button>
```