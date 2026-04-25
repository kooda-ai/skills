---
name: filament-5-advanced-enum-tricks
description: 'Use when: working with Filament 5 Advanced enum tricks, PHP enums, HasLabel, HasColor, HasIcon, enum-backed Select, CheckboxList, Radio, SelectColumn, SelectFilter, TextColumn enum labels, table groupings, infolist TextEntry enum labels, enum colors, enum icons, badges, ToggleButtons, and Heroicon enum icon mappings. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Enum task, Status enum, form/table/filter/infolist enum UI, label/color/icon mapping, or code to review'
---

# Filament 5 Advanced Enum Tricks

## Purpose
Use this skill to create, review, or explain Filament 5 enum integrations using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Advanced enum topic.
2. Do not add enum behavior, interfaces, return types, components, methods, namespaces, casting behavior, icon names, color names, or examples unless they appear in the retrieved documentation.
3. If the current Context7 lookup does not confirm a requested enum topic, run a narrower Context7 lookup or say that the current documentation context did not confirm it.
4. Keep examples close to documented snippets and preserve documented method names, class names, namespaces, return types, component names, and enum case names.
5. Do not infer behavior from Filament 4.x, older examples, Laravel conventions, PHP enum habits, package source code, or memory.

## Workflow
1. Identify the enum surface: enum labels, enum colors, enum icons, form field options, table column options, table filter options, table display, table grouping, infolist display, badge display, or ToggleButtons icons/colors.
2. Run a narrow Context7 query for the exact enum surface before producing code.
3. Use `Filament\Support\Contracts\HasLabel` only when the docs confirm label behavior for the requested component.
4. Use `Filament\Support\Contracts\HasColor` only when the docs confirm color behavior for the requested component.
5. Use `Filament\Support\Contracts\HasIcon` only when the docs confirm icon behavior for the requested component.
6. For enum-backed options, pass the enum class directly to `options()` only for documented components confirmed by the lookup.
7. For table or infolist display behavior, include Eloquent enum casting only when the current lookup confirms that the underlying model attribute must be cast to an enum.
8. For colors and icons, rely on the enum methods instead of duplicating per-component mappings when the docs confirm automatic usage for that component.
9. Finish by checking that every interface, method, component, namespace, return type, icon value, color value, and display claim appears in the current Context7 result.

## Confirmed Core Patterns
- `HasLabel` is implemented on an enum to provide human-readable labels for enum cases.
- `getLabel()` returns `string | Htmlable | null`.
- `getLabel()` can return `$this->name` or a `match ($this)` expression with per-case labels.
- `HasColor` is implemented on an enum to provide colors for enum cases.
- `getColor()` returns `string | array | null`.
- Documented color examples include `gray`, `warning`, `success`, and `danger`.
- `HasIcon` is implemented on an enum to provide icons for enum cases.
- `getIcon()` returns `string | BackedEnum | Htmlable | null`.
- The documented icon example returns `Heroicon::Pencil`, `Heroicon::Eye`, `Heroicon::Check`, and `Heroicon::XMark`.
- A form `Select`, `CheckboxList`, or `Radio` can pass an enum class that implements `HasLabel` to `options()`.
- A table `SelectColumn` or `SelectFilter` can pass an enum class that implements `HasLabel` to `options()`.
- Filament automatically generates key-value pairs for enum-backed options using the enum value and label.
- Filament automatically uses `HasLabel` for `TextColumn`, table groupings, and infolist `TextEntry` when the underlying Eloquent model attribute is cast to an enum.
- Filament automatically applies `HasColor` to `TextColumn`, infolist `TextEntry`, and `ToggleButtons` when an enum is used.
- For columns and entries, documented color behavior is most effective with badge display.
- Filament can use `HasIcon` with components such as `TextColumn` or `ToggleButtons` to display icons automatically.

## Documented Snippets

### Enum labels
```php
use Filament\Support\Contracts\HasLabel;
use Illuminate\Contracts\Support\Htmlable;

enum Status: string implements HasLabel
{
    case Draft = 'draft';
    case Reviewing = 'reviewing';
    case Published = 'published';
    case Rejected = 'rejected';
    
    public function getLabel(): string | Htmlable | null
    {
        return match ($this) {
            self::Draft => 'Draft',
            self::Reviewing => 'Reviewing',
            self::Published => 'Published',
            self::Rejected => 'Rejected',
        };
    }
}
```

### Enum colors
```php
use Filament\Support\Contracts\HasColor;

enum Status: string implements HasColor
{
    case Draft = 'draft';
    case Reviewing = 'reviewing';
    case Published = 'published';
    case Rejected = 'rejected';
    
    public function getColor(): string | array | null
    {
        return match ($this) {
            self::Draft => 'gray',
            self::Reviewing => 'warning',
            self::Published => 'success',
            self::Rejected => 'danger',
        };
    }
}
```

### Enum icons
```php
use BackedEnum;
use Filament\Support\Contracts\HasIcon;
use Filament\Support\Icons\Heroicon;
use Illuminate\Contracts\Support\Htmlable;

enum Status: string implements HasIcon
{
    case Draft = 'draft';
    case Reviewing = 'reviewing';
    case Published = 'published';
    case Rejected = 'rejected';

    public function getIcon(): string | BackedEnum | Htmlable | null
    {
        return match ($this) {
            self::Draft => Heroicon::Pencil,
            self::Reviewing => Heroicon::Eye,
            self::Published => Heroicon::Check,
            self::Rejected => Heroicon::XMark,
        };
    }
}
```

### Form field options
```php
use Filament\Forms\Components\CheckboxList;
use Filament\Forms\Components\Radio;
use Filament\Forms\Components\Select;

Select::make('status')
    ->options(Status::class)

CheckboxList::make('status')
    ->options(Status::class)

Radio::make('status')
    ->options(Status::class)
```

### Table options
```php
use Filament\Tables\Columns\SelectColumn;
use Filament\Tables\Filters\SelectFilter;

SelectColumn::make('status')
    ->options(Status::class)

SelectFilter::make('status')
    ->options(Status::class)
```

## Completion Check
- The answer uses only enum APIs and component behavior confirmed by the current Context7 lookup.
- Each class, interface, method, namespace, return type, color, icon, and component claim is traceable to the retrieved Filament 5.x docs.
- Enum-backed `options()` are limited to documented components confirmed by the lookup.
- Automatic label, color, and icon behavior is described only for documented components confirmed by the lookup.
- Eloquent enum casting is mentioned only where the Context7 result confirms it.
- Code examples keep documented namespaces, method names, return types, component names, enum case names, colors, and Heroicon names intact.