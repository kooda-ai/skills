# Semantic And Vector Search

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x search, release notes, vector columns, and query builder vector similarity clauses.

## Concept And Requirements
Laravel 13 release notes state the framework introduces native support for semantic and vector search for AI-powered search experiences.

The docs describe semantic search as matching by meaning rather than exact keyword overlap by using AI-generated vector embeddings.

The docs state semantic/vector search requires PostgreSQL with the `pgvector` extension and the Laravel AI SDK.

## Vector Column Setup
The docs show ensuring the vector extension exists and creating a vector column:

```php
Schema::ensureVectorExtensionExists();

Schema::create('documents', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->vector('embedding', dimensions: 1536)->index();
    $table->timestamps();
});
```

Confirmed methods: `Schema::ensureVectorExtensionExists()`, `$table->vector(...)`, and `index()` on the vector column example.

## Similarity Queries
The docs show filtering and ordering by vector similarity:

```php
$documents = DB::table('documents')
    ->whereVectorSimilarTo('embedding', $queryEmbedding, minSimilarity: 0.4)
    ->limit(10)
    ->get();
```

The docs show passing a string so Laravel can generate embeddings using the Laravel AI SDK:

```php
$documents = DB::table('documents')
    ->whereVectorSimilarTo('embedding', 'Best wineries in Napa Valley')
    ->limit(10)
    ->get();
```

The docs show disabling automatic distance ordering and applying custom ordering:

```php
$documents = DB::table('documents')
    ->whereVectorSimilarTo('embedding', $queryEmbedding, minSimilarity: 0.4, order: false)
    ->orderBy('created_at', 'desc')
    ->limit(10)
    ->get();
```

## Manual Distance Queries
The docs show selecting, filtering, and ordering by vector distance:

```php
$documents = DB::table('documents')
    ->select('*')
    ->selectVectorDistance('embedding', $queryEmbedding, as: 'distance')
    ->whereVectorDistanceLessThan('embedding', $queryEmbedding, maxDistance: 0.3)
    ->orderByVectorDistance('embedding', $queryEmbedding)
    ->limit(10)
    ->get();
```

Confirmed methods: `whereVectorSimilarTo(...)`, `selectVectorDistance(...)`, `whereVectorDistanceLessThan(...)`, and `orderByVectorDistance(...)`.

## Confirmed Parameters And Behavior
The query builder docs list `whereVectorSimilarTo` parameters: `column`, `vector`, optional `minSimilarity`, and optional `order`.

The docs state `minSimilarity` is a threshold between `0.0` and `1.0`.

The docs state `whereVectorSimilarTo(...)` filters results based on cosine similarity and orders by relevance by default.

The docs state that if a plain string is provided instead of a vector, Laravel can automatically generate embeddings using the Laravel AI SDK.

The docs state `order: false` disables automatic ordering by distance.

## Topics Requiring Fresh Lookup
