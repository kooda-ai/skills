# Testing Tables And Schemas

## Source Boundary
Use this reference only after a fresh Context7 query for `/websites/filamentphp_5_x` confirms the requested Filament 5.x Testing topic.

## Table Records And Filters
The retrieved docs confirm these table testing helpers:
- `assertCanSeeTableRecords($records)`
- `assertCanNotSeeTableRecords($records)`
- `filterTable($filterName, $value)`

Use them for documented table filtering scenarios only when the lookup confirms the same helper names and argument pattern.

## Table Column Existence
The retrieved Tables testing docs confirm `assertTableColumnExists()`:

```php
use function Pest\Livewire\livewire;

it('has an author column', function () {
    livewire(PostResource\Pages\ListPosts::class)
        ->assertTableColumnExists('author');
});
```

The docs also confirm an optional truth test callback and record argument:

```php
use Filament\Tables\Columns\TextColumn;
use function Pest\Livewire\livewire;

it('has an author column', function () {
    $post = Post::factory()->create();

    livewire(PostResource\Pages\ListPosts::class)
        ->assertTableColumnExists('author', function (TextColumn $column): bool {
            return $column->getDescriptionBelow() === $post->subtitle;
        }, $post);
});
```

## Schema And Form State
The retrieved Schemas testing docs confirm using `fillForm()` to populate form fields in Livewire component tests:

```php
use function Pest\Livewire\livewire;

livewire(CreatePost::class)
    ->fillForm([
        'title' => fake()->sentence(),
        // ...
    ]);
```

The docs state that a form schema name can be specified if multiple forms exist on the component. Do not invent the exact argument order unless the current Context7 result shows it.

The docs confirm `assertSchemaStateSet()` with a callback that can inspect state and return an array for continued assertion:

```php
use Illuminate\Support\Str;
use function Pest\Livewire\livewire;

it('can automatically generate a slug from the title without any spaces', function () {
    $title = fake()->sentence();

    livewire(CreatePost::class)
        ->fillForm([
            'title' => $title,
        ])
        ->assertSchemaStateSet(function (array $state): array {
            expect($state['slug'])
                ->not->toContain(' ');

            return [
                'slug' => Str::slug($title),
            ];
        });
});
```

## Use Carefully
- Use `assertTableColumnExists()` only for documented table column existence checks and callback checks.
- Use `fillForm()` and `assertSchemaStateSet()` only for documented schema or form state tests.
- Do not add undocumented table helpers such as sorting, searching, pagination, selectable records, summaries, or bulk selection unless the current Context7 result confirms them.
- Do not add undocumented schema helpers, validation helpers, multiple-form signatures, or state path behavior unless the current Context7 result confirms them.