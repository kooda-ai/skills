# Filament 5 Resources: Pages And Navigation

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Resource pages or navigation topic.

## Register Pages In A Resource
The retrieved docs confirm `getPages()` for registering Resource pages and routes.

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

Use only route keys, page classes, and route strings confirmed by the current lookup.

## Add A View Page
The retrieved docs confirm this command for generating a View page class for an existing Resource.

```bash
php artisan make:filament-page ViewUser --resource=UserResource --type=ViewRecord
```

After generating the View page, the docs show registering it in `getPages()`.

```php
public static function getPages(): array
{
    return [
        'index' => Pages\ListUsers::route('/'),
        'create' => Pages\CreateUser::route('/create'),
        'view' => Pages\ViewUser::route('/{record}'),
        'edit' => Pages\EditUser::route('/{record}/edit'),
    ];
}
```

## Resource Record Sub-navigation
The retrieved docs confirm `getRecordSubNavigation()` for navigation items related to a particular record within the Resource.

```php
use Filament\Resources\Pages\Page;

public static function getRecordSubNavigation(Page $page): array
{
    return $page->generateNavigationItems([
        ViewCustomer::class,
        EditCustomer::class,
        EditCustomerContact::class,
        ManageCustomerAddresses::class,
        ManageCustomerPayments::class,
    ]);
}
```

The relation page example also shows importing page classes from the application Resource namespace before using them in sub-navigation.

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

## Navigation Label
The retrieved docs confirm `$navigationLabel` for customizing a Resource item label in the Filament navigation menu.

```php
protected static ?string $navigationLabel = 'Mis Clientes';
```

## Navigation Icon
The retrieved docs confirm `$navigationIcon` for changing the icon displayed next to the navigation item.

```php
use BackedEnum;
use Filament\Support\Icons\Heroicon;

protected static string | BackedEnum | null $navigationIcon = Heroicon::OutlinedDocumentText;
```

The docs state that the icon must be a valid Filament icon identifier and that the `Heroicon` or `BackedEnum` use statement should be present.

## Navigation Group
The retrieved docs confirm `$navigationGroup` for grouping a Resource navigation item under a category in the sidebar.

```php
use UnitEnum;

protected static string | UnitEnum | null $navigationGroup = 'Shop';
```

## Navigation Parent Item
The retrieved docs confirm `$navigationParentItem` for nesting the current Resource under a parent navigation item. The docs state that `$navigationGroup` should also be set if the parent is grouped.

```php
use UnitEnum;

protected static ?string $navigationParentItem = 'Products';

protected static string | UnitEnum | null $navigationGroup = 'Shop';
```

## Navigation Sort
The retrieved docs confirm `$navigationSort` for controlling the Resource navigation item's position in the menu.

```php
protected static ?int $navigationSort = 2;
```

## Navigation Badge
The retrieved docs confirm `getNavigationBadge()` for displaying a badge next to a navigation item.

```php
public static function getNavigationBadge(): ?string
{
    return static::getModel()::count();
}
```

## Navigation Badge Color
The retrieved docs confirm `getNavigationBadgeColor()` for setting the navigation badge color.

```php
public static function getNavigationBadgeColor(): ?string
{
    return static::getModel()::count() > 10 ? 'warning' : 'primary';
}
```

The docs mention predefined color strings like `warning`, `primary`, and `danger`.

## Navigation Badge Tooltip
The retrieved docs confirm `$navigationBadgeTooltip` for a static badge tooltip and `getNavigationBadgeTooltip()` for a dynamic tooltip.

```php
protected static ?string $navigationBadgeTooltip = 'The number of users';
```

```php
public static function getNavigationBadgeTooltip(): ?string
{
    return 'The number of users';
}
```

## Hide From Navigation
The retrieved docs confirm `$shouldRegisterNavigation = false` and `shouldRegisterNavigation()` for preventing Resources or pages from appearing in navigation.

```php
protected static bool $shouldRegisterNavigation = false;
```

```php
public static function shouldRegisterNavigation(): bool
{
    return false;
}
```

## Plural Model Label
The retrieved docs confirm `$pluralModelLabel` for customizing a Resource plural label.

```php
protected static ?string $pluralModelLabel = 'clientes';
```

The docs state that this overrides the default pluralization of the model label.

## Not Confirmed In Current Lookup
Do not add implementation details for clusters, page titles, breadcrumbs, navigation badge polling/caching, or authorization unless a narrower Context7 lookup returns them.