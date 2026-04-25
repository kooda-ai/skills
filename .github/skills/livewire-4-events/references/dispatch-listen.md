# Dispatching And Listening

## Component Dispatch
The Events docs dispatch from a Livewire component with:

```php
$this->dispatch('post-created');
```

Additional event data is passed as named data:

```php
$this->dispatch('post-created', title: $post->title);
```

The docs state that every other component on the page listening for the event is notified.

## Component Listener
Listen by importing `Livewire\Attributes\On` and placing `#[On(...)]` above the listener method:

```php
use Livewire\Attributes\On;
use Livewire\Component;

new class extends Component {
    #[On('post-created')]
    public function updatePostList($title)
    {
        // ...
    }
};
```

The docs state that additional data sent with the event is provided to the action as its first argument.

## Dynamic Event Names
Dispatch a scoped event name:

```php
$this->dispatch("post-updated.{$post->id}");
```

Listen with a component-data placeholder:

```php
use App\Models\Post;
use Livewire\Attributes\On;
use Livewire\Component;

new class extends Component {
    public Post $post;

    #[On('post-updated.{post.id}')]
    public function refreshPost()
    {
        // ...
    }
};
```

The documented example says a post with ID `3` triggers only on `post-updated.3`.

## Specific Child Component Listeners
Listen for a child event directly on the child component tag:

```blade
<livewire:edit-post @saved="$refresh">
```

Call a parent method instead of `$refresh`:

```blade
<livewire:edit-post @saved="close">
```

Forward a dispatched payload value to the parent method:

```blade
<livewire:edit-post @saved="close($event.detail.postId)">
```

## Targeted PHP Dispatch
Dispatch directly to another component:

```php
$this->dispatch('post-created')->to(component: Dashboard::class);
```

The Events docs describe this as skipping other components listening for that event.

## Self PHP Dispatch
The Events docs describe restricting an event to only the component it was triggered from with `dispatch()->self()` and show this snippet:

```php
$this->dispatch('post-created')->to(self: true);
```

## Blade Dispatch Helpers
Dispatch from a Blade template with `$dispatch`:

```blade
<button wire:click="$dispatch('show-post-modal', { id: {{ $post->id }} })">
    EditPost
</button>
```

Dispatch directly to another component from Blade with `$dispatchTo()`:

```blade
<button wire:click="$dispatchTo('posts', 'show-post-modal', { id: {{ $post->id }} })">
    EditPost
</button>
```