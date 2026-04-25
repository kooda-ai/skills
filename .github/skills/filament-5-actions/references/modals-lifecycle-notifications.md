# Filament 5 Actions: Modals, Lifecycle, And Notifications

Use this reference only after a Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant modal, lifecycle, cancellation, or notification action topic.

## Extra Modal Footer Actions
The retrieved docs confirm `extraModalFooterActions()` for adding custom buttons to an action modal footer. The method accepts an array of actions or a closure returning an array. The confirmed snippet uses `makeModalSubmitAction()` to create an extra submit action.

```php
use Filament\Actions\Action;

Action::make('create')
    ->schema([
        // ...
    ])
    ->extraModalFooterActions(fn (Action $action): array => [
        $action->makeModalSubmitAction('createAnother', arguments: ['another' => true]),
    ])
```

## Sticky Modal Footer
The retrieved docs confirm `stickyModalFooter()` for keeping an action modal footer visible while scrolling modal content.

```php
use Filament\Actions\Action;

Action::make('updateAuthor')
    ->schema([
        // ...
    ])
    ->action(function (array $data): void {
        // ...
    })
    ->stickyModalFooter()
```

## CreateAction Lifecycle Hooks
The retrieved docs confirm these `CreateAction` lifecycle hooks:

- `beforeFormFilled()`: runs before form fields are populated with their default values.
- `afterFormFilled()`: runs after form fields are populated with their default values.
- `beforeFormValidated()`: runs before form fields are validated when the form is submitted.
- `afterFormValidated()`: runs after form fields are validated when the form is submitted.
- `before()`: runs before form fields are saved to the database.
- `after()`: runs after form fields are saved to the database.

```php
use Filament\Actions\CreateAction;

CreateAction::make()
    ->beforeFormFilled(function () {
        // Runs before the form fields are populated with their default values.
    })
    ->afterFormFilled(function () {
        // Runs after the form fields are populated with their default values.
    })
    ->beforeFormValidated(function () {
        // Runs before the form fields are validated when the form is submitted.
    })
    ->afterFormValidated(function () {
        // Runs after the form fields are validated when the form is submitted.
    })
    ->before(function () {
        // Runs before the form fields are saved to the database.
    })
    ->after(function () {
        // Runs after the form fields are saved to the database.
    })
```

## Canceling An Action
The retrieved docs confirm `$action->cancel()` for halting a replication process and closing the action modal.

```php
$action->cancel();
```

## Notification Actions
The retrieved docs confirm that notifications can include actions rendered as buttons through `actions()`. The confirmed action examples use `button()` and `color()`.

```php
use Filament\Actions\Action;
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->actions([
        Action::make('view')
            ->button(),
        Action::make('undo')
            ->color('gray'),
    ])
    ->send();
```

## Not Confirmed In Current Lookup
Do not add implementation details for modal widths, slide overs, modal headings beyond the table action snippet, modal submit or cancel label customization, sticky headers, database transactions, `halt()`, lifecycle hooks on action classes other than the confirmed `CreateAction` hooks, or notification action URLs unless a narrower Context7 lookup returns them.