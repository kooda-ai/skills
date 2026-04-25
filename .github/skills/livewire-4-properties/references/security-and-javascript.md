# Security And JavaScript

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 property security, dehydration, Eloquent property, or JavaScript access topic.

## Public Property Security
- Public properties are accessible and modifiable on both the server and the client side.
- Treat public property values like request input from a traditional endpoint.
- Validate and authorize public property values before persisting them or using them for sensitive operations.
- Use `#[Locked]` when a public property must not be modified from the client side.

## Eloquent Properties
- The security docs show using an Eloquent model public property instead of a raw ID when deleting a model.
- When an Eloquent model is assigned to a public Livewire property, Livewire automatically locks the property and ensures the ID is not changed.
- The Properties docs warn that dehydrated values can expose system information to JavaScript, including property names, model class names, model IDs, and eager-loaded relationships.
- The docs show Laravel `Relation::morphMap()` as a way to avoid exposing full model class names during dehydration.
- The docs warn that query constraints such as `select(...)` are not preserved between requests for Eloquent model and collection properties.
- The docs warn that large Eloquent collections can have performance impact.
- The docs recommend computed properties when expensive Eloquent queries should not be stored as public property state.

## JavaScript `$wire` Access
- Livewire exposes a `$wire` object inside Alpine expressions within a Livewire component.
- `$wire.property` reads a property client side without a server roundtrip.
- Assigning `$wire.property = ''` changes the property client side without an immediate request; the server-side value is synchronized on a subsequent request.
- `$wire.set('todo', '')` sets a property and by default triggers a network request.
- `$wire.set('todo', '', false)` defers the network request and synchronizes on a subsequent request.