# Filament 5 Actions: Setup And Utilities

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Actions setup or utility injection topic.

## Livewire Component Action Support
The retrieved docs state that a Livewire component must implement `HasActions` and `HasSchemas`, and use the corresponding traits to enable Filament action and schema functionality.

```php
use Filament\Actions\Concerns\InteractsWithActions;
use Filament\Actions\Contracts\HasActions;
use Filament\Schemas\Concerns\InteractsWithSchemas;
use Filament\Schemas\Contracts\HasSchemas;
use Livewire\Component;

class ManagePost extends Component implements HasActions, HasSchemas
{
    use InteractsWithActions;
    use InteractsWithSchemas;

    // ...
}
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

## ActionGroup Utility Injection
The retrieved docs list these variables for Filament 5.x action groups:

- `$group`: the current `Filament\Actions\ActionGroup` instance.
- `$livewire`: the `Livewire\Component` instance.
- `$model`: the Eloquent model FQN for the current action group, if one is attached.
- `$record`: the Eloquent record for the current action group, if one is attached.
- `$mountedActions`: the actions currently mounted in the Livewire component.

## Not Confirmed In Current Lookup
Do not add standalone action rendering syntax, generated action method naming, keyboard shortcut behavior, authorization behavior, testing helpers, or transaction behavior unless a narrower Context7 lookup returns them.