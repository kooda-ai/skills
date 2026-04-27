# Pagination

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x pagination.

## Paginator Methods
The docs show paginating Eloquent results:

```php
use App\Models\User;

$users = User::paginate(15);
```

The docs show simple pagination for query builder results:

```php
$users = DB::table('users')->simplePaginate(15);
```

The docs state `simplePaginate(...)` is more efficient when only Next and Previous links are needed because it avoids counting total records.

The docs show query builder cursor pagination:

```php
$users = DB::table('users')->orderBy('id')->cursorPaginate(15);
```

The docs state cursor pagination requires an `orderBy` clause on the query builder.

The docs show Eloquent cursor pagination:

```php
$users = User::where('votes', '>', 100)->cursorPaginate(15);
```

## Pagination URL Customization
The docs show appending specific query string parameters to pagination links:

```php
use App\Models\User;

Route::get('/users', function () {
    $users = User::paginate(15);

    $users->appends(['sort' => 'votes']);

    // ...
});
```

The docs show appending all current request query string values:

```php
$users = User::paginate(15)->withQueryString();
```

The docs show customizing the URI used by the paginator:

```php
use App\Models\User;

Route::get('/users', function () {
    $users = User::paginate(15);

    $users->withPath('/admin/users');

    // ...
});
```

The docs show appending a hash fragment:

```php
$users = User::paginate(15)->fragment('users');
```

The docs show retrieving a URL for a specific page:

```php
$paginator->url($page)
```

The docs show retrieving the page query-string parameter name:

```php
$paginator->getPageName()
```

The docs state the default page query-string parameter is `page`.

## Pagination Views
The docs show rendering links with a custom view and passing additional data:

```blade
{{ $paginator->links('view.name') }}

<!-- Passing additional data to the view... -->
{{ $paginator->links('view.name', ['foo' => 'bar']) }}
```

The docs show publishing pagination views:

```shell
php artisan vendor:publish --tag=laravel-pagination
```

The docs state the views are published to `resources/views/vendor/pagination`.

The docs show using Bootstrap pagination views from `App\Providers\AppServiceProvider`:

```php
use Illuminate\Pagination\Paginator;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Paginator::useBootstrapFive();
    Paginator::useBootstrapFour();
}
```

The docs show adjusting the pagination link window:

```blade
{{ $users->onEachSide(5)->links() }}
```

## JSON And Manual Paginators
The docs show returning a paginator directly from a route:

```php
use App\Models\User;

Route::get('/users', function () {
    return User::paginate();
});
```

The docs state returning a paginator instance from a route or controller automatically serializes pagination metadata and data to JSON, including keys like `total`, `current_page`, `last_page`, and `data`.

The docs state manual paginator instances can be created with `Illuminate\Pagination\Paginator`, `Illuminate\Pagination\LengthAwarePaginator`, or `Illuminate\Pagination\CursorPaginator`.

The docs state `Paginator` and `CursorPaginator` do not need the total number of items and do not have methods for retrieving the index of the last page.

The docs state `LengthAwarePaginator` requires a count of the total number of items in the result set.

The docs map `Paginator` to `simplePaginate`, `CursorPaginator` to `cursorPaginate`, and `LengthAwarePaginator` to `paginate`.

The docs state arrays passed to manual paginator instances should be manually sliced.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using multiple paginator page names, pagination default view configuration beyond the Bootstrap snippets, custom page resolvers, cursor pagination limitations beyond the returned `orderBy` statement, API resource pagination details, paginator instance constructor signatures, or pagination behavior in Livewire/Inertia/frontend packages.
