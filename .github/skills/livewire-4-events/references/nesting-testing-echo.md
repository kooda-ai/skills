# Nesting, Testing, And Echo

## Parent-Child Event Communication
The Nesting docs show a parent listening for a child event with `#[On('remove-todo')]`:

```php
use Illuminate\Support\Facades\Auth;
use Livewire\Attributes\Computed;
use Livewire\Attributes\On;
use Livewire\Component;
use App\Models\Todo;

new class extends Component {
    #[On('remove-todo')]
    public function remove($todoId)
    {
        $todo = Todo::find($todoId);

        $this->authorize('delete', $todo);

        $todo->delete();
    }

    #[Computed]
    public function todos()
    {
        return Auth::user()->todos;
    }
};
```

The child dispatches the event from an action:

```php
public function remove()
{
    $this->dispatch('remove-todo', todoId: $this->todo->id);
}
```

The Nesting docs state this takes two network requests: one for the child action that dispatches the event, and one after the client-side event is intercepted by the parent.

## Client-Side Dispatch From Child Templates
The Nesting docs show avoiding the first request by dispatching directly on the client side:

```blade
<button wire:click="$dispatch('remove-todo', { todoId: {{ $todo->id }} })">Remove</button>
```

The docs state: as a rule of thumb, always prefer dispatching client-side when possible.

## Alternatives Mentioned In The Docs
If events are used only to call behavior on a parent from a child, the Events docs point to `$parent`:

```blade
<button wire:click="$parent.showCreatePostForm()">Create Post</button>
```

The Nesting docs also show direct parent access for removal:

```blade
<button wire:click="$parent.remove({{ $todo->id }})">Remove</button>
```

The Nesting docs state that if child components are created primarily to trigger parent updates through events, islands can eliminate event communication overhead because they share the same component context.

## Testing Dispatched Events
Assert an event was dispatched:

```php
Livewire::test(CreatePost::class)
    ->call('save')
    ->assertDispatched('post-created');
```

The Testing docs also show string component names:

```php
Livewire::test('post.create')
    ->set('title', 'New post')
    ->call('save')
    ->assertDispatched('post-created');
```

Assert event parameters with named arguments:

```php
Livewire::test('post.show')
    ->call('delete', postId: 3)
    ->assertDispatched('notify', message: 'Post deleted');
```

Use a closure for complex parameter assertions:

```php
Livewire::test('post.show')
    ->call('delete', postId: 3)
    ->assertDispatched('notify', function ($event, $params) {
        return ($params['message'] ?? '') === 'Post deleted';
    });
```

The testing method reference includes:

```php
->assertDispatched('post-created')
->assertNotDispatched('post-created')
```

## Testing Event Listeners
Dispatch events from the test environment and assert the listener response:

```php
Livewire::test(Dashboard::class)
    ->assertSee('Posts created: 0')
    ->dispatch('post-created')
    ->assertSee('Posts created: 1');
```

The testing method reference includes dispatching with parameters:

```php
->dispatch('post-created', postId: $post->id)
```

## Echo Prerequisites
The Events docs state that Laravel Echo must be installed and `window.Echo` must be globally available.

## Echo Listener Basics
Listen for a public Echo event with `#[On]`:

```php
use Livewire\Attributes\On;
use Livewire\Component;

new class extends Component {
    public $showNewOrderNotification = false;

    #[On('echo:orders,OrderShipped')]
    public function notifyNewOrder()
    {
        $this->showNewOrderNotification = true;
    }
};
```

## Dynamic Echo Channels
Use `getListeners()` for variables embedded in Echo channel names:

```php
public function getListeners()
{
    return [
        "echo:orders.{$this->order->id},OrderShipped" => 'notifyShipped',
    ];
}
```

Or use dynamic event name syntax:

```php
#[On('echo:orders.{order.id},OrderShipped')]
public function notifyNewOrder()
{
    $this->showNewOrderNotification = true;
}
```

Access the Echo payload through the passed `$event` parameter:

```php
#[On('echo:orders.{order.id},OrderShipped')]
public function notifyNewOrder($event)
{
    $order = Order::find($event['orderId']);
}
```

## Custom Broadcast Names
When Laravel `broadcastAs()` returns a custom name, listen with that custom name instead of the class name, prefixed with a dot:

```php
#[On('echo:scores,.score.submitted')]
public function handleScoreSubmitted($event)
{
    $this->scores[] = $event['score'];
}
```

The docs also show a dynamic channel with a custom broadcast name:

```php
#[On('echo:scores.{game.id},.score.submitted')]
public function handleScoreSubmitted($event)
{
    $this->scores[] = $event['score'];
}
```

## Private And Presence Channels
The Events docs say to define authentication callbacks before using private and presence channels.

The documented listener prefixes are:

```php
public function getListeners()
{
    return [
        "echo:orders,OrderShipped" => 'notifyNewOrder',
        "echo-private:orders,OrderShipped" => 'notifyNewOrder',
        "echo-presence:orders,OrderShipped" => 'notifyNewOrder',
        "echo-presence:orders,here" => 'notifyNewOrder',
        "echo-presence:orders,joining" => 'notifyNewOrder',
        "echo-presence:orders,leaving" => 'notifyNewOrder',
    ];
}
```