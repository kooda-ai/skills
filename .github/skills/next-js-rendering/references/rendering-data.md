# Rendering, Data, And Metadata

This reference captures the Server and Client Components, fetching data, caching, Route Handlers, Server Actions, Suspense, and metadata details bundled into this skill.

## Server And Client Components
The current docs describe Server Components as the default App Router component model. The docs describe Client Components as requiring the `'use client'` directive.

Use Client Components only when the current task needs client-side interactivity, browser APIs, state, effects, or event handlers confirmed by the docs.

## Data Fetching
The docs show data fetching directly in async Server Components. They also show streaming data by passing a promise into a Client Component and resolving it with Suspense.

Keep data-fetching examples close to documented `fetch()` or server-side function patterns. If the user asks for a specific ORM or external client pattern, refresh the docs for the exact example that confirms it.

## Caching And Revalidation
The current docs cover cache-related APIs and directives including:

- `'use cache'`
- `cacheLife`
- `cacheTag`
- `revalidatePath`
- `revalidateTag`
- `updateTag`

Use only the exact API names, cache profiles, and invalidation behavior confirmed by the current lookup. If the task depends on default caching behavior for a specific surface, refresh the docs for that exact surface first.

The current docs also confirm that `updateTag` can only be called from Server Actions. If cache invalidation is needed in another context, refresh the docs for the exact alternative before answering.

## Streaming And Suspense
The docs cover streaming UI with Suspense and route-level loading UI. The docs also cover Partial Prerendering in the current Next.js documentation.

The current docs show a documented pattern where a Server Component passes a promise to a Client Component and the Client Component reads it with React's `use` API inside a Suspense boundary.

If the user asks how runtime data, cached content, and static shell behavior interact beyond what is written here, explicitly say this skill does not confirm the missing detail.

## Route Handlers
The docs cover Route Handlers with `route.ts` or `route.js` file conventions and request-handling APIs in the app directory.

Keep handler examples aligned with documented HTTP method exports and documented request or response objects from the current lookup. Do not add unsupported handler caching claims without a fresh lookup for that exact scenario.

## Server Actions
The docs cover Server Actions through the `'use server'` directive. They also show action usage with forms and cache revalidation after mutations.

If the user asks about action invocation from client code, validation flow, auth boundaries, or pending UI helpers, refresh the docs for that exact action pattern before adding detail.

## Metadata
The current docs cover:

- Static metadata exports.
- `generateMetadata()`.
- Metadata in Server Components.

If the user asks about Open Graph images, file-based metadata, or bot-specific behavior, refresh the docs for that exact metadata surface before answering.

## Topics Requiring Fresh Lookup
This reference does not freeze every detail for React cache utilities, bot handling, advanced streaming tradeoffs, or surface-specific caching defaults. If those details matter, explicitly say this skill does not confirm them.