# Filament 5 Tables: Columns

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant column topic.

## Confirmed Column Types
The retrieved docs confirm built-in column types in the `Filament\Tables\Columns` namespace.

- Display columns: `TextColumn`, `IconColumn`, `ImageColumn`, `ColorColumn`.
- Editable columns: `SelectColumn`, `ToggleColumn`, `TextInputColumn`, `CheckboxColumn`.
- Custom columns are mentioned by the docs, but no implementation details were retrieved in the current lookup.

## Basic Text And Icon Columns

```php
use Filament\Tables\Columns\IconColumn;
use Filament\Tables\Columns\TextColumn;
use Filament\Tables\Table;

public function table(Table $table): Table
{
    return $table
        ->columns([
            TextColumn::make('title'),
            TextColumn::make('slug'),
            IconColumn::make('is_featured')
                ->boolean(),
        ]);
}
```

## Searchable And Sortable Columns

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('title')
    ->searchable()
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('title')
    ->sortable()
```

## Date, DateTime, And Time Formatting
The docs confirm `date()`, `dateTime()`, and `time()` on `TextColumn`. The column state must be a valid date or datetime.

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('created_at')
    ->date()
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('created_at')
    ->dateTime()
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('created_at')
    ->time()
```

## Money And State Formatting
The docs confirm `money()` and `formatStateUsing()` in custom data examples.

```php
use Filament\Tables\Columns\TextColumn;
use Illuminate\Support\Str;

TextColumn::make('category')
    ->formatStateUsing(fn (string $state): string => Str::headline($state))
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('price')
    ->money()
```

## Labels And State Callbacks
The docs confirm `label()` and `state()` in custom data examples.

```php
use Filament\Tables\Columns\TextColumn;
use Illuminate\Support\Str;

TextColumn::make('brand')
    ->state(fn (array $record): string => Str::title($record['brand'] ?? 'Unknown'))
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('sku')
    ->label('SKU')
```

## Image Column

```php
use Filament\Tables\Columns\ImageColumn;

ImageColumn::make('thumbnail')
    ->label('Image')
```

## Toggle Column

```php
use Filament\Tables\Columns\ToggleColumn;

ToggleColumn::make('is_admin')
```

## Horizontal Alignment
The docs confirm `alignStart()`, `alignCenter()`, `alignEnd()`, and `alignment(Alignment::End)`. `alignStart()` is the default.

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('email')
    ->alignStart()
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('email')
    ->alignCenter()
```

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('email')
    ->alignEnd()
```

```php
use Filament\Support\Enums\Alignment;
use Filament\Tables\Columns\TextColumn;

TextColumn::make('email')
    ->label('Email address')
    ->alignment(Alignment::End)
```

## Column Utility Injections
For Filament table columns, documented injectable context includes `$column`, `$livewire`, `$rowLoop`, `$state`, `$record`, and `$table`.

## Not Confirmed In Current Lookup
Do not add these without a narrower Context7 lookup that returns them: `badge()`, `limit()`, `tooltip()`, `copyable()`, `wrap()`, `html()`, `markdown()`, `color()`, `icon()`, `url()`, `description()`, `placeholder()`, `default()`, `toggleable()`, `hidden()`, `visible()`, summaries, or layout columns.