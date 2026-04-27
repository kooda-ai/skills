# Full-Text Search

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x search, query builder full-text clauses, and full-text index migrations.

## Full-Text Indexes
The docs show creating a full-text index in a migration:

```php
Schema::create('articles', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('body');
    $table->timestamps();

    $table->fullText(['title', 'body']);
});
```

The docs show PostgreSQL language selection for stemming:

```php
$table->fullText('body')->language('english');
```

Confirmed methods: `fullText(...)` and `language('english')`.

## Full-Text Queries
The docs show using `whereFullText(...)` with Eloquent:

```php
$articles = Article::whereFullText('body', 'web developer')->get();
```

The docs show searching across a composite full-text index by passing an array of column names:

```php
$articles = Article::whereFullText(
    ['title', 'body'], 'web developer'
)->get();
```

The query builder docs show the `DB` facade form:

```php
$users = DB::table('users')
    ->whereFullText('bio', 'web developer')
    ->get();
```

## Confirmed Behavior
The docs state `whereFullText(...)` searches columns that have full-text indexes.

The docs state `whereFullText(...)` is supported by MariaDB, MySQL, and PostgreSQL.

The docs state Laravel automatically transforms `whereFullText(...)` into the appropriate database-specific SQL syntax, such as `MATCH(...) AGAINST(...)` for MariaDB and MySQL or `to_tsvector(...) @@ plainto_tsquery(...)` for PostgreSQL.

The docs state full-text search can understand word boundaries and stemming, including matching related terms such as `running` to `run`.

The docs state results are automatically sorted by relevance on MariaDB and MySQL, but on PostgreSQL `whereFullText(...)` only filters results.

The docs state `orWhereFullText(...)` can incorporate full-text search clauses as `or` conditions.

## Topics Requiring Fresh Lookup
