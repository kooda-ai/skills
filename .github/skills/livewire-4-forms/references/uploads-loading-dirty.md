# Uploads Loading And Dirty States

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 upload, loading, or dirty-state topic.

## File Uploads
- File-upload forms use the `Livewire\WithFileUploads` trait.
- With the trait in place, a file input can use `wire:model` like other inputs.
- The docs show validating a single upload with `#[Validate('image|max:1024')]`.
- The docs show storing an uploaded file with `$this->photo->store(path: 'photos')`.
- Multiple uploads use a property initialized as an array and a file input with the `multiple` attribute.
- The docs show validating multiple uploads with rules for `photos.*`.
- Multiple uploaded files can be looped over and stored one by one.

## Temporary Previews
- Image uploads can be previewed before submission with `$photo->temporaryUrl()` in the template.
- The docs state that temporary URLs are only supported for image MIME types for security reasons.

## Temporary Upload Configuration
- The docs show a `temporary_file_upload` configuration array.
- Documented keys include `rules`, `middleware`, and `directory`.
- The documented example uses validation rules, throttling middleware, and a temporary directory name.

## Form Submission State
- During form submission, Livewire automatically disables submit buttons and marks form inputs as `readonly` in the documented actions guidance.
- `wire:loading` displays an element during a Livewire request.
- `wire:loading.remove` hides an element during a Livewire request.
- `wire:loading.class="opacity-50"` adds a class during loading.
- `wire:loading.class.remove="..."` removes a class during loading.
- `wire:loading.attr="disabled"` toggles an attribute during loading.
- Documented display modifiers include `.inline-flex`, `.inline`, `.block`, `.table`, `.flex`, and `.grid`.
- Documented delay modifiers include `.delay`, `.delay.shortest`, `.delay.shorter`, `.delay.short`, `.delay.long`, `.delay.longer`, and `.delay.longest`.

## Loading Targets
- By default, `wire:loading` is triggered when the component makes a server request.
- `wire:target="save"` scopes a loading indicator to one action or property.
- The docs show targeting multiple actions, a specific action with parameters, a property update, and all requests except a named target with `wire:target.except`.

## Data Loading
- Livewire automatically adds a `data-loading` attribute to elements that trigger network requests.
- The docs describe `data-loading` selectors as a Livewire 4 loading-state approach that can be simpler and more flexible than `wire:loading` for styling.
- Tailwind examples include `data-loading:opacity-50`, `data-loading:pointer-events-none`, `has-data-loading:opacity-50`, `in-data-loading:hidden`, and `not-in-data-loading:hidden`.
- Standard CSS can target `[data-loading]` and element-specific selectors such as `button[data-loading]`.

## Dirty State
- `wire:dirty` displays an element when local input state differs from the server-side component state.
- `wire:dirty.class="border-yellow"` applies a class while the target is dirty.
- `wire:dirty` can be combined with `wire:target="title"` to target a specific property.