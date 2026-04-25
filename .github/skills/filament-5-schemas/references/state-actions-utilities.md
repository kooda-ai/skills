# Filament 5 Schemas: State, Actions, And Utilities

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant state, action, or utility injection topic.

## State Path, Fill, And Get State
The retrieved docs show a Livewire form schema storing state at `data`, filling the form in `mount()`, and reading the submitted state through `getState()`.

```php
public ?array $data = [];

public function mount(): void
{
    $this->form->fill();
}

public function form(Schema $schema): Schema
{
    return $schema
        ->components([
            // ...
        ])
        ->statePath('data');
}

public function create(): void
{
    dd($this->form->getState());
}
```

## Schema Component Utility Injection
The retrieved docs state that many configuration methods accept functions for dynamic customization. These functions can inject utilities such as `$get`, `$record`, and `$operation`.

Documented schema component utility injection parameters:

- `$component`: the current `Filament\Schemas\Components\Component` instance.
- `$get`: a `Filament\Schemas\Components\Utilities\Get` function for retrieving values from the current schema data. Validation is not run on form fields.
- `$model`: the Eloquent model FQN for the current schema.
- `$livewire`: the `Livewire\Component` instance.
- `$operation`: the current operation being performed by the schema, usually `create`, `edit`, or `view`.
- `$record`: the Eloquent record for the current schema.

## Actions Inside Schemas
The retrieved docs show `Filament\Actions\Action` embedded in a schema component slot with `afterContent()`. The action can inject schema get and set utilities.

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
    )

TextInput::make('slug')
```

## Action Utility Injection
The retrieved docs list these variables as available within Filament 5.x actions:

- `$action`: the current `Filament\Actions\Action` instance.
- `$arguments`: the array of arguments passed to the action when it was triggered.
- `$data`: data submitted from form fields in the action modal; empty before the modal form is submitted.
- `$livewire`: the `Livewire\Component` instance.
- `$model`: the Eloquent model FQN for the current action, if one is attached.
- `$record`: the Eloquent record for the current action, if one is attached.
- `$selectedRecords`: selected Eloquent records for bulk actions only.
- `$mountedActions`: the actions currently mounted in the Livewire component.
- `$schema`: the `Filament\Schemas\Schema` object that the action belongs to, for actions in schemas only.
- `$schemaComponent`: the schema component that the action belongs to, for actions in schemas only.
- `$schemaGet`: a function for retrieving values from schema data, for actions in schemas only. Validation is not run on form fields.
- `$schemaSet`: a function for setting values in schema data, for actions in schemas only.
- `$schemaComponentState`: the current value of the schema component, for actions in schemas only.
- `$schemaOperation`: the current schema operation, usually `create`, `edit`, or `view`, for actions in schemas only.
- `$schemaState`: the current value of the schema that the action belongs to, for actions in schemas only.
- `$table`: the `Filament\Tables\Table` object that the action belongs to, for actions in tables only.

## Not Confirmed In Current Lookup
Do not add implementation details for lifecycle hooks, validation behavior beyond shown `required()` examples, reactive state updates, relationship state, model state, custom operations, or schema action placement methods other than `afterContent()` unless a narrower Context7 lookup returns them.