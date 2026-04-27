---
name: laravel-13-api-resources-serialization
description: 'Use when: working with Laravel 13 Eloquent API resources, JSON resources, JsonResource, ResourceCollection, resource responses, toResource(), Resource::collection(), toResourceCollection(), JSON:API resources, JsonApiResource, make:resource --json-api, resource attributes, resource relationships, sparse fieldsets, includes, Content-Type application/vnd.api+json, Eloquent serialization, toArray(), toJson(), hidden attributes, visible attributes, appends, accessors, casts, model JSON route responses, and Laravel 13 API resource/serialization code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 API resources, JSON:API resources, Eloquent serialization, or review task'
---

# Laravel 13 API Resources And Serialization

## Purpose
Use this skill to create, review, or explain Laravel 13 Eloquent API resources, JSON:API resources, resource collections, and Eloquent serialization using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact API resource, JSON:API resource, resource collection, or Eloquent serialization topic.
2. Do not add resource generator flags, resource class imports, response wrapping behavior, collection behavior, JSON:API behavior, serialization methods, visibility APIs, accessor/appended attribute behavior, cast formats, route response behavior, headers, links, meta, relationships, includes, sparse fieldsets, or examples unless they appear in the current Context7 result or the reference files below.
3. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, methods, class names, paths, properties, headers, and payload concepts.
5. Do not infer behavior from older Laravel versions, JSON:API specification docs, package docs, blog posts, source code, or general Laravel memory.

## Reference Map
- Returning resources from routes, `toResource()`, resource collections, `toResourceCollection()`, custom `ResourceCollection`, and metadata boundary: [resources-collections.md](./references/resources-collections.md)
- First-party JSON:API resources, `make:resource --json-api`, `JsonApiResource`, `$attributes`, `$relationships`, sparse fieldsets, includes, and content type: [json-api-resources.md](./references/json-api-resources.md)
- Eloquent `toJson()`, automatic route serialization, visibility methods, appended accessor attributes, and custom date serialization casts: [eloquent-serialization.md](./references/eloquent-serialization.md)

## Workflow
1. Identify the exact surface: single resource response, model `toResource()`, resource collection, custom resource collection, metadata, JSON:API resource generation, JSON:API attributes, JSON:API relationships, sparse fieldsets, includes, content type, model JSON serialization, visibility, appended accessors, date serialization, or code review.
2. Query Context7 for that exact Laravel 13 topic.
3. Load the relevant reference file from the map above.
4. Use only documented commands, methods, classes, properties, response helpers, serialization methods, visibility APIs, cast formats, headers, and examples.
5. For resource topics not in the references, such as standard `make:resource` without `--json-api`, exact `JsonResource` imports, conditional attributes, conditional relationships, data wrapping configuration, pagination response details, `additional()`, `with()`, or exact `links` / `meta` array shapes, rely on the fresh Context7 lookup.
6. For JSON:API topics not in the references, such as concrete relationship syntax, link generation APIs, sparse fieldset request syntax, include request syntax, compliant response examples, resource identifiers, errors, or pagination, rely on the fresh Context7 lookup.
7. For serialization topics not in the references, such as `$hidden`, `$visible`, runtime `append()`, `setAppends()`, relationship hiding, date serialization methods, custom casts beyond the returned date format, or array serialization beyond methods shown here, rely on the fresh Context7 lookup.
8. For reviews, flag only documented mismatches: unconfirmed generator flag, unconfirmed import, unsupported serialization method, unconfirmed visibility API, wrong resource collection behavior, unsupported JSON:API behavior, unconfirmed header, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- The docs show returning a resource from a route with `return new PostResource($post);`.
- The docs show returning a model resource with `$post->toResource()`.
- The docs show `PostResource::collection(Post::all())` for returning multiple resources.
- The docs show `Post::all()->toResourceCollection()` for returning a resource collection from a model collection.
- The docs show `UserResource::collection(User::all())` in a route.
- Custom resource collection classes can extend `Illuminate\Http\Resources\Json\ResourceCollection`.
- The docs show a custom `CommentsCollection` returning `['data' => $this->collection]` from `toArray(Request $request): array`.
- Laravel prevents double-wrapping even when resource collections are nested according to the returned docs.
- Metadata such as `links` or other resource-specific information can be added within `toArray()` according to the docs.
- The docs state any `links` defined by the resource are merged with links automatically provided by Laravel for paginated responses.
- `php artisan make:resource PostResource --json-api` is documented for generating a JSON:API resource.
- The generated JSON:API resource class extends `Illuminate\Http\Resources\JsonApi\JsonApiResource`.
- JSON:API resource classes can define `$attributes` and `$relationships` properties.
- The docs state `JsonApiResource` extends the standard `JsonResource`.
- The docs state `JsonApiResource` automatically manages resource object structure, relationships, sparse fieldsets, and includes.
- The docs state JSON:API resources set the `Content-Type` header to `application/vnd.api+json`.
- Laravel 13 release notes describe first-party JSON:API resources for compliant responses and mention object serialization, relationship inclusion, sparse fieldsets, link generation, and compliant response headers.
- `toJson()` is documented for converting a model to JSON.
- `toJson(JSON_PRETTY_PRINT)` is documented for passing JSON encoding options.
- Casting an Eloquent model or collection to a string automatically calls `toJson()` according to the docs.
- Laravel automatically serializes Eloquent models and collections to JSON when they are returned from routes or controllers according to the docs.
- The docs state `toJson()` is recursive like `toArray()`, so attributes and relations are converted to JSON.
- Runtime visibility methods documented in the returned docs include `makeVisible()`, `mergeVisible()`, `makeHidden()`, `mergeHidden()`, `setVisible()`, and `setHidden()`.
- The docs show appending a custom accessor attribute using `#[Appends(['is_admin'])]` with an accessor returning an `Illuminate\Database\Eloquent\Casts\Attribute`.
- The docs show a custom date cast format with `'created_at' => 'datetime:Y-m-d'` for serialization to array or JSON.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 API resource, JSON:API resource, resource collection, or serialization topic.
- Every command, method, class, property, header, helper, route response behavior, serialization behavior, visibility API, cast format, and JSON:API statement is traceable to the lookup or references.
- JSON:API specification behavior, resource response structure, pagination metadata, and serialization details are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed API resource or serialization features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
