# Form Objects

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 `Livewire\Form` topic.

## Creation And Shape
- The documented command for generating a form object is `php artisan livewire:form PostForm`.
- A form object class extends `Livewire\Form`.
- Documented examples place form classes under the `App\Livewire\Forms` namespace.
- A form object can contain public properties and `#[Validate]` attributes.
- A component uses a form object as a typed public property, such as `public PostForm $form`.

## Blade Binding
- When using form objects, prepend the component form property name to model bindings and error directives.
- Documented examples use `wire:model="form.title"` and `wire:model="form.content"`.
- Matching error keys are `@error('form.title')` and `@error('form.content')`.

## Data Access
- The docs show `Post::create($this->form->all())` for creating from all form properties.
- The docs show `Post::create($this->form->only(['title', 'content']))` for selecting specific form properties.
- Inside a form object, documented examples use `$this->only(['title', 'content'])` before create or update.
- Inside a form object, documented examples use `$this->all()` before update in an editing flow.

## Moving Logic Into The Form
- The docs show moving methods such as `store()` and `update()` into the form object.
- A form method can call `$this->validate()` before persistence.
- A form method can create a record with selected form data.
- A form method can update a stored model with selected form data.

## Editing Existing Records
- Documented create/update reuse stores an optional model property such as `public ?Post $post`.
- The docs show a `setPost(Post $post)` method that assigns the model and fills form fields from the model.
- The docs show `Rule::unique('posts')->ignore($this->post)` inside `rules()` for update validation.

## Reset And Pull
- `$this->reset()` resets all form fields.
- `$this->reset('title')` resets one field.
- `$this->reset(['title', 'content'])` resets multiple fields.
- `$this->pull()` retrieves and resets all form fields.
- `$this->pull('title')` retrieves and resets one field.
- `$this->pull(['title', 'content'])` retrieves and resets selected fields as a key-value array.

## Form-Object Error Prefixing
- When `$this->addError()` is called inside a form object, the docs state that the error key is automatically prefixed with the form property name assigned in the parent component.
- The documented example says a form assigned to `$data` prefixes `key` as `data.key`.