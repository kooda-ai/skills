# Filament 5 Infolists: Entries And TextEntry

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Infolists entry topic.

## Defining Entries
The retrieved docs define infolist entries as components used to display data within a schema array.

The docs mention these built-in entry categories:

- text entries
- icon entries
- image entries
- color entries
- code entries
- key-value entries
- repeatable entries
- custom entries

Only add concrete class names or methods for these entry categories when the current Context7 lookup confirms them. In the retrieved results, `Filament\Infolists\Components\TextEntry` is the concrete entry class with method examples.

## TextEntry In Schema
The retrieved schema docs show `TextEntry` inside a schema layout.

```php
use Filament\Infolists\Components\TextEntry;
use Filament\Schemas\Components\Section;

Section::make('Auditing')
    ->schema([
        TextEntry::make('created_at')
            ->dateTime(),
        TextEntry::make('updated_at')
            ->dateTime(),
    ])
```

## Badge With Dynamic Color
The retrieved docs show `badge()` and a dynamic `color()` callback based on the entry state.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('status')
    ->badge()
    ->color(fn (string $state): string => match ($state) {
        'draft' => 'gray',
        'reviewing' => 'warning',
        'published' => 'success',
        'rejected' => 'danger',
    })
```

## Format State Callback
The retrieved docs show `formatStateUsing()` to transform displayed state without altering the underlying data.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('status')
    ->formatStateUsing(fn (string $state): string => __("statuses.{$state}"))
```

## Word Limit
The retrieved docs show `words()` to limit displayed words. The docs state that an ellipsis is appended by default when words are truncated.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('description')
    ->words(10)
```

## Numeric Formatting
The retrieved docs show `numeric()` formatting the entry state as a number using the default application locale.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('stock')
    ->numeric()
```

## Entry Utility Injection
The retrieved docs list these parameters as available for injection within Filament infolist entries:

- `$component`: the current `Filament\Infolists\Components\Entry` instance.
- `$get`: a `Filament\Schemas\Components\Utilities\Get` function for retrieving values from the current schema data. Validation is not run on form fields.
- `$model`: the Eloquent model FQN for the current schema, nullable.
- `$livewire`: the `Livewire\Component` instance.
- `$state`: the current value of the entry.
- `$operation`: the current operation, usually `create`, `edit`, or `view`.
- `$record`: the Eloquent record for the current schema, nullable.

## Not Confirmed In Current Lookup
Do not add methods for icons, images, colors, code blocks, key-value entries, repeatable entries, markdown, HTML, money, list separators, character limits, placeholders, defaults, copyable behavior, timezone behavior, or custom entries unless a narrower Context7 lookup returns them.
