# Search Boundaries

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x search, query builder search clauses, and release notes.

## Laravel Framework Search Scope
This slice covers the Laravel 13 framework search APIs confirmed by the docs:

- Full-text indexes with `fullText(...)`.
- Full-text queries with `whereFullText(...)` and `orWhereFullText(...)`.
- Semantic/vector search with PostgreSQL `pgvector`.
- Vector columns with `vector(...)`.
- Vector query builder methods returned by the docs.

## Laravel AI SDK Boundary
The Laravel 13 search docs state semantic/vector search requires the Laravel AI SDK and that Laravel can automatically generate embeddings when a plain string is passed to `whereVectorSimilarTo(...)`.

The framework search docs returned for this slice did not provide concrete Laravel AI SDK configuration or embedding-generation calls. For those details, resolve and query the Laravel AI SDK documentation and use the `laravel-ai-sdk` skill.

## Scout Boundary
The full-text search docs mention that PostgreSQL `whereFullText(...)` only filters results and says to consider Scout's database engine for relevance-based ordering.

Do not add Scout installation, configuration, engine behavior, external driver details, model traits, indexing commands, or search syntax unless a fresh Context7 lookup confirms those details from the appropriate docs.

## Database Vendor Boundary
The Laravel docs returned for this slice confirm MariaDB, MySQL, and PostgreSQL support for full-text search, and PostgreSQL with `pgvector` for semantic/vector search.

Do not add database-specific setup, generated SQL beyond the returned examples, ranking formulas, pgvector extension installation steps outside Laravel's `Schema::ensureVectorExtensionExists()`, or unsupported database behavior unless a fresh Context7 lookup confirms it.

## Review Checklist
When reviewing search code, check only documented issues:

- `whereFullText(...)` used without a documented full-text index.
- PostgreSQL code assuming automatic relevance ordering from `whereFullText(...)`.
- Vector search code that does not account for the documented PostgreSQL `pgvector` requirement.
- Concrete AI SDK method names added from framework docs that did not include them.
- Vector distance methods, parameters, or schema methods not confirmed by the current lookup.
