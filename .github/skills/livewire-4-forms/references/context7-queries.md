# Context7 Queries

Use this reference to refresh Livewire 4 Forms source context before applying the skill.

## Library
- Preferred Context7 library ID: `/websites/livewire_laravel_4_x`
- If the library ID is not already available in the conversation, resolve `Livewire` with Context7 before querying docs.

## Query Shapes
- Basic forms: `Livewire 4 forms documentation: form submission with wire:submit, wire:model binding, native input examples, validation before persistence, and error display.`
- Form objects: `Livewire 4 form objects: livewire:form command, Livewire\Form, public typed form property, form.title bindings, store/update methods, reset, pull, all, and only.`
- Validation: `Livewire 4 validation for forms: Validate attribute, onUpdate false, rules method, Rule objects, custom messages, validationAttributes, manual errors, withValidator, ValidationException, and JavaScript errors.`
- Real-time binding: `Livewire 4 wire:model modifiers for forms: .live, .blur, .change, .enter, .lazy, .debounce, .throttle, .number, .boolean, .fill, .deep, .preserve-scroll, and validation timing.`
- Uploads: `Livewire 4 file uploads in forms: WithFileUploads, temporary files, wire:model file input, validation, multiple uploads, temporaryUrl, storing files, temporary_file_upload config, and upload tests.`
- Loading and dirty states: `Livewire 4 forms loading and dirty states: wire:loading, data-loading, wire:target, automatic form disabling, wire:dirty, wire:dirty.class, and property targets.`
- Custom inputs: `Livewire 4 custom form controls: Blade components forwarding wire:model attributes, Alpine x-modelable controls, and child components with #[Modelable].`
- Security: `Livewire 4 form security: public properties, client-side tampering, Locked attribute, Eloquent model property locking, action parameter authorization, and safe persistence.`
- Testing: `Livewire 4 testing forms and validation: Livewire::test set call assertHasErrors, validation rule assertions, uploaded file fakes, fake storage, and storage assertions.`

## Use Rules
- Prefer narrow queries over broad summaries when a task names a specific method, modifier, attribute, or testing helper.
- If Context7 does not return a requested API, do not include it; query again with the exact term once before leaving it out.
- Preserve the exact names and signatures returned by Context7.