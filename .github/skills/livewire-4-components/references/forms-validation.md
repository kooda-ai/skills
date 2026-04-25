# Forms And Validation

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 form, validation, or form object topic.

## Basic Forms
- A Livewire form binds component properties with `wire:model`.
- A form submits to a component action with `wire:submit="save"`.
- The docs show persistence with `Post::create($this->only(['title', 'content']))`, `session()->flash(...)`, and `$this->redirect('/posts')`.
- Validation errors can be displayed with Blade's `@error('title') {{ $message }} @enderror` pattern.

## Validation Attributes
- Add `#[Validate('required')]` from `Livewire\Attributes\Validate` above a property to attach validation rules.
- The docs state that `#[Validate]` rules run before each server-side property update.
- The docs also say to still call `$this->validate()` before persisting data so properties that have not been updated are validated too.
- `$this->validate()` returns validated data.
- `#[Validate('required|min:3', onUpdate: false)]` disables automatic validation and leaves validation to `$this->validate()`.
- `#[Validate('required', as: 'date of birth')]` customizes the attribute name.
- `#[Validate('required', message: 'Please provide a post title')]` customizes the validation message.
- Multiple `#[Validate]` attributes can provide different messages for different rules.
- `#[Validate('required', message: '...', translate: false)]` opts out of localization.
- Array syntax can customize keys, such as rules for `todos` and `todos.*`.
- The docs warn that PHP attributes do not support runtime syntaxes such as Laravel `Rule` objects; use `rules()` for those.

## Rules Method
- Define a protected `rules()` method to return validation rules when `#[Validate]` is not suitable.
- `rules()` is documented for runtime syntax such as `Illuminate\Validation\Rule` objects.
- Rules from `rules()` are applied when `$this->validate()` runs.
- The docs state that `rules()` does not validate on data updates by itself.
- Add an empty `#[Validate]` attribute to a property when using `rules()` but wanting real-time validation behavior.
- The docs also document `messages()` and `validationAttributes()` methods.
- The docs warn not to define properties or methods named `rules`, `messages`, `validationAttributes`, or `validationCustomValues` unless customizing validation, because those names conflict with Livewire mechanisms.

## Form Objects
- Create a form object with `php artisan livewire:form PostForm`.
- The command creates `app/Livewire/Forms/PostForm.php`.
- A form class extends `Livewire\Form` and can contain properties and `#[Validate]` attributes.
- A component can type a public form property, such as `public PostForm $form`.
- Templates bind form object properties with names like `wire:model="form.title"` and display errors with keys like `form.title`.
- The docs show `Post::create($this->form->only(['title', 'content']))`, `$this->form->all()`, `$this->form->validate()`, `$this->form->store()`, and `$this->form->update()` patterns.
- Form object create/update reuse is documented with a `setPost(Post $post)` method that stores the model and fills properties.
- Form objects can call `reset()` for all fields, `reset('title')` for one field, or `reset(['title', 'content'])` for multiple fields.
- Form objects can call `pull()` to retrieve and reset all properties, `pull('title')` for one property, or `pull(['title', 'content'])` for selected properties.

## Real-Time Fields
- By default, Livewire sends a network request when a form is submitted or another action is called, not while the form is being filled out.
- `wire:model.live="title"` sends requests as the user types.
- `wire:model.live.blur="title"` sends a request when the user tabs or clicks away from the input.
- Real-time validation requires a request-triggering model binding such as `.live` or `.blur`; `#[Validate]` rules then run before the property is updated.
- The docs show real-time saving with `updated($name, $value)` and `wire:model.live.blur`.
- With `.live`, the docs state that a default debounce of 250ms is applied to text input updates.
- Customize debounce with `.debounce.150ms` and throttle with `.throttle.150ms`.

## Loading And Dirty States
- Livewire automatically disables submit buttons and marks inputs as `readonly` while a form is being submitted.
- `wire:loading` can show loading UI during a request.
- The docs show using Tailwind with Livewire's automatic `data-loading` attribute, including `in-data-loading:hidden` and `not-in-data-loading:hidden` examples.
- `wire:dirty.class="border-yellow"` toggles a class when an input value diverges from the server-side component value.
- `wire:dirty` with `wire:target="title"` toggles an entire element for a specific property.

## Extracting Inputs
- Repeated input markup can be extracted to Blade components.
- Forward attributes with `{{ $attributes }}` so `wire:model`, `disabled`, `class`, and `required` reach the real input.
- Custom Alpine-powered controls can use `x-modelable="count"` and `{{ $attributes }}` so `wire:model="quantity"` binds to the custom control value.
- The docs state that `x-modelable` works for both `wire:model` and `x-model`.

## Manual Validation Control
- `$this->addError([key], [message])` manually adds a validation message to the error bag.
- `$this->resetValidation([?key])` resets validation errors for a key or all errors if no key is supplied.
- `$this->getErrorBag()` retrieves the underlying Laravel error bag.
- Inside a form object, errors added with `$this->addError()` are automatically prefixed with the form property name assigned in the parent component.
- `withValidator()` gives access to the Validator instance before rules are evaluated; the docs show registering it in `boot()`.
- Livewire catches `ValidationException` exceptions thrown inside components and provides the errors to the view.

## Testing And JavaScript Errors
- Test validation with `Livewire::test(...)->set(...)->call(...)->assertHasErrors(...)`.
- `assertHasErrors()` can assert a property, multiple properties, or a property with specific rules such as `['title' => ['min:3']]`.
- The `$errors` magic property is available client-side.
- The docs list `$errors.has('field')`, `$errors.first('field')`, `$errors.get('field')`, `$errors.all()`, `$errors.clear()`, and `$errors.clear('field')`.
- In Alpine, access errors through `$wire.$errors`.

## Deprecated Attribute Note
- The validation docs mention the old `#[Rule]` attribute in Livewire v3 and recommend changing occurrences to `#[Validate]` to stay current.
- Do not introduce `#[Rule]` in new Livewire 4 guidance unless the current Context7 lookup confirms the user is asking about legacy migration.