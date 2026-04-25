# Form Setup

Use this reference only after a fresh Context7 lookup confirms the requested Forms setup topic.

## Standalone Livewire Form
The retrieved docs confirm that a Livewire component using a Filament form:

- Implements `Filament\Schemas\Contracts\HasSchemas`.
- Uses `Filament\Schemas\Concerns\InteractsWithSchemas`.
- Defines a public nullable array property such as `public ?array $data = [];` for form state.
- Calls `$this->form->fill()` in `mount()`.
- Defines `form(Schema $schema): Schema` using `Filament\Schemas\Schema`.
- Configures fields with `components([...])`.
- Stores form state with `statePath('data')`.
- Reads validated form data with `$this->form->getState()` in the submit method.

Confirmed imports from the retrieved standalone form example:

```php
use Filament\Forms\Components\MarkdownEditor;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Concerns\InteractsWithSchemas;
use Filament\Schemas\Contracts\HasSchemas;
use Filament\Schemas\Schema;
use Illuminate\Contracts\View\View;
use Livewire\Component;
```

Confirmed standalone form skeleton:

```php
class CreatePost extends Component implements HasSchemas
{
    use InteractsWithSchemas;

    public ?array $data = [];

    public function mount(): void
    {
        $this->form->fill();
    }

    public function form(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('title')
                    ->required(),
                MarkdownEditor::make('content'),
            ])
            ->statePath('data');
    }

    public function create(): void
    {
        dd($this->form->getState());
    }
}
```

## Resource Form Delegation
The retrieved docs confirm a Resource `form()` method that delegates to a reusable form schema class.

```php
use App\Filament\Resources\Customers\Schemas\CustomerForm;
use Filament\Schemas\Schema;

public static function form(Schema $schema): Schema
{
    return CustomerForm::configure($schema);
}
```

## Reusable Form Schema Class
The retrieved docs confirm a reusable form schema class with `public static function configure(Schema $schema): Schema`.

```php
namespace App\Filament\Resources\Customers\Schemas;

use Filament\Forms\Components\TextInput;
use Filament\Schemas\Schema;

class CustomerForm
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('name'),
            ]);
    }
}
```

## Boundary With Schemas Skill
Forms are configured through `Filament\Schemas\Schema` in the retrieved docs. For schema layout behavior beyond the confirmed form examples, load the Filament 5 Schemas skill and run a fresh Context7 lookup for that exact topic.