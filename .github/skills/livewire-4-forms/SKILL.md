---
name: livewire-4-forms
description: 'Use when: working with Livewire 4 Forms, wire:submit, wire:model, form objects, Livewire\Form, livewire:form, form.title bindings, #[Validate], rules(), validation messages, @error, $errors, real-time validation, WithFileUploads, temporaryUrl(), loading states, wire:dirty, custom inputs, x-modelable, #[Modelable], validation tests, and upload tests. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 form submission, form object, validation, upload, binding, dirty/loading state, custom input, or form test concern'
---

# Livewire 4 Forms

## Purpose
Use this skill to create, review, or explain Livewire 4 forms using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Livewire 4 Forms topic.
2. Do not add form APIs, directives, modifiers, validation helpers, upload behavior, testing helpers, security advice, or examples unless they appear in the retrieved documentation.
3. If a requested Forms detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep examples close to documented snippets and preserve documented namespaces, attributes, directive names, modifier names, method names, parameter names, and value strings.
5. Do not infer behavior from Livewire 3, Laravel request/controller habits, Alpine patterns, package source code, or memory.

## Reference Map
- Context7 query shapes for refreshing source context: [context7-queries.md](./references/context7-queries.md)
- Basic submission, native inputs, `wire:model`, and modifiers: [submission-binding.md](./references/submission-binding.md)
- `Livewire\Form` objects, form-object properties, create/update flows, `reset()`, and `pull()`: [form-objects.md](./references/form-objects.md)
- Validation attributes, `rules()`, messages, manual errors, JavaScript errors, and custom validators: [validation.md](./references/validation.md)
- File uploads, temporary previews, loading indicators, `data-loading`, and dirty states: [uploads-loading-dirty.md](./references/uploads-loading-dirty.md)
- Custom form controls, `x-modelable`, `#[Modelable]`, form security, and tests: [custom-inputs-security-testing.md](./references/custom-inputs-security-testing.md)

## Workflow
1. Identify the form concern: basic submission, native input binding, update timing, form object extraction, create/update reuse, validation, upload, loading state, dirty state, custom input, security, or testing.
2. Run a narrow Context7 query for the exact Livewire 4 Forms topic before producing code or review findings.
3. Load the relevant reference file from the map above.
4. For simple forms, use the documented `wire:submit` pattern, bind public properties with `wire:model`, and validate before persistence.
5. For reusable or larger forms, choose a documented `Livewire\Form` object, a public typed form property, and Blade paths such as `form.title` only when the lookup confirms form-object binding.
6. For validation, choose `#[Validate]` for documented attribute rules, `rules()` for runtime rule objects, and `messages()` or `validationAttributes()` only when the current docs confirm them.
7. For real-time behavior, confirm the exact `wire:model` modifier set, such as `.live`, `.blur`, `.change`, `.enter`, `.lazy`, `.debounce.Xms`, or `.throttle.Xms`, and do not assume a request is sent without the documented modifier.
8. For uploads, confirm `WithFileUploads`, the property shape, validation rules, `temporaryUrl()`, storage call, multiple-upload array behavior, and any temporary upload configuration before using them.
9. For feedback states, choose documented `wire:loading`, automatic `data-loading`, `wire:target`, or `wire:dirty` patterns according to the triggering action or property.
10. For extracted controls, distinguish between Blade components that forward attributes with `{{ $attributes }}`, Alpine controls using `x-modelable`, and Livewire child components using `#[Modelable]`.
11. For security, treat public form properties and action parameters as client-controlled data, confirm locking or Eloquent model locking from the docs, and authorize before sensitive persistence when documented.
12. For tests, use only documented `Livewire::test(...)->set(...)->call(...)->assertHasErrors(...)`, Laravel upload fakes, and storage assertions returned by the lookup.
13. Finish by checking that every class, trait, attribute, directive, modifier, method, helper, testing assertion, and security claim is traceable to the current Context7 result and the loaded reference file.

## Decision Points
- Use component properties for small forms whose state and validation stay local to one component.
- Use a `Livewire\Form` object when the docs-confirmed task benefits from grouping form fields, validation, and create/update methods.
- Use `#[Validate]` for static attribute rules; use `rules()` when the docs-confirmed rules need Laravel `Rule` objects or other runtime syntax.
- Use request-triggering model modifiers for real-time validation; otherwise validation runs when an action such as `wire:submit` calls `$this->validate()`.
- Use `WithFileUploads` before binding file inputs with `wire:model`.

## Confirmed Core Patterns
- Livewire forms bind component properties or form-object properties with `wire:model` and submit to a component action with `wire:submit="save"`.
- `wire:submit` intercepts form submission, prevents the default browser submission, and calls the named Livewire action.
- Native controls documented with `wire:model` include text inputs, textareas, single checkboxes, checkbox groups, radio buttons, select dropdowns, and multi-select dropdowns.
- By default, `wire:model` changes do not send network requests until an action such as `wire:submit` or `wire:click` runs.
- Documented update modifiers include `.live`, `.blur`, `.change`, `.enter`, `.lazy`, `.debounce.Xms`, `.throttle.Xms`, `.number`, `.boolean`, `.fill`, `.deep`, and `.preserve-scroll`.
- `php artisan livewire:form PostForm` scaffolds a form object; documented form classes extend `Livewire\Form` and are used from components as typed public properties.
- Form-object template bindings prepend the form property name, such as `wire:model="form.title"` and `@error('form.title')`.
- `#[Validate]` attaches validation rules to properties; `$this->validate()` is still called before persistence in documented examples.
- `rules()` is documented for dynamic validation and Laravel `Rule` objects, and those rules run when `$this->validate()` is called.
- Manual validation controls documented for forms include `$this->addError()`, `$this->resetValidation()`, `$this->getErrorBag()`, `withValidator()`, custom validators, and `ValidationException` handling.
- File-upload forms use `Livewire\WithFileUploads`, file input `wire:model`, validation rules such as `image|max:1024`, and storage calls on uploaded files.
- Image uploads can use `temporaryUrl()` for previews; the docs state temporary URLs are only supported for image MIME types.
- Loading feedback can use `wire:loading` or automatic `data-loading` attributes; dirty feedback can use `wire:dirty` and `wire:dirty.class`.
- Custom form controls can forward `wire:model` through Blade attributes, use Alpine `x-modelable`, or use Livewire `#[Modelable]` on a child component property.
- Tests for forms use `Livewire::test()`, `set()`, `call()`, and `assertHasErrors()`; upload tests use Laravel fake files and fake storage in the documented examples.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact Forms topic.
- The answer does not include APIs, modifiers, helper methods, test assertions, upload behavior, or security guidance absent from the retrieved Livewire 4.x docs.
- All examples preserve documented Livewire 4 namespaces, traits, attributes, directive names, modifier names, method signatures, property paths, validation keys, and storage calls.
- Validation guidance distinguishes `#[Validate]`, `rules()`, manual error-bag helpers, and custom validators according to the retrieved docs.
- Upload guidance includes `WithFileUploads` and documented validation/storage behavior before using file inputs.
- Unconfirmed topics are explicitly left out or followed by a narrower Context7 lookup.