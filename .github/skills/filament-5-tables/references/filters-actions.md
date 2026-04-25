# Filament 5 Tables: Filters And Actions

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant filter or action topic.

## Available Filters
The retrieved docs state that `Filter::make()` renders a checkbox by default. When checked, the associated `query()` is activated.

The docs also mention these alternatives:

- Toggle buttons for a simpler on/off state.
- Select filters for predefined options.
- Ternary filters for true, false, and blank states, especially for boolean columns.
- A dedicated trashed filter for soft-deletable records.

Only use implementation details below when the current Context7 result confirms them.

## SelectFilter With Options

```php
use Filament\Tables\Filters\SelectFilter;

SelectFilter::make('status')
    ->options([
        'draft' => 'Draft',
        'reviewing' => 'Reviewing',
        'published' => 'Published',
    ])
```

## SelectFilter With Relationship

```php
use Filament\Tables\Filters\SelectFilter;

SelectFilter::make('parent')
    ->relationship('parent', 'name')
    ->searchable()
    ->preload()
```

## TrashedFilter

```php
use Filament\Tables\Filters\TrashedFilter;

TrashedFilter::make()
```

## Record And Toolbar Actions
Use `recordActions()` for row-specific actions and `toolbarActions()` for toolbar and bulk actions.

```php
use App\Models\Post;
use Filament\Actions\Action;
use Filament\Actions\BulkActionGroup;
use Filament\Actions\DeleteBulkAction;
use Filament\Tables\Table;

public function table(Table $table): Table
{
    return $table
        ->columns([
            // ...
        ])
        ->recordActions([
            Action::make('feature')
                ->action(function (Post $record) {
                    $record->is_featured = true;
                    $record->save();
                })
                ->hidden(fn (Post $record): bool => $record->is_featured),
            Action::make('unfeature')
                ->action(function (Post $record) {
                    $record->is_featured = false;
                    $record->save();
                })
                ->visible(fn (Post $record): bool => $record->is_featured),
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DeleteBulkAction::make(),
            ]),
        ]);
}
```

## BulkActionGroup
Use `BulkActionGroup` to group multiple bulk actions into a dropdown. The docs state that actions outside the group render next to the dropdown trigger.

```php
use Filament\Actions\BulkAction;
use Filament\Actions\BulkActionGroup;
use Filament\Tables\Table;
use Illuminate\Support\Collection;

public function table(Table $table): Table
{
    return $table
        ->toolbarActions([
            BulkActionGroup::make([
                BulkAction::make('delete')
                    ->requiresConfirmation()
                    ->action(fn (Collection $records) => $records->each->delete()),
                BulkAction::make('forceDelete')
                    ->requiresConfirmation()
                    ->action(fn (Collection $records) => $records->each->forceDelete()),
            ]),
            BulkAction::make('export')
                ->button()
                ->action(fn (Collection $records) => ...),
        ]);
}
```

## External API Delete Action
The custom data docs show `Action::make()`, `color()`, `icon()`, `modalIcon()`, `modalHeading()`, `requiresConfirmation()`, and `action()` for a table action that deletes an external API record.

```php
use Filament\Actions\Action;
use Filament\Notifications\Notification;
use Filament\Support\Icons\Heroicon;
use Filament\Tables\Columns\TextColumn;
use Filament\Tables\Table;
use Illuminate\Support\Facades\Http;

public function table(Table $table): Table
{
    $baseUrl = 'https://dummyjson.com';

    return $table
        ->records(fn (): array => Http::baseUrl($baseUrl)
            ->get('products')
            ->collect()
            ->get('products', [])
        )
        ->columns([
            TextColumn::make('title'),
            TextColumn::make('category'),
            TextColumn::make('price')
                ->money(),
        ])
        ->recordActions([
            Action::make('delete')
                ->color('danger')
                ->icon(Heroicon::Trash)
                ->modalIcon(Heroicon::OutlinedTrash)
                ->modalHeading('Delete Product')
                ->requiresConfirmation()
                ->action(function (array $record) use ($baseUrl) {
                    $response = Http::baseUrl($baseUrl)
                        ->delete("products/{$record['id']}");

                    if ($response->failed()) {
                        Notification::make()
                            ->title('Product failed to delete')
                            ->danger()
                            ->send();

                        return;
                    }

                    Notification::make()
                        ->title('Product deleted')
                        ->success()
                        ->send();
                }),
        ]);
}
```

## Action Utility Injections
For Filament 5.x actions, documented injectable context includes `$action`, `$arguments`, `$data`, `$livewire`, `$model`, `$record`, `$selectedRecords`, `$mountedActions`, `$schema`, `$schemaComponent`, `$schemaGet`, `$schemaSet`, `$schemaComponentState`, `$schemaOperation`, `$schemaState`, and `$table`.

## Not Confirmed In Current Lookup
Do not add implementation details for filter forms, filter indicators, default filters, `TernaryFilter` code, `Filter::make()->query()` code, `headerActions()`, `EditAction`, `ViewAction`, or action modal forms unless a narrower Context7 lookup returns them.