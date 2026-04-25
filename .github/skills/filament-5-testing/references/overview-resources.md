# Testing Overview And Resources

## Source Boundary
Use this reference only after a fresh Context7 query for `/websites/filamentphp_5_x` confirms the requested Filament 5.x Testing topic.

## Testing Basis
- Filament testing utilities leverage Livewire testing helpers because all Filament components are mounted to a Livewire component.
- The docs use Pest examples with `use function Pest\Livewire\livewire;`.
- The docs state that tests can be adapted for PHPUnit by replacing Pest's `livewire()` function with Livewire's `Livewire::test()` method.
- The retrieved testing overview confirms guides for panel Resources, Tables, Schemas, Actions, and sent Notifications.

## Resource Page And Form Patterns
The retrieved Resource testing examples confirm mounting Resource pages with Livewire and passing a record ID to an edit page:

```php
use App\Filament\Resources\Users\Pages\EditUser;
use App\Models\User;
use Illuminate\Support\Str;
use function Pest\Livewire\livewire;

it('validates the form data', function (array $data, array $errors) {
    $user = User::factory()->create();

    $newUserData = User::factory()->make();

    livewire(EditUser::class, [
        'record' => $user->id,
    ])
        ->fillForm([
            'name' => $newUserData->name,
            'email' => $newUserData->email,
            ...$data,
        ])
        ->call('save')
        ->assertHasFormErrors($errors)
        ->assertNotNotified();
})->with([
    '`name` is required' => [['name' => null], ['name' => 'required']],
    '`name` is max 255 characters' => [['name' => Str::random(256)], ['name' => 'max']],
    '`email` is a valid email address' => [['email' => Str::random()], ['email' => 'email']],
    '`email` is required' => [['email' => null], ['email' => 'required']],
    '`email` is max 255 characters' => [['email' => Str::random(256)], ['email' => 'max']],
]);
```

## Resource Table Filtering Pattern
The retrieved Resource testing docs confirm applying a table filter and asserting the visible and hidden records:

```php
use App\Filament\Resources\Users\Pages\ListUsers;
use App\Models\User;
use function Pest\Livewire\livewire;

it('can filter users by `locale`', function () {
    $users = User::factory()->count(5)->create();

    livewire(ListUsers::class)
        ->assertCanSeeTableRecords($users)
        ->filterTable('locale', $users->first()->locale)
        ->assertCanSeeTableRecords($users->where('locale', $users->first()->locale))
        ->assertCanNotSeeTableRecords($users->where('locale', '!=', $users->first()->locale));
});
```

## Use Carefully
- Use `fillForm()`, `call('save')`, `assertHasFormErrors()`, `assertNotNotified()`, `assertCanSeeTableRecords()`, `filterTable()`, and `assertCanNotSeeTableRecords()` only when the current Context7 result confirms them for the task.
- Do not add create-page, view-page, delete, route, policy, database, or authentication test helpers unless a fresh Context7 result returns those details.