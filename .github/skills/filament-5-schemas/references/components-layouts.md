# Filament 5 Schemas: Components And Layouts

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant component or layout topic.

## Mixed Form And Infolist Schema
The retrieved docs show a schema containing layout components, form components, and infolist entries together.

```php
use Filament\Forms\Components\Checkbox;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\TextInput;
use Filament\Infolists\Components\TextEntry;
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
                Section::make('Auditing')
                    ->schema([
                        TextEntry::make('created_at')
                            ->dateTime(),
                        TextEntry::make('updated_at')
                            ->dateTime(),
                    ]),
            ]),
    ]);
```

## Grid And Section
The docs show `Grid::make(2)` containing `Section::make(...)->schema([...])`. `Section` is used to group schema components.

```php
use Filament\Schemas\Components\Grid;
use Filament\Schemas\Components\Section;

Grid::make(2)
    ->schema([
        Section::make('Details')
            ->schema([
                // ...
            ]),
        Section::make('Auditing')
            ->schema([
                // ...
            ]),
    ])
```

## Tabs
The docs show `Tabs::make()` with `tabs([...])`, and each `Tab::make()` can contain its own `schema([...])`.

```php
use Filament\Schemas\Components\Tabs;
use Filament\Schemas\Components\Tabs\Tab;

Tabs::make('Tabs')
    ->tabs([
        Tab::make('Tab 1')
            ->schema([
                // ...
            ]),
        Tab::make('Tab 2')
            ->schema([
                // ...
            ]),
        Tab::make('Tab 3')
            ->schema([
                // ...
            ]),
    ])
```

## Builder Blocks
The docs show `Builder::make()` with `blocks([...])`. Each `Block::make()` has a unique name and a `schema([...])`; the example also uses `columns(2)` on a block.

```php
use Filament\Forms\Components\Builder;
use Filament\Forms\Components\Builder\Block;
use Filament\Forms\Components\FileUpload;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\Textarea;
use Filament\Forms\Components\TextInput;

Builder::make('content')
    ->blocks([
        Block::make('heading')
            ->schema([
                TextInput::make('content')
                    ->label('Heading')
                    ->required(),
                Select::make('level')
                    ->options([
                        'h1' => 'Heading 1',
                        'h2' => 'Heading 2',
                        'h3' => 'Heading 3',
                        'h4' => 'Heading 4',
                        'h5' => 'Heading 5',
                        'h6' => 'Heading 6',
                    ])
                    ->required(),
            ])
            ->columns(2),
        Block::make('paragraph')
            ->schema([
                Textarea::make('content')
                    ->label('Paragraph')
                    ->required(),
            ]),
        Block::make('image')
            ->schema([
                FileUpload::make('url')
                    ->label('Image')
                    ->image()
                    ->required(),
                TextInput::make('alt')
                    ->label('Alt text')
                    ->required(),
            ]),
    ])
```

## Confirmed Component Classes
The retrieved docs confirm these component classes and namespaces in schema examples:

- `Filament\Forms\Components\TextInput`
- `Filament\Forms\Components\MarkdownEditor`
- `Filament\Forms\Components\Checkbox`
- `Filament\Forms\Components\Select`
- `Filament\Forms\Components\Builder`
- `Filament\Forms\Components\Builder\Block`
- `Filament\Forms\Components\FileUpload`
- `Filament\Forms\Components\Textarea`
- `Filament\Infolists\Components\TextEntry`
- `Filament\Schemas\Components\Grid`
- `Filament\Schemas\Components\Section`
- `Filament\Schemas\Components\Tabs`
- `Filament\Schemas\Components\Tabs\Tab`

## Confirmed Component Methods
The retrieved docs confirm these methods in schema component examples: `make()`, `components()`, `schema()`, `options()`, `dateTime()`, `tabs()`, `blocks()`, `columns()`, `label()`, `required()`, and `image()`.

## Not Confirmed In Current Lookup
Do not add implementation details for fieldsets, flex, split layouts, repeaters, toggles, date pickers, rich editors, hidden or visible conditions, disabled or dehydrated state, relationships, or custom components unless a narrower Context7 lookup returns them.