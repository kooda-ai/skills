# Submission And Binding

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 form submission or `wire:model` topic.

## Basic Form Pattern
- A Livewire form submits with `wire:submit="save"` on the `<form>` element.
- `wire:submit` intercepts submission, prevents the default browser submission, and calls the named action on the server.
- The documented create form binds fields with `wire:model="title"` and `wire:model="content"`, then persists with data selected from the component properties.
- Documented examples validate before persistence and redirect after saving.
- Validation errors are displayed with Blade `@error('field') {{ $message }} @enderror`.

## Native Inputs
- Text input: `<input type="text" wire:model="title">`.
- Textarea: `<textarea wire:model="content"></textarea>`.
- For a textarea bound to a string property, Livewire populates the textarea from the property; do not manually interpolate the value inside the textarea when using `wire:model`.
- A single checkbox can bind to a boolean property.
- Multiple checkboxes with values can bind to an array property.
- Radio buttons bind the selected value to one property.
- A select dropdown binds the selected option value to one property.
- A multi-select dropdown binds selected values to an array property.

## Update Timing
- By default, `wire:model` updates do not send network requests by themselves.
- A network request is sent when an action runs, such as a `wire:submit` or `wire:click` action.
- `.live` sends updates to the server as the user types.
- The docs state that `.live` applies a default debounce to text input updates and that `.debounce.Xms` customizes it.
- `.throttle.Xms` throttles updates when used with `.live`.
- `.blur` updates when the input loses focus.
- `.change` updates when the element fires a change event, and is documented as useful for select elements.
- `.enter` updates when the user presses Enter.
- `.lazy` updates on change and sends a network request.

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
- `.deep` also listens to events from child elements when binding on a wrapper element.
- `.preserve-scroll` maintains scroll position during updates.

## Real-Time Validation Binding
- `#[Validate]` rules can run before server-side property updates.
- Real-time validation needs a model binding that sends a server request, such as a documented `.live` or `.blur` combination.
- The docs show `wire:model.live.blur="field"` with `@error('field')` for contact-style forms.