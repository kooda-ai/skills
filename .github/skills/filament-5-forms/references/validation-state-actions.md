# Validation, State, and Actions

Use this reference only after a fresh Context7 lookup confirms the requested validation, state lifecycle, or schema action topic.

## Required and Field-Specific Validation Calls
The retrieved docs confirm these validation-related or input-specific calls in Forms snippets:

- `required()` on `TextInput`, `FileUpload`, and `Forms\Components\TextInput` inside `createOptionForm()`.
- `email()` on `Forms\Components\TextInput` inside `createOptionForm()`.
- `numeric()` on `TextInput`.
- `rules([...])` on `TextInput`.
- `required(fn (...) => ...)` for conditionally required fields when confirmed by the current lookup.

Do not add other validation methods, messages, unique rules, min/max rules, dehydration rules, or relationship-saving behavior unless a fresh Context7 lookup confirms them.

## Conditional Visibility and Required Fields
The retrieved docs confirm `hidden()` on a form field with either a boolean or a function. Utility injection such as `Get` can be used in the function when the current lookup confirms it.

```php
use Filament\Forms\Components\TextInput;

TextInput::make('name')
    ->hidden(! FeatureFlag::active());
```

The retrieved docs also confirm conditionally required fields by passing a function to `required()`. Use this only when the current lookup confirms the needed utility and condition.

## Closure Rules With `Get`
The retrieved docs confirm wrapping a closure validation rule in another function so `Get` can be injected and used to read another field value.

```php
use Closure;
use Filament\Schemas\Components\Utilities\Get;

TextInput::make('slug')->rules([
    fn (Get $get): Closure => function (string $attribute, $value, Closure $fail) use ($get) {
        if ($get('other_field') === 'foo' && $value !== 'bar') {
            $fail("The {$attribute} is invalid.");
        }
    },
]);
```

## Updating State With `afterStateUpdated()`
The retrieved docs confirm `live(onBlur: true)` and `afterStateUpdated()` for generating a slug from a title. The example injects `Set` and receives `?string $state`.

```php
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Utilities\Set;
use Illuminate\Support\Str;

TextInput::make('title')
    ->live(onBlur: true)
    ->afterStateUpdated(fn (Set $set, ?string $state) => $set('slug', Str::slug($state)));

TextInput::make('slug');
```

## Actions Inside Schemas
The retrieved docs confirm inserting an `Action` into a schema component, including a form field slot through `afterContent()`. The action can use `Get $schemaGet` and `Set $schemaSet` utilities to read and modify form state.

```php
use Filament\Actions\Action;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Utilities\Get;
use Filament\Schemas\Components\Utilities\Set;

TextInput::make('title')
    ->afterContent(
        Action::make('generateSlug')
            ->action(function (Get $schemaGet, Set $schemaSet) {
                $schemaSet('slug', str($schemaGet('title'))->slug());
            })
    );

TextInput::make('slug');
```

## Dependent Fields Need a Server Request
The retrieved docs state that reactive updates require the field to be configured with `live()`, because the schema only refreshes on user interaction that triggers a server request otherwise.