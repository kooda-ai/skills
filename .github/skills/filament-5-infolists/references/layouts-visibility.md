# Filament 5 Infolists: Layouts, Visibility, And Boundaries

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Infolists layout or visibility topic.

## Grid And Section
The retrieved docs show a schema containing `Grid` and `Section` layout components. In the auditing section, the schema contains `TextEntry` entries.

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

## Responsive Section Columns
The retrieved docs show `columns()` on a `Section`, with responsive Tailwind breakpoint keys. They also show `columnSpan()` and `columnOrder()` on schema components inside the grid.

```php
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Section;

Section::make()
    ->columns([
        'sm' => 3,
        'xl' => 6,
        '2xl' => 8,
    ])
    ->schema([
        TextInput::make('name')
            ->columnSpan([
                'default' => 1,
                'sm' => 2,
                'xl' => 3,
                '2xl' => 4,
            ])
            ->columnOrder([
                'default' => 2,
                'xl' => 1,
            ]),
        TextInput::make('email')
            ->columnSpan([
                'default' => 1,
                'xl' => 2,
            ])
            ->columnOrder([
                'default' => 1,
                'xl' => 2,
            ]),
        // ...
    ])
```

Use these layout methods with infolist entries only when the current Context7 lookup confirms the method is available for the schema component being used.

## Tabs
The retrieved docs show `Tabs::make()` with `tabs([...])`, and each `Tab::make()` can contain its own `schema([...])`.

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

## Entry Visibility
The retrieved docs show hiding an infolist entry with `hidden()` and using `visible()` as an alternative.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('role')
    ->hidden()
```

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('role')
    ->hidden(! FeatureFlag::active())
```

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('role')
    ->visible(FeatureFlag::active())
```

## Not Confirmed In Current Lookup
Do not add split layouts, fieldsets, repeatable layout details, collapsible sections, relation manager layout behavior, ViewRecord page navigation, infolist actions, entry suffix actions, hint actions, action modals, or schema action placement methods unless a narrower Context7 lookup returns them.
