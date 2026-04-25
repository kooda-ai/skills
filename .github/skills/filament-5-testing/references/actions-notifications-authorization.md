# Testing Actions, Notifications, And Authorization Context

## Source Boundary
Use this reference only after a fresh Context7 query for `/websites/filamentphp_5_x` confirms the requested Filament 5.x Testing topic.

## Actions
The retrieved Actions testing docs confirm `callAction()` for triggering an action in a Pest Livewire test:

```php
use function Pest\Livewire\livewire;

it('can send invoices', function () {
    $invoice = Invoice::factory()->create();

    livewire(EditInvoice::class, [
        'invoice' => $invoice,
    ])
        ->callAction('send');

    expect($invoice->refresh())
        ->isSent()->toBeTrue();
});
```

## Table Actions With TestAction
The retrieved docs confirm `Filament\Actions\Testing\TestAction` for targeting table actions:

```php
use Filament\Actions\Testing\TestAction;
use function Pest\Livewire\livewire;

$invoice = Invoice::factory()->create();

livewire(ListInvoices::class)
    ->callAction(TestAction::make('send')->table($invoice));

livewire(ListInvoices::class)
    ->assertActionVisible(TestAction::make('send')->table($invoice));

livewire(ListInvoices::class)
    ->assertActionExists(TestAction::make('send')->table($invoice));
```

## Notifications
The retrieved Resource validation example confirms `assertNotNotified()` after failed validation. The retrieved Testing and Resource examples also confirm `assertNotified()` as a notification assertion helper. Use these helpers only when the current Context7 result confirms the notification scenario.

## Authorization Context
The retrieved Actions docs confirm the `authorize()` method for linking actions to policy methods:

```php
use Filament\Actions\Action;

Action::make('edit')
    ->url(fn (): string => route('posts.edit', ['post' => $this->post]))
    ->authorize('update')
```

The same retrieved result states that Filament automatically handles policies for built-in actions in panel Resources.

## Use Carefully
- Use `callAction()`, `TestAction::make()`, `table()`, `assertActionVisible()`, and `assertActionExists()` only when the current lookup confirms them.
- Do not add undocumented action helpers such as mounting, form filling, disabled/hidden assertions, halted actions, modal assertions, or action validation assertions unless the current Context7 result confirms them.
- Do not add notification payload matching, database notification assertions, or broadcast notification assertions unless the current Context7 result confirms them.
- Do not create authorization test scaffolding, policy method lists, role setup, or permission package examples from memory. Only use `authorize()` and built-in panel Resource policy handling when confirmed by the current lookup.