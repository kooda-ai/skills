---
name: next-js-rendering
description: 'Use when: working with Next.js rendering, App Router rendering, Server Components, Client Components, use client, use server, data fetching, caching, revalidation, use cache, cacheLife, cacheTag, revalidatePath, revalidateTag, updateTag, Route Handlers, Server Actions, streaming, Suspense, Partial Prerendering, metadata, generateMetadata, and Next.js rendering review. Uses bundled Next.js references and does not require external query templates.'
argument-hint: 'Next.js rendering topic, server or client boundary, cache API, Route Handler, Server Action, or metadata task'
---

# Next.js Rendering

## Purpose
Use this skill to create, review, or explain Next.js rendering and data-flow code using only details confirmed in the bundled Next.js reference files in this skill.

## Source Rule
1. Use the bundled reference files below as the source of truth before giving code, commands, architecture guidance, or review findings.
2. Do not add rendering behavior, cache behavior, metadata behavior, Route Handler behavior, Server Action behavior, or client and server boundary rules unless they appear in the reference files below.
3. If a requested detail is not confirmed by the reference files, explicitly say this skill does not confirm it.
4. Keep examples close to the documented snippets captured in the references and preserve documented directives, function names, hook names, file conventions, request or response APIs, and cache API names.
5. Do not infer behavior from older Next.js releases, general React server-rendering patterns, community blog posts, or memory unless the reference files confirm it.

## Reference Map
- Server and Client Components, data fetching, caching, revalidation, Route Handlers, Server Actions, streaming, and metadata: [rendering-data.md](./references/rendering-data.md)

## Workflow
1. Identify the rendering surface: Server Component, Client Component, client or server directive, data fetching, cache control, revalidation, Route Handler, Server Action, streaming, Suspense, Partial Prerendering, static metadata, or `generateMetadata()`.
2. Load the closest reference file from the map above.
3. Confirm the client or server boundary first, using only documented signals such as `'use client'`, `'use server'`, Server Components, Client Components, Route Handlers, or metadata exports.
5. For data fetching and caching, confirm the exact documented API such as `'use cache'`, `cacheLife`, `cacheTag`, `revalidatePath`, `revalidateTag`, or `updateTag` before using it.
6. For mutations, confirm whether the task belongs in a Server Action or a Route Handler and keep the behavior restricted to what the reference files confirm.
7. For streaming and Suspense, use only the rendering flow and boundaries confirmed by the reference files.
8. Finish by checking that every directive, function, file convention, cache API, Route Handler claim, Server Action claim, and metadata statement is traceable to the reference files.

## Confirmed Core Patterns
- The docs describe Server Components as the default App Router component model and Client Components as requiring the `'use client'` directive.
- The docs cover data fetching in async Server Components and streaming with Suspense.
- The docs cover cache and revalidation APIs including `'use cache'`, `cacheLife`, `cacheTag`, `revalidatePath`, `revalidateTag`, and `updateTag`.
- The docs cover Route Handlers, Server Actions, Partial Prerendering, static metadata exports, and `generateMetadata()`.

## Completion Check
- Every directive, cache API, Route Handler statement, Server Action statement, metadata statement, and rendering behavior claim is traceable to the reference files.
- Unconfirmed rendering topics are omitted or explicitly called out as not confirmed by this skill's bundled Next.js references.