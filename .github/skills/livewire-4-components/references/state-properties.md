# State And Properties

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 properties, state, or `wire:model` topic.

## Public Property State
- Livewire properties store and manage state inside components.
- Public properties are accessible and modifiable on both the server and client side.
- Initialize property values in `mount()` when the component first renders.
- `fill(array $values)` bulk assigns multiple public properties from an associative array.
- `reset()` resets one or more properties back to their initial state before `mount()` ran; the docs warn it will not reset to values assigned in `mount()`.
- `pull()` retrieves a property value and resets it in one operation; calling `pull()` with no arguments is documented as the same as `all()` plus `reset()`, and `pull([...])` is documented as the same as `only(...)` plus `reset(...)`.

## Data Binding
- `wire:model="propertyName"` binds an input to a component property.
- By default, a property bound with `wire:model` is synchronized with the server when an action such as `wire:click` or `wire:submit` runs.
- The docs describe these `wire:model` modifiers: `.live`, `.blur`, `.change`, `.enter`, `.lazy`, `.debounce.Xms`, `.throttle.Xms`, `.number`, `.boolean`, `.fill`, `.deep`, and `.preserve-scroll`.
- `.deep` listens to events from child elements when binding on a wrapping element.
- `.number` casts a value to an integer on the server, and `.boolean` casts a value to a boolean on the server.

## Supported Property Types
- Primitive property types documented by Livewire are `Array`, `String`, `Integer`, `Float`, `Boolean`, and `Null`.
- Common PHP or Laravel types documented by Livewire are `BackedEnum`, `Illuminate\Support\Collection`, `Illuminate\Database\Eloquent\Collection`, `Illuminate\Database\Eloquent\Model`, `DateTime`, `Carbon\Carbon`, and `Illuminate\Support\Stringable`.
- Livewire serializes and dehydrates properties to JSON between requests and hydrates them back into PHP on the next request.
- The docs warn that dehydrated values can expose system information to JavaScript, including property names, model class names, model IDs, and eager-loaded relationships.
- For Eloquent collections and models, the docs warn that query constraints such as `select(...)` are not preserved between requests and that large Eloquent collections can have performance impact.
- The docs recommend computed properties when expensive Eloquent queries should not be stored as public property state.

## Custom Property Types
- A custom type can implement `Livewire\Wireable`.
- A Wireable class implements `toLivewire()` and static `fromLivewire($value)` so Livewire can convert it to JSON and back into PHP.
- The docs mention Synthesizers as the advanced mechanism for supporting different property types.

## JavaScript Property Access
- Livewire exposes a `$wire` object inside Alpine expressions within a Livewire component.
- `$wire.property` can read a property client-side without a server roundtrip.
- Assigning `$wire.property = ''` changes the property client-side without an immediate request; the server-side value is synchronized on a subsequent request.
- `$wire.set('todo', '')` sets a property and by default triggers a network request.
- `$wire.set('todo', '', false)` defers the network request and synchronizes on a subsequent request.

## URL Properties
- The documented `#[Url]` attribute accepts these parameters:

```php
#[Url(
    ?string $as = null,
    bool $history = false,
    bool $keep = false,
    mixed $except = null,
    mixed $nullable = null,
)]
```

- The docs show `#[Url(as: 'q')]` to map a property to a custom query-string name.

## Locked Properties And Security
- Treat public properties as user input, as if they were request input from a traditional endpoint.
- Validate and authorize public property values before persisting them.
- Use `#[Locked]` from `Livewire\Attributes\Locked` to prevent a public property from being modified on the client side.
- When an Eloquent model is assigned to a public Livewire property, Livewire automatically locks the property and ensures the ID is not changed.
- The docs show Laravel `Relation::morphMap()` as a way to avoid exposing full model class names during dehydration.