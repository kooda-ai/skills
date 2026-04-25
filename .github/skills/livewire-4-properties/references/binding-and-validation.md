# Binding And Validation

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 `wire:model`, form object property, or validation topic.

## Basic Binding
- `wire:model="propertyName"` binds an HTML input element to a Livewire component property.
- `wire:model` creates two-way data binding: input changes update the component property, and component property changes update the input.
- The docs show `wire:model` on text inputs and textareas.
- For a textarea bound to a string property, Livewire populates the textarea from the property without explicit `{{ }}` interpolation.

## Update Timing
- By default, Livewire sends network requests when an action is performed, such as `wire:click` or `wire:submit`.
- By default, `wire:model` property changes do not trigger network requests by themselves.
- `wire:model.live="title"` sends property updates to the server as a user types.
- `wire:model.blur="title"` syncs when the input loses focus.
- `wire:model.change="state"` syncs when the element fires a `change` event.
- `wire:model.enter="search"` syncs when the user presses Enter.
- When using `.live`, `.debounce.Xms` customizes debounce behavior and `.throttle.Xms` customizes throttle behavior.

## Documented Modifiers
- `.live` sends updates to the server.
- `.blur` updates on blur.
- `.change` updates on change.
- `.enter` updates on Enter.
- `.lazy` updates on change and sends a network request.
- `.debounce.Xms` debounces updates when used with `.live`.
- `.throttle.Xms` throttles updates when used with `.live`.
- `.number` casts the value to an integer on the server.
- `.boolean` casts the value to a boolean on the server.
- `.fill` uses the initial value from the HTML `value` attribute.
- `.deep` also listens to events from child elements when the binding is placed on a wrapping element.
- `.preserve-scroll` maintains scroll position during updates.

## Form Object Properties
- A form object class extends `Livewire\Form` and can contain public properties.
- A component can declare a public typed form property, such as `public PostForm $form`.
- Templates bind form object properties with paths such as `wire:model="form.title"`.
- Validation errors for form object properties use keys such as `form.title`.
- Form object examples document `validate()`, `reset()`, `pull()`, and selected persistence with `only(['title', 'content'])`.

## Property Validation
- `#[Validate('required')]` from `Livewire\Attributes\Validate` attaches validation rules to a property.
- The docs state that `#[Validate]` rules run before each server-side property update.
- The docs still call `$this->validate()` before persisting data so properties that have not been updated are validated too.
- `$this->validate()` returns validated data.
- `#[Validate('required|min:3', onUpdate: false)]` disables automatic validation and leaves validation to `$this->validate()`.
- `#[Validate('required', as: 'date of birth')]` customizes the attribute name.
- `#[Validate('required', message: 'Please provide a post title')]` customizes the validation message.
- Multiple `#[Validate]` attributes can provide different messages for different rules.
- Use `rules()` for runtime rule syntax such as Laravel `Rule` objects.
- Add an empty `#[Validate]` attribute when using `rules()` but wanting real-time validation behavior confirmed by the docs.