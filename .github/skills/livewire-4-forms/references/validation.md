# Validation

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 validation topic.

## Core Validation Flow
- Livewire builds on Laravel validation.
- Component actions can call `$this->validate()` before persisting form data.
- `$this->validate()` returns validated data in documented examples.
- Blade `@error('field') {{ $message }} @enderror` displays validation errors.

## Validate Attribute
- Use `Livewire\Attributes\Validate` as `#[Validate(...)]` on component or form-object properties.
- The documented attribute signature includes `rule`, `attribute`, `as`, `message`, `onUpdate`, and `translate` parameters.
- `#[Validate('required|min:3')]` attaches rules to a property.
- `#[Validate]` rules run before each server-side property update.
- The docs still call `$this->validate()` before persistence so untouched properties are validated too.
- `#[Validate('required|min:3', onUpdate: false)]` disables automatic validation on property updates and leaves validation to explicit `$this->validate()` calls.
- `#[Validate('required', as: 'date of birth')]` customizes the attribute name in validation messages.
- `#[Validate('required', message: 'Please provide a post title')]` customizes the validation message.
- Multiple `#[Validate]` attributes can provide different messages for different rules on one property.
- Array syntax can define rules and messages for array fields such as `titles` and `titles.*`.
- `#[Validate(..., translate: false)]` opts out of Laravel translation for the provided validation message.

## Rules Method
- Define a protected `rules()` method when PHP attributes are not suitable for a rule.
- `rules()` is documented for runtime syntax such as Laravel `Rule` objects.
- Rules from `rules()` apply when `$this->validate()` is called.
- The docs state that `rules()` does not run validation on data updates by itself.
- Add an empty `#[Validate]` attribute to a property when using `rules()` but wanting real-time validation behavior confirmed by the docs.
- `messages()` customizes validation messages.
- `validationAttributes()` customizes attribute names.

## Manual Error Control
- `$this->addError('key', 'message')` manually adds a validation message.
- `$this->resetValidation('key')` resets validation errors for one key.
- `$this->resetValidation()` resets all validation errors.
- `$this->getErrorBag()` retrieves the underlying Laravel error bag.
- Inside form objects, errors added with `$this->addError()` are prefixed with the form property name assigned in the parent component.

## Validator Customization
- `withValidator()` gives access to the validator instance before rules are evaluated.
- The docs show registering `withValidator()` inside `boot()` and adding errors in an `after()` callback.
- Custom validation logic can manually use `Validator::make(...)->validate()`.
- If a `ValidationException` is thrown inside a component, Livewire catches it and provides the errors to the view.

## JavaScript Errors
- Livewire exposes a `$errors` magic property in JavaScript-capable Blade expressions.
- The docs show `$errors.has('email')` and `$errors.first('email')`.
- The validation docs describe `$errors` methods for checking, retrieving, and clearing validation errors.
- In Alpine components, validation errors can be accessed through `$wire.$errors`.

## Real-Time Validation
- Real-time validation requires a request-triggering model binding such as a documented `.live` or `.blur` usage.
- The docs show `wire:model.live.blur="name"` with `#[Validate(...)]` and matching `@error('name')` output.
- When using `rules()` for dynamic rules, an empty `#[Validate]` attribute can enable real-time validation behavior on the property.