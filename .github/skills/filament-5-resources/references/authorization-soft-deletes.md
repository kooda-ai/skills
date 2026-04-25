# Filament 5 Resources: Authorization And Soft Deletes

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Resource authorization, deleting records, or soft-delete topic.

## Resource Authorization
The retrieved Resource docs state that Filament handles authorization by observing Laravel model policies registered in the application.

## List Page Authorization
The retrieved docs state that users can access the List page if the `viewAny()` method of the model policy returns `true`.

The docs also state that the `reorder()` policy method controls reordering records within the table.

## Edit Page Authorization
The retrieved docs state that users can access the Edit page if the `update()` method of the corresponding model policy returns `true`.

The docs state that users can delete a record if the `delete()` policy method returns `true`.

## Delete Authorization
The retrieved docs state that users can delete records if the `delete()` policy method returns `true`.

For bulk delete operations, the docs state that Filament uses the `deleteAny()` method to improve performance by avoiding individual record checks.

## Soft-delete Authorization
The retrieved docs state that when using soft-deletes, Filament uses specific policy methods for force-deletion and restoration.

- `forceDelete()` controls individual force-delete actions.
- `restore()` controls individual restore actions.
- `forceDeleteAny()` controls bulk force-delete operations.
- `restoreAny()` controls bulk restore operations.

## Generate Resource With Soft Deletes
The retrieved docs confirm `--soft-deletes` for generating a Resource with soft-delete functionality by default.

```bash
php artisan make:filament-resource Customer --soft-deletes
```

The docs state that Filament does not allow interaction with soft-deleted records by default. Use `--soft-deletes` when generating a new Resource to enable restoring, force-deleting, and filtering trashed records.

## Delete Action In Resource Table
The retrieved docs confirm adding `DeleteAction` to table `recordActions()` for deleting individual records directly from the Resource table.

```php
use Filament\Actions\DeleteAction;
use Filament\Tables\Table;

public static function table(Table $table): Table
{
    return $table
        ->columns([
            // ...
        ])
        ->recordActions([
            // ...
            DeleteAction::make(),
        ]);
}
```

## Soft Deletes In Existing Resource Table
The retrieved docs confirm this Resource table setup for filtering, deleting, force-deleting, and restoring trashed records.

```php
use Filament\Actions\BulkActionGroup;
use Filament\Actions\DeleteAction;
use Filament\Actions\DeleteBulkAction;
use Filament\Actions\ForceDeleteAction;
use Filament\Actions\ForceDeleteBulkAction;
use Filament\Actions\RestoreAction;
use Filament\Actions\RestoreBulkAction;
use Filament\Tables\Filters\TrashedFilter;
use Filament\Tables\Table;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\SoftDeletingScope;

public static function table(Table $table): Table
{
    return $table
        ->columns([
            // ...
        ])
        ->filters([
            TrashedFilter::make(),
            // ...
        ])
        ->recordActions([
            // You may add these actions to your table if you're using a simple
            // resource, or you just want to be able to delete records without
            // leaving the table.
            DeleteAction::make(),
            ForceDeleteAction::make(),
            RestoreAction::make(),
            // ...
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DeleteBulkAction::make(),
                ForceDeleteBulkAction::make(),
                RestoreBulkAction::make(),
                // ...
            ]),
        ]);
}

public static function getRecordRouteBindingEloquentQuery(): Builder
{
    return parent::getRecordRouteBindingEloquentQuery()
        ->withoutGlobalScopes([
            SoftDeletingScope::class,
        ]);
}
```

## Soft Deletes In Existing Resource Edit Page
The retrieved docs confirm adding delete, force-delete, and restore actions to the header of a Resource Edit page.

```php
use Filament\Actions;

protected function getHeaderActions(): array
{
    return [
        Actions\DeleteAction::make(),
        Actions\ForceDeleteAction::make(),
        Actions\RestoreAction::make(),
        // ...
    ];
}
```

## Soft Deletes In Relation Manager
The retrieved docs confirm soft-deleting support in a relation manager by removing `SoftDeletingScope` from the table query and adding `TrashedFilter`, delete, force-delete, restore, and related bulk actions.

```php
use Filament\Actions\DeleteAction;
use Filament\Actions\DeleteBulkAction;
use Filament\Actions\ForceDeleteAction;
use Filament\Actions\ForceDeleteBulkAction;
use Filament\Actions\RestoreAction;
use Filament\Actions\RestoreBulkAction;
use Filament\Tables\Filters\TrashedFilter;
use Filament\Tables\Table;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\SoftDeletingScope;

public function table(Table $table): Table
{
    return $table
        ->modifyQueryUsing(fn (Builder $query) => $query->withoutGlobalScopes([
            SoftDeletingScope::class,
        ]))
        ->columns([
            // ...
        ])
        ->filters([
            TrashedFilter::make(),
            // ...
        ])
        ->recordActions([
            DeleteAction::make(),
            ForceDeleteAction::make(),
            RestoreAction::make(),
            // ...
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DeleteBulkAction::make(),
                ForceDeleteBulkAction::make(),
                RestoreBulkAction::make(),
                // ...
            ]),
        ]);
}
```

The retrieved snippet uses `BulkActionGroup::make()` but did not include its import. Do not invent missing imports unless a fresh Context7 lookup returns them.

## Not Confirmed In Current Lookup
Do not add implementation details for skipping authorization, `authorizeResourceAccess`, full policy class examples, `can*` Resource methods, testing patterns, or soft-delete model setup unless a narrower Context7 lookup returns them.