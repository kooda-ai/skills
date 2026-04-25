# Filament 5 Resources: Setup

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Resources setup topic.

## Create A Resource
The retrieved docs confirm `make:filament-resource` for generating a new Resource for an Eloquent model.

```bash
php artisan make:filament-resource Customer
```

The docs state that this creates the basic structure for managing the model's data.

## Generated Structure
The retrieved docs state that creating a Resource generates several files, including:

- The main Resource class.
- Pages for interaction: Create, Edit, and List.
- Schemas for forms and infolists.
- Tables for data display.

Do not invent exact generated file paths, class names, namespaces, or method signatures unless the current Context7 lookup returns them.

## Resource Form Method
The retrieved docs confirm that Resource classes use a `form()` method to construct forms for record creation and editing. The documented Resource example delegates to a dedicated schema class.

```php
use App\Filament\Resources\Customers\Schemas\CustomerForm;
use Filament\Schemas\Schema;

public static function form(Schema $schema): Schema
{
	return CustomerForm::configure($schema);
}
```

The docs state that Filament separates form schemas into dedicated files by default for better organization.

## Resource Infolist Method
The retrieved docs confirm that a Resource `infolist()` method can delegate to a dedicated infolist schema class.

```php
use App\Filament\Resources\Customers\Schemas\CustomerInfolist;
use Filament\Schemas\Schema;

public static function infolist(Schema $schema): Schema
{
	return CustomerInfolist::configure($schema);
}
```

## Resource Table Method
The retrieved docs confirm that Resource classes contain a `table()` method used to build the table on the List page. The documented Resource example delegates to a dedicated table configuration class.

```php
use App\Filament\Resources\Customers\Tables\CustomersTable;
use Filament\Tables\Table;

public static function table(Table $table): Table
{
	return CustomersTable::configure($table);
}
```

The docs state that Filament creates a table file by default and references it in the `table()` method to keep the Resource class clean and organized.

## Simple Resource
The retrieved docs confirm `--simple` for generating a simple Resource that manages records using modals on a single page.

```bash
php artisan make:filament-resource Customer --simple
```

The docs describe this as suitable for less complex models.

## Resource URL
The retrieved docs confirm the static `getUrl()` method on a Resource class for generating a URL to the Resource List page.

```php
use App\Filament\Resources\Customers\CustomerResource;

CustomerResource::getUrl(); // /admin/customers
```

The documented example uses no arguments for the default List page.

## Custom Slug
The retrieved docs confirm the protected static `$slug` property for defining a custom Resource URL slug.

```php
protected static ?string $slug = 'pending-orders';
```

The docs state that this overrides Filament's default naming convention.

## Resource Schema And Table Details
The retrieved Resources docs state that generated Resources include schemas for forms and infolists and tables for data display. For implementation details of schemas and tables, load the relevant Filament 5 Schemas or Filament 5 Tables skill and run a fresh Context7 lookup for the exact topic.

## Not Confirmed In Current Lookup
Do not add implementation details for Resource `$model`, `extends Resource`, full Resource namespaces, generated page file paths, generated schema class names beyond the documented examples above, generated table class names beyond the documented examples above, or command flags other than `--simple` unless a narrower Context7 lookup returns them.