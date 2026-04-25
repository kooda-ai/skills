# Custom Inputs Security And Testing

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 custom input, form security, or testing topic.

## Blade Custom Controls
- Repeated input markup can be extracted into Blade components.
- Attribute forwarding with `{{ $attributes }}` lets external attributes such as `wire:model` reach the rendered control.
- The docs show an Alpine counter Blade component with `x-modelable="count"` and `{{ $attributes }}` on the root element.
- `x-modelable` makes the named Alpine data value bindable from outside the component.
- The docs state that `x-modelable` works for both `wire:model` and `x-model`.

## Livewire Child Inputs
- `Livewire\Attributes\Modelable` marks a public property on a child component as bindable from a parent `wire:model`.
- The docs show `#[Modelable] public $value = ''` inside a child input component.
- The parent can then use the child like an input with `<livewire:todo-input wire:model="todo" />`.
- The docs also show richer custom input components, such as a rich text editor or date picker, using `#[Modelable]`.

## Form Security
- Public Livewire properties are exposed to the client and can be modified from the browser.
- The docs show a vulnerable edit form when a public record ID can be modified client-side and used for updates.
- `#[Locked]` prevents a public property from being modified on the client side.
- Public Eloquent model properties are automatically locked by Livewire in the documented secure edit pattern.
- Action parameters are arbitrary user input and should be authorized before sensitive updates or deletes.
- The docs show authorizing an action parameter with `$this->authorize('delete', $post)` before deleting a model.

## Validation Tests
- Test form validation with `Livewire::test(...)->set(...)->call(...)->assertHasErrors(...)`.
- `assertHasErrors('title')` asserts that a field has a validation error.
- `assertHasErrors(['title' => ['min:3']])` asserts a specific validation rule.
- `assertHasErrors(['title', 'content'])` asserts multiple fields.
- Use the component class or component name exactly as documented by the current lookup.

## Upload Tests
- The docs test uploads with Laravel fake storage and fake uploaded files.
- Use `Storage::fake('avatars')` for a fake disk in the documented example.
- Use `UploadedFile::fake()->image('avatar.png')` for a fake image.
- The docs show setting the upload property with `Livewire::test(...)->set('photo', $file)`.
- The docs show calling the upload action and asserting the stored file with `Storage::disk('avatars')->assertExists('uploaded-avatar.png')`.