# Filament 5 Schemas: Setup

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Schemas setup topic.

## Livewire Component With Form Schema
The retrieved docs show a Livewire component implementing `HasSchemas`, using `InteractsWithSchemas`, defining a `form(Schema $schema): Schema` method, filling the form in `mount()`, and reading submitted state with `$this->form->getState()`.

```php
<?php

namespace App\Livewire;

use Filament\Forms\Components\MarkdownEditor;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Concerns\InteractsWithSchemas;
use Filament\Schemas\Contracts\HasSchemas;
use Filament\Schemas\Schema;
use Illuminate\Contracts\View\View;
use Livewire\Component;

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
                // ...
            ])
            ->statePath('data');
    }

    public function create(): void
    {
        dd($this->form->getState());
    }

    public function render(): View
    {
        return view('livewire.create-post');
    }
}
```

## Minimum Livewire Schema Setup
The docs identify `HasSchemas` and `InteractsWithSchemas` as required for a Livewire component to use Filament schema functionality.

```php
use Filament\Schemas\Concerns\InteractsWithSchemas;
use Filament\Schemas\Contracts\HasSchemas;
use Livewire\Component;

class ViewProduct extends Component implements HasSchemas
{
    use InteractsWithSchemas;

    // ...
}
```

## Reusable Form Schema Class
The docs show reusable schema classes for Resource code organization. The documented pattern uses `configure(Schema $schema): Schema` and returns `$schema->components([...])`.

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
                // ...
            ]);
    }
}
```

## Resource Form Schema Delegation
The retrieved docs show Resource form methods delegating to reusable schema classes.

```php
use App\Filament\Resources\Customers\Schemas\CustomerForm;
use Filament\Schemas\Schema;

public static function form(Schema $schema): Schema
{
    return CustomerForm::configure($schema);
}
```

## Resource Infolist Schema Delegation
The retrieved docs show Resource infolist methods delegating to reusable schema classes.

```php
use App\Filament\Resources\Customers\Schemas\CustomerInfolist;
use Filament\Schemas\Schema;

public static function infolist(Schema $schema): Schema
{
    return CustomerInfolist::configure($schema);
}
```

## Not Confirmed In Current Lookup
Do not add implementation details for Blade rendering, multiple schema names, model binding, relationship saving, or schema generation commands unless a narrower Context7 lookup returns them.