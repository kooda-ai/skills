# Validation, Forms, And Uploads

## Validation Tests
- The retrieved Testing docs assert validation errors with `assertHasErrors()`.
- Confirmed required-field shape: `assertHasErrors('title')` after setting `title` to an empty value and calling `save`.
- Confirmed rule-specific shape: `assertHasErrors(['title' => ['min:3']])` after setting `title` to a too-short value and calling `save`.
- Keep the action name, property name, and rule name aligned with the current docs and component under test.

## Form Object Context
- The retrieved Forms docs confirm form classes extending `Livewire\Form`.
- The retrieved Forms docs confirm `#[Validate(...)]` attributes on form properties.
- The retrieved Forms docs confirm a component can declare a typed public form property, call `$this->validate()`, and persist `$this->form->only([...])`.
- The retrieved Forms docs confirm a `rules()` method for validation rules that need Laravel `Rule` objects.
- The current Testing excerpts did not confirm a form-object-specific test property path. Run a narrower Context7 lookup before using paths such as `form.title` inside `set()` or `assertHasErrors()`.

## File Upload Tests
- The retrieved Uploads docs test file uploads with Laravel fake storage and fake uploaded files.
- Confirmed setup helpers include `Storage::fake('avatars')` and `UploadedFile::fake()->image('avatar.png')`.
- Confirmed Livewire flow: `Livewire::test(UploadPhoto::class)->set('photo', $file)->call('upload', 'uploaded-avatar.png')`.
- Confirmed storage assertion: `Storage::disk('avatars')->assertExists('uploaded-avatar.png')`.
- The retrieved component example includes `WithFileUploads`, a public `$photo` property, and storing the uploaded file with `storeAs('/', $name, disk: 'avatars')`.

## Cautions
- Confirm the exact upload trait namespace in the current Context7 result before writing imports.
- Do not add temporary URL, multiple upload, validation, or storage cleanup test claims unless the current query returns them.
- Do not replace the documented fake upload flow with browser automation unless the docs for the task confirm that approach.