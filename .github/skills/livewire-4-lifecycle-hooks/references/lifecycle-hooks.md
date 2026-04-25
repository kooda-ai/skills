# Lifecycle Hooks Reference

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 lifecycle hook topic.

## Component Hook Table
The Livewire 4.x lifecycle hooks page lists these component lifecycle hooks:

- `mount()`: called when a component is created.
- `hydrate()`: called when a component is re-hydrated at the beginning of a subsequent request.
- `boot()`: called at the beginning of every request, both initial and subsequent.
- `updating()`: called before updating a component property.
- `updated()`: called after updating a property.
- `rendering()`: called before the component's view is rendered.
- `rendered()`: called after the component's view is rendered.
- `dehydrate()`: called at the end of every component request.
- `exception($e, $stopPropagation)`: called when an exception is thrown.

## Mount
- Livewire uses `mount()` for accepting parameters and initializing component state.
- Livewire components do not use `__construct()` for this work because components are re-constructed on subsequent network requests, while initialization should happen once when the component is first created.
- The docs show `mount()` receiving data passed into the component as method parameters, including Eloquent model parameters.
- Lifecycle hook methods can use Laravel dependency injection by type-hinting method parameters.
- The lifecycle page points to properties, nesting, and pages docs for initializing properties, receiving data from parent components, and accessing route parameters with `mount()`.

## Boot
- `boot()` runs at the beginning of every server request for a component, both initialization and subsequent requests.
- Use `boot()` for setup code that should run every time the component class is booted.
- The docs show `boot()` initializing a protected Eloquent model property because protected properties are not persisted between requests.
- The docs note that a computed property is often better for the demonstrated protected-property use case.
- For sensitive public properties such as IDs, the docs say to authorize the property's value before using it or add `#[Locked]` so it is not changed client-side.

## Update Hooks
- Client-side users can update public properties in many ways, most commonly by modifying an input with `wire:model`.
- Update hooks intercept public-property updates so code can validate or authorize a value before it is set, or ensure a property is set in a given format.
- The docs show `updating($property, $value)` running before a property is updated.
- The docs show `updated($property)` running after a property is updated.
- The forms documentation also shows `updated($name, $value)` for automatically saving a field after it updates.
- Property-specific hook names can target a property directly, such as `updatedUsername()`; the docs say the same technique can be applied to the `updating` hook.
- Array properties have an additional `$key` argument passed to update hooks to specify the changing element.
- When the array itself is updated instead of a specific key, the `$key` argument is null.
- The docs show `updatedPreferences($value, $key)` for an array property.

## Hydrate And Dehydrate
- Hydrate and dehydrate refer to Livewire serializing a component to JSON for the client side and unserializing that JSON back into a PHP object on the subsequent request.
- `hydrate()` runs at the beginning of every subsequent request and does not run on the initial request, where `mount()` runs.
- `dehydrate()` runs at the end of every single request.
- The docs demonstrate `mount()`, `hydrate()`, and `dehydrate()` together to support using a custom DTO in component state.
- The docs say the DTO example demonstrates the abilities and nature of `hydrate()` and `dehydrate()`, but recommend Wireables or Synthesizers for custom types instead.

## Render Hooks
- Use `rendering()` and `rendered()` to hook into the process of rendering a component's Blade view.
- `rendering($view, $data)` runs before the provided view is rendered.
- In `rendering($view, $data)`, `$view` is the view about to be rendered and `$data` is the data provided to the view.
- `rendered($view, $html)` runs after the provided view is rendered.
- In `rendered($view, $html)`, `$view` is the rendered view and `$html` is the final rendered HTML.

## Exception Hook
- `exception($e, $stopPropagation)` can intercept and catch errors, such as to customize an error message or ignore a specific type of exception.
- The docs describe checking the exception value and using the `$stopPropagation` parameter to catch the issue.
- Calling `$stopPropagation()` can stop further execution, and the docs mention this as the pattern used by internal methods like `validate()`.

## Trait Hooks
- Traits can define lifecycle hook methods for reuse across components or for extracting component code into a dedicated file.
- To avoid conflicts when multiple traits declare lifecycle hooks, Livewire supports prefixing hook methods with the camelCased name of the trait declaring them.
- For a `HasPostForm` trait, the docs show `mountHasPostForm()`, `hydrateHasPostForm()`, `bootHasPostForm()`, `updatingHasPostForm()`, `updatedHasPostForm()`, `renderingHasPostForm()`, `renderedHasPostForm()`, and `dehydrateHasPostForm()`.

## Form Object Hooks
- Form objects in Livewire support property update hooks.
- These hooks work similarly to component update hooks and let code perform actions when properties in the form object change.
- The docs show a `PostForm` class extending `Livewire\Form` with `public $title = ''` and `public $tags = []`.
- The documented form-object hooks are `updating($property, $value)`, `updated($property, $value)`, `updatingTitle($value)`, `updatedTitle($value)`, `updatingTags($value, $key)`, and `updatedTags($value, $key)`.