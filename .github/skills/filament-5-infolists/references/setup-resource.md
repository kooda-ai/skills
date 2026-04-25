# Filament 5 Infolists: Setup And Resource Usage

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Infolists setup topic.

## Package Purpose
The retrieved docs describe Filament's Infolists package as a way to display a read-only list of data for a specific entity. The package is integrated into other Filament packages, including panel resources, relation managers, and action modals. The docs also state that understanding the infolist builder can help when developing custom Livewire applications or working with other Filament features.

## Resource Infolist Schema Delegation
The retrieved docs show a Resource `infolist()` method delegating to a reusable customer infolist schema class.

```php
use App\Filament\Resources\Customers\Schemas\CustomerInfolist;
use Filament\Schemas\Schema;

public static function infolist(Schema $schema): Schema
{
    return CustomerInfolist::configure($schema);
}
```

## Reusable Infolist Schema Boundary
The Resource example confirms the `CustomerInfolist::configure($schema)` delegation pattern. Use a reusable infolist schema class only when a current Context7 lookup confirms the class structure needed for the task.

The related schema documentation confirms reusable schema classes using a `configure(Schema $schema): Schema` method and `$schema->components([...])`. Keep reusable infolist examples close to that confirmed schema pattern and include only infolist entries and layout components confirmed by the current lookup.

```php
use Filament\Schemas\Schema;

class CustomerInfolist
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->components([
                // ...
            ]);
    }
}
```

## Schema Type And Components
The retrieved Resource infolist example imports `Filament\Schemas\Schema`. The retrieved schema examples show `$schema->components([...])` containing `Filament\Infolists\Components\TextEntry` entries and schema layout components.

```php
use Filament\Infolists\Components\TextEntry;
use Filament\Schemas\Components\Section;

$schema
    ->components([
        Section::make('Auditing')
            ->schema([
                TextEntry::make('created_at')
                    ->dateTime(),
                TextEntry::make('updated_at')
                    ->dateTime(),
            ]),
    ]);
```

## Livewire Boundary
The retrieved Infolists overview says the infolist builder is relevant to custom Livewire applications, but the current lookup did not return a complete custom Livewire infolist implementation. Do not add Blade rendering, named schema access, model binding, or Livewire infolist lifecycle details unless a narrower Context7 lookup confirms them.

The broader schema docs confirm `HasSchemas` and `InteractsWithSchemas` for Livewire schema functionality, but the returned full example is for a form schema. Do not present that form-specific example as an infolist implementation unless the current lookup confirms the infolist-specific details.

## Not Confirmed In Current Lookup
Do not add CLI commands, generated file paths, ViewRecord page behavior, relation manager infolist code, action modal infolist code, model binding behavior, custom Livewire infolist rendering, or custom entry implementation details unless a narrower Context7 lookup returns them.
