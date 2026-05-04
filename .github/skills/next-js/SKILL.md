---
name: next-js
description: 'Use when: working with Next.js, App Router, file-system routing, page.tsx, layout.tsx, loading.tsx, error.tsx, not-found.tsx, dynamic routes, route groups, parallel routes, proxy, middleware, redirects, rewrites, Link, useRouter, usePathname, useSearchParams, Server Components, Client Components, data fetching, caching, revalidation, Route Handlers, Server Actions, streaming, Suspense, metadata, create-next-app, TypeScript, Tailwind CSS, CSS Modules, global CSS, next/image, next/font, next/script, environment variables, next.config, Docker, static export, deployment, and Next.js upgrades. Uses bundled Next.js references and does not require external query templates.'
argument-hint: 'Next.js topic, exact API/file/convention to create, explain, or review'
---

# Next.js

## Purpose
Use this skill to create, review, or explain Next.js code using only details confirmed in the bundled Next.js reference files in this skill.

## Source Rule
1. Use the bundled reference files below as the source of truth before giving code, commands, architecture guidance, or review findings.
2. Do not add file conventions, commands, config keys, rendering behavior, cache behavior, deployment guidance, upgrade steps, or component APIs unless they appear in the reference files below.
3. If a requested detail is not confirmed by the reference files, explicitly say this skill does not confirm it.
4. Keep examples close to the documented snippets captured in the references and preserve documented file names, directives, config keys, component names, hook names, command flags, and path conventions.
5. Do not infer behavior from older Next.js releases, React-only examples, blog posts, repository code, or general memory unless the reference files confirm it.

## Reference Map
- App Router routing, layouts, special files, redirects, rewrites, proxy, and navigation APIs: [routing-navigation.md](./references/routing-navigation.md)
- Server and Client Components, data fetching, caching, revalidation, Route Handlers, Server Actions, streaming, and metadata: [rendering-data.md](./references/rendering-data.md)
- Project setup, styling, image/font/script components, environment variables, and `next.config`: [setup-assets-config.md](./references/setup-assets-config.md)
- Build, deployment, static export, and upgrade boundaries: [deployment-upgrades.md](./references/deployment-upgrades.md)

## Related Split Skills
- Use `next-js-routing` for routing-only work such as App Router conventions, `page.tsx`, `layout.tsx`, root layout, dynamic segments, catch-all routes, route groups, parallel routes, `loading.tsx`, `error.tsx`, `not-found.tsx`, `default.tsx`, proxy, redirects, rewrites, `Link`, `useRouter`, `usePathname`, and `useSearchParams`.
- Use `next-js-rendering` for rendering and data-flow work such as Server Components, Client Components, `'use client'`, `'use server'`, data fetching, caching, revalidation, `'use cache'`, `cacheLife`, `cacheTag`, `revalidatePath`, `revalidateTag`, `updateTag`, Route Handlers, Server Actions, streaming, Suspense, Partial Prerendering, metadata, and `generateMetadata()`.

## Workflow
1. Identify the Next.js surface: routing, layouts, navigation, rendering, data fetching, caching, Route Handlers, Server Actions, metadata, setup, styling, image optimization, font loading, script loading, environment variables, configuration, build, deployment, or upgrading.
2. Load the closest reference file from the map above.
3. For broad requests that cross multiple surfaces, split the work into focused subtopics such as routing/navigation, rendering/data, and setup/configuration, then handle each slice separately before synthesizing the final answer.
4. Use only documented file conventions such as `app`, `page`, `layout`, `loading`, `error`, `not-found`, `route`, `proxy`, `next.config`, and documented component or function exports when the reference files confirm them.
5. For client and server boundaries, confirm whether the task requires `'use client'`, `'use server'`, Server Components, Client Components, Route Handlers, or metadata exports.
6. For cache or revalidation guidance, confirm the exact documented API such as `'use cache'`, `cacheLife`, `cacheTag`, `revalidatePath`, `revalidateTag`, or `updateTag` before using it.
7. For setup or deployment guidance, verify the exact command, config key, file name, or platform note in the reference files instead of generalizing from prior Next.js versions.
8. Finish by checking that every command, file path, directive, hook, config key, and behavioral claim is traceable to the reference files.

## Confirmed Core Patterns
- The docs describe Next.js as using file-system based routing with the App Router.
- The docs show `page` files for routes and `layout` files for shared UI structure, including a required root layout.
- The docs cover dynamic segments, route groups, parallel routes, loading UI, error boundaries, not-found handling, redirects, rewrites, and proxy behavior.
- The docs cover Server Components, Client Components, data fetching in Server Components, streaming with Suspense, Route Handlers, Server Actions, caching and revalidation APIs, and metadata exports.
- The docs cover `create-next-app`, TypeScript-capable setup flows, CSS styling approaches, `next/image`, `next/font`, `next/script`, environment variables, `next.config`, deployment guidance, static export, and version upgrade guides.

## Completion Check
- Every file convention, command, hook, directive, config key, component API, cache API, and deployment or upgrade statement is traceable to the reference files.
- Unconfirmed topics are omitted or explicitly called out as not confirmed by this skill's bundled Next.js references.