# Complex and Editor Components

Use this reference only after a fresh Context7 lookup confirms the requested Repeater, Builder, editor, or boolean field topic.

## RichEditor
The retrieved docs confirm basic `RichEditor` initialization.

```php
use Filament\Forms\Components\RichEditor;

RichEditor::make('content');
```

The retrieved docs describe it as used for editing and previewing HTML content with image uploads. Do not add toolbar, file storage, or sanitization details unless a fresh lookup confirms them.

## MarkdownEditor
The retrieved docs confirm basic `MarkdownEditor` initialization.

```php
use Filament\Forms\Components\MarkdownEditor;

MarkdownEditor::make('content');
```

## Toggle and Checkbox
The retrieved docs confirm basic `Toggle` and `Checkbox` initialization.

```php
use Filament\Forms\Components\Toggle;

Toggle::make('is_admin');
```

```php
use Filament\Forms\Components\Checkbox;

Checkbox::make('is_admin');
```

## Repeater Item Labels
The retrieved docs confirm `Repeater`, nested `schema([...])`, `columns(2)`, and dynamic `itemLabel()`. Fields referenced from `$state` should be `live()` for live updates.

```php
use Filament\Forms\Components\Repeater;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\TextInput;

Repeater::make('members')
    ->schema([
        TextInput::make('name')
            ->required()
            ->live(onBlur: true),
        Select::make('role')
            ->options([
                'member' => 'Member',
                'administrator' => 'Administrator',
                'owner' => 'Owner',
            ])
            ->required(),
    ])
    ->columns(2)
    ->itemLabel(fn (array $state): ?string => $state['name'] ?? null);
```

## Repeater Relationship
The retrieved docs confirm `relationship()` for linking a `Repeater` field to a `HasMany` Eloquent relationship. The docs state that Filament handles loading and saving data directly to the relationship.

```php
use Filament\Forms\Components\Repeater;

Repeater::make('qualifications')
    ->relationship()
    ->schema([
        // ...
    ]);
```

Do not add relationship ordering, pivot data, mutation hooks, or model-saving details unless a fresh lookup confirms them.

## Builder Blocks and Extra Item Actions
The retrieved docs confirm `Builder`, `Builder\Block`, `blocks([...])`, `extraItemActions([...])`, and `getItemState($arguments['item'])` inside an action.

```php
use Filament\Actions\Action;
use Filament\Forms\Components\Builder;
use Filament\Forms\Components\Builder\Block;
use Filament\Forms\Components\TextInput;
use Filament\Support\Icons\Heroicon;
use Illuminate\Support\Facades\Mail;

Builder::make('content')
    ->blocks([
        Block::make('contactDetails')
            ->schema([
                TextInput::make('email')
                    ->label('Email address')
                    ->email()
                    ->required(),
            ]),
    ])
    ->extraItemActions([
        Action::make('sendEmail')
            ->icon(Heroicon::Square2Stack)
            ->action(function (array $arguments, Builder $component): void {
                $itemData = $component->getItemState($arguments['item']);

                Mail::to($itemData['email'])
                    ->send(
                        // ...
                    );
            }),
    ]);
```

## Builder Item Controls
The retrieved docs confirm disabling Builder drag-and-drop reordering with `reorderable(false)` and disabling deletion with `deletable(false)`. Both methods support dynamic control via a function according to the retrieved docs.

```php
use Filament\Forms\Components\Builder;

Builder::make('content')
    ->blocks([
        // ...
    ])
    ->reorderable(false);
```

```php
use Filament\Forms\Components\Builder;

Builder::make('content')
    ->blocks([
        // ...
    ])
    ->deletable(false);
```