# Filament 5 Resources: Relationships And Search

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Resource relationship or search topic.

## Relation Managers
The retrieved docs confirm `getRelations()` for registering relation managers in a Resource.

```php
public static function getRelations(): array
{
    return [
        RelationManagers\PostsRelationManager::class,
    ];
}
```

The docs state that registering the generated relation manager makes it accessible and tells Filament it can load the relation manager.

## Relation Pages
The retrieved docs confirm relation pages registered through `getPages()`.

```php
public static function getPages(): array
{
    return [
        'index' => Pages\ListCustomers::route('/'),
        'create' => Pages\CreateCustomer::route('/create'),
        'view' => Pages\ViewCustomer::route('/{record}'),
        'edit' => Pages\EditCustomer::route('/{record}/edit'),
        'addresses' => Pages\ManageCustomerAddresses::route('/{record}/addresses'),
    ];
}
```

The docs state that when creating a relation page, the user is prompted for details like the relationship name and title attribute.

The docs also state that using a relation page means a separate relation manager does not need to be generated or registered.

## Relation Page Sub-navigation
The retrieved docs confirm adding a relation page to Resource record sub-navigation with `getRecordSubNavigation()` and `$page->generateNavigationItems()`.

```php
use App\Filament\Resources\Customers\Pages;
use Filament\Resources\Pages\Page;

public static function getRecordSubNavigation(Page $page): array
{
    return $page->generateNavigationItems([
        // ...
        Pages\ManageCustomerAddresses::class,
    ]);
}
```

## Global Search Record Title
The retrieved docs confirm `$recordTitleAttribute` for choosing the model attribute used as the global search result title.

```php
protected static ?string $recordTitleAttribute = 'title';
```

The docs state that the attribute must exist on the model.

## Authorization Note
Use [authorization-soft-deletes.md](./authorization-soft-deletes.md) for Resource authorization and soft-delete behavior. Do not use action-only authorization snippets as Resource policy guidance unless a fresh Resource-specific Context7 lookup confirms the topic.

## Not Confirmed In Current Lookup
Do not add implementation details for relation manager generation commands, attach/associate actions, relationship table columns, child Resource classes, parent Resource APIs, or global search result details beyond `$recordTitleAttribute` unless a narrower Context7 lookup returns them.