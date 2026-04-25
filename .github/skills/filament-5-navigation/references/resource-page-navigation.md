# Resource And Page Navigation

Use this reference only after a fresh Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Filament 5 Resource or Page navigation topic.

## Navigation Labels
The retrieved docs confirm that Resource navigation items use the Resource plural label by default and that `$navigationLabel` customizes the item label.

```php
protected static ?string $navigationLabel = 'Mis Clientes';
```

When the current lookup confirms dynamic labels for the target surface, use `getNavigationLabel(): string`.

## Navigation Icons
The retrieved docs confirm `$navigationIcon` for a navigation item icon.

```php
use BackedEnum;

protected static string | BackedEnum | null $navigationIcon = 'heroicon-o-user-group';
```

The retrieved docs also confirm a `Heroicon` enum example.

```php
use BackedEnum;
use Filament\Support\Icons\Heroicon;

protected static string | BackedEnum | null $navigationIcon = Heroicon::OutlinedDocumentText;
```

The retrieved docs confirm `$activeNavigationIcon` for an icon displayed only when the navigation item is active.

```php
use BackedEnum;
use Filament\Support\Icons\Heroicon;

protected static string | BackedEnum | null $activeNavigationIcon = Heroicon::OutlinedDocumentText;
```

## Groups, Parent Items, And Sort Order
The retrieved docs confirm `$navigationGroup` for grouping a navigation item.

```php
use UnitEnum;

protected static string | UnitEnum | null $navigationGroup = 'Shop';
```

The retrieved docs confirm `$navigationParentItem` for nesting the current Resource under a parent navigation item. If the parent is grouped, the current item should also define the same `$navigationGroup`.

```php
use UnitEnum;

protected static ?string $navigationParentItem = 'Products';

protected static string | UnitEnum | null $navigationGroup = 'Shop';
```

The retrieved docs confirm `$navigationSort` for controlling the navigation item position.

```php
protected static ?int $navigationSort = 2;
```

## Badges And Tooltips
When confirmed by the current lookup, use `getNavigationBadge()` for a navigation badge.

```php
public static function getNavigationBadge(): ?string
{
    return static::getModel()::count();
}
```

When confirmed by the current lookup, use `getNavigationBadgeColor()` for the navigation badge color.

```php
public static function getNavigationBadgeColor(): ?string
{
    return static::getModel()::count() > 10 ? 'warning' : 'primary';
}
```

Only use badge color strings confirmed by the lookup. Previously retrieved docs included `danger`, `gray`, `info`, `primary`, `success`, `warning`, and examples using `warning`, `primary`, and `danger`.

When confirmed by the current lookup, use `$navigationBadgeTooltip` or `getNavigationBadgeTooltip(): ?string` for badge tooltips.

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
When confirmed by the current lookup, use `$shouldRegisterNavigation = false` or `shouldRegisterNavigation(): bool` to prevent a Resource or Page item from appearing in navigation.

```php
protected static bool $shouldRegisterNavigation = false;
```

```php
public static function shouldRegisterNavigation(): bool
{
    return false;
}
```

The docs state that hiding a navigation item controls whether the item appears in navigation, not direct access.

## Record Sub-navigation
The retrieved docs confirm `getRecordSubNavigation()` for navigation items related to a particular Resource record.

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

## Not Confirmed In Current Lookup
Do not add implementation details for cluster classes, custom page title APIs, navigation badge polling or caching, authorization, or access control unless a narrower Context7 lookup returns them.