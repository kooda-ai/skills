# Eager Loading And Querying

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x eager loading and relationship querying.

## Eager Loading With `with()`
The docs show eager loading a relationship with `with(...)` to reduce query count:

```php
$books = Book::with('author')->get();

foreach ($books as $book) {
    echo $book->author->name;
}
```

Confirmed methods and dynamic property: `with('author')`, `get()`, and `$book->author`.

## Constrained Eager Loading
The docs show passing a closure to `with(...)` to constrain eager loading:

```php
use App\Models\User;

$users = User::with(['posts' => function ($query) {
    $query->where('title', 'like', '%code%');
}])->get();
```

The docs also show ordering in the eager loading query:

```php
$users = User::with(['posts' => function ($query) {
    $query->orderBy('created_at', 'desc');
}])->get();
```

Confirmed methods: `with(...)`, `where(...)`, `orderBy(...)`, and `get()`.

## Collection `load()`
The docs show eager loading relationships for all models in an Eloquent collection with `load(...)`:

```php
$users->load(['comments', 'posts']);

$users->load('comments.author');

$users->load(['comments', 'posts' => fn ($query) => $query->where('active', 1)]);
```

The docs state `load` supports single relationships, multiple relationships, nested relationships, and query constraints.

## Lazy Eager Loading
The docs show loading relationships after parent models have already been retrieved:

```php
use App\Models\Book;

$books = Book::all();

if ($condition) {
    $books->load('author', 'publisher');
}
```

The docs show constrained lazy eager loading:

```php
$author->load(['books' => function ($query) {
    $query->orderBy('published_date', 'asc');
}]);
```

The docs show `loadMissing(...)`:

```php
$book->loadMissing('author');
```

Confirmed methods: `all()`, `load(...)`, `orderBy(...)`, and `loadMissing(...)`.

## Relationship Existence With Eager Loading
The docs show `withWhereHas(...)` to filter parent models based on relationship existence while eager loading those relationships:

```php
use App\Models\User;

$users = User::withWhereHas('posts', function ($query) {
    $query->where('featured', true);
})->get();
```

Confirmed methods: `withWhereHas(...)`, `where(...)`, and `get()`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `has`, `whereHas`, `orWhereHas`, `doesntHave`, `whereDoesntHave`, nested relationship existence queries, `withCount`, aggregate eager loading, default eager loading on models, preventing lazy loading, morph eager loading beyond `loadMorph`, or relationship query-builder operations beyond shown examples.
