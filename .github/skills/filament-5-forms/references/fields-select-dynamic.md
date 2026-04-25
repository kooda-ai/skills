# Fields, Select, and Dynamic Forms

Use this reference only after a fresh Context7 lookup confirms the requested field, Select, or dynamic Forms topic.

## Confirmed Components
The retrieved docs confirm these form component classes:

- `Filament\Forms\Components\TextInput`
- `Filament\Forms\Components\MarkdownEditor`
- `Filament\Forms\Components\RichEditor`
- `Filament\Forms\Components\Select`
- `Filament\Forms\Components\Checkbox`
- `Filament\Forms\Components\Toggle`
- `Filament\Forms\Components\FileUpload`

The retrieved docs also show these schema layout components used with form fields:

- `Filament\Schemas\Components\Grid`
- `Filament\Schemas\Components\Section`

Do not add other field classes such as date pickers, time pickers, color pickers, key-value fields, radio fields, checkbox lists, or tags inputs unless a narrower Context7 lookup confirms them for Filament 5.x.

## Editor and Boolean Fields
The retrieved docs confirm these simple component initializers:

```php
use Filament\Forms\Components\MarkdownEditor;

MarkdownEditor::make('content');
```

```php
use Filament\Forms\Components\RichEditor;

RichEditor::make('content');
```

```php
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin');
```

```php
use Filament\Forms\Components\Checkbox;

Checkbox::make('is_admin');
```

## Basic Field Schema
The retrieved docs confirm form fields inside `$schema->components([...])` and nested layout `schema([...])` calls.

```php
use Filament\Forms\Components\Checkbox;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Grid;
use Filament\Schemas\Components\Section;

$schema
    ->components([
        Grid::make(2)
            ->schema([
                Section::make('Details')
                    ->schema([
                        TextInput::make('name'),
                        Select::make('position')
                            ->options([
                                'developer' => 'Developer',
                                'designer' => 'Designer',
                            ]),
                        Checkbox::make('is_admin'),
                    ]),
            ]),
    ]);
```

## Select Options and Multiple Select
The retrieved docs confirm `Select::make(...)->options([...])` and `multiple()`.

```php
use Filament\Forms\Components\Select;

Select::make('technologies')
    ->multiple()
    ->options([
        'tailwind' => 'Tailwind CSS',
        'alpine' => 'Alpine.js',
        'laravel' => 'Laravel',
        'livewire' => 'Laravel Livewire',
    ]);
```

The retrieved docs state that when multiple selections are stored on an Eloquent model property, the property should be cast to `array`.

```php
protected function casts(): array
{
    return [
        'technologies' => 'array',
    ];
}
```

The retrieved docs also confirm `multiple(FeatureFlag::active())`.

## Select BelongsTo Relationship
The retrieved docs confirm `relationship()` on `Select` for a BelongsTo relationship, with a relationship name and title attribute.

```php
use Filament\Forms\Components\Select;

Select::make('author_id')
    ->relationship(name: 'author', titleAttribute: 'name');
```

## Creating Select Options in a Modal
The retrieved docs confirm `createOptionForm([...])` on a relationship Select.

```php
use Filament\Forms\Components\Select;

Select::make('author_id')
    ->relationship(name: 'author', titleAttribute: 'name')
    ->createOptionForm([
        Forms\Components\TextInput::make('name')
            ->required(),
        Forms\Components\TextInput::make('email')
            ->required()
            ->email(),
    ]);
```

Preserve the documented pattern unless a fresh lookup confirms a different import style.

## Dynamic Dependent Fields
The retrieved docs confirm dynamic fields by passing a function to `schema()` on a layout component. The example uses `Select::make('type')->live()`, `afterStateUpdated()`, a keyed `Grid`, `Get`, and conditional arrays of field components.

```php
use Filament\Forms\Components\FileUpload;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Grid;
use Filament\Schemas\Components\Utilities\Get;

Select::make('type')
    ->options([
        'employee' => 'Employee',
        'freelancer' => 'Freelancer',
    ])
    ->live()
    ->afterStateUpdated(fn (Select $component) => $component
        ->getContainer()
        ->getComponent('dynamicTypeFields')
        ->getChildSchema()
        ->fill());

Grid::make(2)
    ->schema(fn (Get $get): array => match ($get('type')) {
        'employee' => [
            TextInput::make('employee_number')
                ->required(),
            FileUpload::make('badge')
                ->image()
                ->required(),
        ],
        'freelancer' => [
            TextInput::make('hourly_rate')
                ->numeric()
                ->required()
                ->prefix('€'),
            FileUpload::make('contract')
                ->required(),
        ],
        default => [],
    })
    ->key('dynamicTypeFields');
```