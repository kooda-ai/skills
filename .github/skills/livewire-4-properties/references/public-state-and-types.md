# Public State And Types

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 public property, helper, supported type, or custom type topic.

## Public Property State
- Livewire properties are the primary mechanism for storing and managing component state.
- Public properties are accessible and modifiable on both the server and the client side.
- Public property values can be declared directly on the component class.
- `mount()` is called when the component is initialized and is documented for setting initial property values.
- Data passed into a component can be received through `mount()` or assigned to public properties when names match the passed values.

## Property Helpers
- `fill(array $values)` bulk assigns multiple properties from an associative array.
- `reset(...)` resets specified properties to the default state defined in the class property declaration.
- Form object examples document `reset()` for all fields, `reset('title')` for one field, and `reset(['title', 'content'])` for multiple fields.
- `pull()` retrieves and resets all properties in the documented form object example.
- `pull('title')` returns a single value before resetting it.
- `pull(['title', 'content'])` returns a key-value array before resetting the selected properties.
- The docs show persistence examples with `only(['title', 'content'])` when creating a model from selected component or form properties.

## Primitive Property Types
- Livewire documents these primitive public property types: `array`, `string`, `int`, `float`, `bool`, and `null`.
- Primitive property values are serialized to JSON between requests.

## Common PHP And Laravel Types
- Livewire documents common PHP or Laravel property types in the Properties docs; confirm the exact current list before using it in final guidance.
- Previously documented examples include `BackedEnum`, `Illuminate\Support\Collection`, `Illuminate\Database\Eloquent\Collection`, `Illuminate\Database\Eloquent\Model`, `DateTime`, `Carbon\Carbon`, and `Illuminate\Support\Stringable`.
- Use the current Context7 result as the source of truth if the supported type list changes.

## Custom Property Types
- A custom type can implement `Livewire\Wireable`.
- A Wireable class implements `toLivewire()` and static `fromLivewire($value)` so Livewire can convert the value to JSON and back into PHP.
- The docs mention Synthesizers as the advanced mechanism for supporting different property types.