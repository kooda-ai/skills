---
name: laravel-13-search
description: 'Use when: working with Laravel 13 search, full-text search, fullText indexes, whereFullText(), orWhereFullText(), database-specific relevance ordering, semantic search, vector search, PostgreSQL pgvector, Schema::ensureVectorExtensionExists(), vector columns, whereVectorSimilarTo(), selectVectorDistance(), whereVectorDistanceLessThan(), orderByVectorDistance(), Laravel AI SDK embedding boundaries, and Laravel 13 search code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 full-text search, semantic/vector search, pgvector, embedding boundary, or review task'
---

# Laravel 13 Search

## Purpose
Use this skill to create, review, or explain Laravel 13 full-text search and semantic/vector search code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact search topic.
2. Do not add search methods, schema methods, column methods, index methods, database support claims, relevance behavior, vector distance APIs, embedding behavior, Scout behavior, AI SDK APIs, imports, or examples unless they appear in the current Context7 result or the reference files below.
3. If the task requires concrete embedding generation APIs, resolve and query the Laravel AI SDK docs and use the `laravel-ai-sdk` skill rather than inventing SDK method names from framework search docs.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented method names, database names, parameter names, table names, column names, and example values.
6. Do not infer behavior from older Laravel versions, database vendor docs, pgvector docs, Scout docs, AI provider docs, package source code, blog posts, or general Laravel memory.

## Reference Map
- Full-text indexes, `fullText(...)`, PostgreSQL language selection, `whereFullText(...)`, `orWhereFullText(...)`, supported databases, and relevance-ordering boundaries: [full-text-search.md](./references/full-text-search.md)
- Vector extension setup, vector columns, `whereVectorSimilarTo(...)`, automatic embedding boundary, manual distance methods, and pgvector requirements: [semantic-vector-search.md](./references/semantic-vector-search.md)
- Search boundaries for Laravel AI SDK, Scout, database-specific behavior, and unconfirmed features: [search-boundaries.md](./references/search-boundaries.md)

## Workflow
1. Identify the exact surface: full-text index, full-text query, composite full-text query, PostgreSQL full-text language, full-text relevance ordering, vector extension setup, vector column migration, semantic search query, vector similarity filtering, vector distance selection, AI SDK embedding boundary, or code review.
2. Query Context7 for that exact Laravel 13 search topic.
3. Load the relevant reference file from the map above.
4. Use only documented schema methods, query builder methods, database support claims, parameter names, search behavior, and examples.
5. For full-text search topics not in the references, such as dropping full-text indexes, custom generated SQL, database-specific full-text modes, Scout database engine setup, external search engines, ranking formulas, or search result highlighting, rely on the fresh Context7 lookup.
6. For semantic/vector search topics not in the references, such as embedding generation calls, AI provider configuration, vector dimensions beyond the shown example, vector migration options beyond `index()`, pgvector installation outside Laravel, `whereVectorDistanceGreaterThan`, exact distance metrics, or Scout integration, rely on the fresh Context7 lookup and package-specific docs where needed.
7. For reviews, flag only documented mismatches: missing documented full-text index, unsupported database claim, wrong relevance-ordering assumption, unconfirmed schema method, unconfirmed vector query method, unconfirmed AI SDK API, unsupported pgvector behavior, or package behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel 13 search docs cover database-native full-text search and semantic/vector search.
- `whereFullText(...)` searches columns configured with full-text indexes.
- Full-text search is documented as supported by MariaDB, MySQL, and PostgreSQL.
- `whereFullText(...)` automatically generates database-specific SQL for the underlying database.
- `Article::whereFullText('body', 'web developer')->get()` is documented.
- `Article::whereFullText(['title', 'body'], 'web developer')->get()` is documented for searching across a composite full-text index.
- `DB::table('users')->whereFullText('bio', 'web developer')->get()` is documented.
- `orWhereFullText(...)` is documented as an `or` condition for full-text search clauses.
- Full-text results are automatically ordered by relevance on MySQL and MariaDB, but not on PostgreSQL according to the search docs.
- The docs show `$table->fullText(['title', 'body'])` for creating a full-text index.
- The docs show `$table->fullText('body')->language('english')` for PostgreSQL stemming language selection.
- Semantic/vector search uses AI-generated vector embeddings to match meaning rather than exact keyword overlap.
- Laravel 13 release notes state semantic/vector search is native in Laravel 13 and supports PostgreSQL with `pgvector`.
- The search docs state semantic/vector search requires PostgreSQL with the `pgvector` extension and the Laravel AI SDK.
- The docs show `Schema::ensureVectorExtensionExists()` before creating a vector-backed table.
- The docs show `$table->vector('embedding', dimensions: 1536)->index()` for storing embeddings.
- `whereVectorSimilarTo('embedding', $queryEmbedding, minSimilarity: 0.4)` is documented.
- Passing a plain string such as `'Best wineries in Napa Valley'` to `whereVectorSimilarTo(...)` is documented, with automatic embedding generation through the Laravel AI SDK according to the query builder docs.
- `whereVectorSimilarTo(..., order: false)` is documented for disabling automatic distance ordering so custom sorting can be applied.
- The docs show `selectVectorDistance(...)`, `whereVectorDistanceLessThan(...)`, and `orderByVectorDistance(...)` for more granular vector distance queries.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 search topic.
- Every schema method, query builder method, database support claim, search behavior, vector method, parameter name, and AI SDK boundary statement is traceable to the lookup or references.
- Database vendor, pgvector, Scout, and AI SDK details are not inferred when the Laravel 13 docs did not confirm them.
