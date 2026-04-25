---
name: livewire-4-validation-files
description: 'Use when: working with Livewire 4 Validation, validate(), #[Validate], rules(), real-time validation, form objects, validation errors, file uploads, WithFileUploads, temporaryUrl(), upload progress, cancel upload, JavaScript upload APIs, S3 temporary uploads, file downloads, response()->download(), streamDownload(), assertFileDownloaded(), and assertNoFileDownloaded(). Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 validation, upload, download, or validation/file test concern'
---

# Livewire 4 Validation And Files

## Purpose
Use this skill to create, review, or explain Livewire 4 validation, file upload, and file download features using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact validation, upload, or download topic.
2. Do not add validation APIs, upload methods, upload events, temporary storage behavior, S3 configuration, download response behavior, testing helpers, or examples unless they appear in the retrieved documentation.
3. If a detail is not confirmed by the retrieved docs, say the current documentation context did not confirm it and either run a narrower Context7 lookup or leave it out.
4. Keep examples close to documented snippets and preserve namespaces, traits, attributes, directive names, method names, parameter names, event names, config keys, and value strings.
5. Do not infer behavior from Livewire 3, Laravel controller habits beyond the retrieved docs, package source code, or memory.

## Covered Topics
- Validation with `validate()`, `#[Validate]`, `rules()`, form objects, real-time validation, manual errors, custom validators, JavaScript errors, and tests
- File uploads with `WithFileUploads`, `wire:model`, temporary previews, multiple uploads, progress, cancellation, JavaScript upload APIs, S3, and configuration
- File downloads with Laravel download responses, `streamDownload()`, and Livewire test assertions

## Workflow
1. Identify the concern: basic validation, attribute validation, runtime rules, real-time validation, form-object validation, manual error control, JavaScript error display, upload input, temporary preview, multiple upload, upload progress, S3 temporary upload, download response, or file-related tests.
2. Run a narrow Context7 query for the exact Livewire 4 topic before producing code or review findings.
3. For basic validation, use `$this->validate([...])` inside the action and render errors with Blade `@error` only as documented.
4. For co-located property rules, use `Livewire\Attributes\Validate`; remember that attribute validation runs before each property update, but `$this->validate()` should still run before persistence.
5. Use `onUpdate: false` on `#[Validate]` only when the docs-confirmed task needs to disable automatic property-update validation.
6. Use `as`, `message`, `translate: false`, multiple `#[Validate]` attributes, or array key syntax only according to the current docs.
7. For Laravel `Rule` objects or runtime validation syntax, use a `rules()` method, and add `messages()` or `validationAttributes()` only when documented by the current lookup.
8. For real-time validation with `rules()`, include an empty `#[Validate]` attribute when the docs-confirmed task needs rules to run on property updates.
9. For larger validation datasets, use a documented `Livewire\Form` object, a typed public form property, template keys such as `form.title`, and form methods such as `all()` or `validate()`.
10. For manual validation control, choose among `$this->addError()`, `$this->resetValidation()`, `$this->getErrorBag()`, `withValidator()`, custom validators, and `ValidationException` handling only when the current docs confirm the case.
11. For client-side validation display, use `$errors` methods such as `has()`, `first()`, `get()`, `all()`, and `clear()` as documented, and access them through `$wire.$errors` when using Alpine.
12. For file uploads, add `Livewire\WithFileUploads`, bind `<input type="file">` with `wire:model`, and avoid using `upload` as a component method or property name.
13. For storing uploads, use documented Laravel upload methods on the temporary upload, such as `store()`, `storeAs()`, `storePublicly()`, or `storePubliclyAs()`, preserving documented named arguments.
14. For multiple uploads, use a property array, an input with `multiple`, and validation rules like `photos.*` only as documented.
15. For image previews, use `temporaryUrl()` only for image MIME types and account for documented signed temporary URL behavior.
16. For upload feedback, use `wire:loading wire:target="property"`, `data-loading`, or the documented upload browser events: `livewire-upload-start`, `livewire-upload-finish`, `livewire-upload-cancel`, `livewire-upload-error`, and `livewire-upload-progress`.
17. For upload cancellation or custom JavaScript upload integrations, verify the exact current docs before using `$cancelUpload('photo')`, `$wire.cancelUpload('photo')`, `$wire.upload()`, `$wire.uploadMultiple()`, or `$wire.removeUpload()`.
18. For S3 temporary uploads, use `LIVEWIRE_TEMPORARY_FILE_UPLOAD_DISK=s3`, `php artisan livewire:config`, and `php artisan livewire:configure-s3-upload-cleanup` only as documented.
19. For downloads, return standard Laravel download responses such as `response()->download(...)`, `Storage::disk(...)->download(...)`, or `response()->streamDownload(...)` from a Livewire action.
20. For download tests, use `assertFileDownloaded('name.pdf')` or `assertNoFileDownloaded()` only as documented.
21. Finish by checking that every trait, attribute, method, directive, event name, config key, and test assertion is traceable to the current Context7 result.

## Confirmed Core Patterns
- `$this->validate()` validates component properties and returns the validated data.
- `#[Validate]` attaches rules to properties and runs them before property updates; `$this->validate()` should still be called before persisting.
- PHP attributes cannot support runtime syntaxes such as Laravel `Rule` objects, so those belong in `rules()`.
- `rules()` validation runs when `$this->validate()` is called unless an empty `#[Validate]` attribute is used for real-time property-update validation.
- Real-time validation requires network-triggering bindings such as `wire:model.live` or `wire:model.live.blur`.
- Form objects extend `Livewire\Form`, are assigned to typed public component properties, and use template paths prefixed by the form property name.
- Manual validation error helpers include `addError()`, `resetValidation()`, and `getErrorBag()`.
- Livewire catches `ValidationException` exceptions thrown inside components and provides the errors to the view.
- Validation tests use `Livewire::test()`, `set()`, `call()`, and `assertHasErrors()`.
- File uploads require `WithFileUploads` before using `wire:model` on file inputs.
- Livewire stores uploads temporarily, then the public property is set to the temporary uploaded file for validation or storage.
- The method or property name `upload` is reserved by Livewire.
- `temporaryUrl()` is restricted to image MIME types for temporary previews.
- Direct S3 temporary uploads use the `LIVEWIRE_TEMPORARY_FILE_UPLOAD_DISK` environment variable and require cleanup configuration for old temporary files.
- File uploads have dedicated browser events for start, finish, cancel, error, and progress states.
- Livewire file downloads are handled by sending Base64-encoded file contents to the frontend and decoding them into a client-side download.
- Streaming downloads are supported, but the download is not triggered until the contents are collected and delivered to the browser.
- File download tests use `assertFileDownloaded()` and `assertNoFileDownloaded()`.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact validation, upload, or download feature.
- No validation helper, upload behavior, upload event, S3 option, download behavior, or testing assertion absent from the retrieved Livewire 4.x docs was added.
- Validation guidance distinguishes `validate()`, `#[Validate]`, `rules()`, form objects, real-time validation, and manual error helpers.
- Upload guidance includes `WithFileUploads` and avoids the reserved `upload` method or property name.
- Download guidance uses Laravel download responses and documents Livewire's Base64 handling only when relevant.
- Tests use only the file and validation assertions confirmed by the current docs.
