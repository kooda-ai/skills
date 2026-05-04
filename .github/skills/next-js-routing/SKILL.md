---
name: next-js-routing
description: 'Use when: working with Next.js routing, App Router, file-system routing, app directory, page.tsx, layout.tsx, root layout, dynamic routes, catch-all routes, route groups, parallel routes, loading.tsx, error.tsx, not-found.tsx, default.tsx, proxy, redirects, rewrites, Link, useRouter, usePathname, useSearchParams, and Next.js route review. Uses bundled Next.js references and does not require external query templates.'
argument-hint: 'Next.js routing topic, route structure, special file, navigation API, or route review task'
---

# Next.js Routing

## Purpose
Use this skill to create, review, or explain Next.js routing and navigation code using only details confirmed in the bundled Next.js reference files in this skill.

## Source Rule
1. Use the bundled reference files below as the source of truth before giving code, commands, architecture guidance, or review findings.
2. Do not add route file conventions, segment syntax, special-file behavior, hook behavior, proxy behavior, redirect or rewrite behavior, or navigation APIs unless they appear in the reference files below.
3. If a requested detail is not confirmed by the reference files, explicitly say this skill does not confirm it.
4. Keep examples close to the documented snippets captured in the references and preserve documented file names, folder conventions, hook names, config keys, component names, and path syntax.
5. Do not infer behavior from older Next.js releases, Pages Router habits, React Router examples, blog posts, or general memory unless the reference files confirm it.

## Reference Map
- App Router routing, layouts, special files, redirects, rewrites, proxy, and navigation APIs: [routing-navigation.md](./references/routing-navigation.md)

## Workflow
1. Identify the routing surface: route structure, root layout, nested layout, dynamic segment, catch-all segment, route group, parallel route, loading UI, error boundary, not-found UI, proxy, redirect, rewrite, or navigation API.
2. Load the closest reference file from the map above.
3. Map the route structure using only documented file conventions such as `app`, `page`, `layout`, `loading`, `error`, `not-found`, `default`, and `proxy` when the reference files confirm them.
5. For parameterized routes, confirm the exact documented syntax such as `[slug]`, `[...slug]`, or `[[...slug]]` before using it.
6. For navigation code, confirm whether the task requires `Link`, `useRouter`, `usePathname`, or `useSearchParams`, and keep those APIs restricted to the behavior confirmed by the reference files.
7. For redirects, rewrites, and proxy behavior, verify the exact documented surface such as `next.config.js` or `proxy` before describing matching or request handling behavior.
8. Finish by checking that every file path, folder convention, hook, config key, and routing claim is traceable to the reference files.

## Confirmed Core Patterns
- The docs describe App Router routing as file-system based.
- The docs show `page` files for routes and `layout` files for shared UI, including a required root layout.
- The docs cover dynamic segments, catch-all routes, optional catch-all routes, route groups, parallel routes, and special files including `loading`, `error`, `not-found`, and `default`.
- The docs cover `proxy`, redirects, rewrites, `Link`, `useRouter`, `usePathname`, and `useSearchParams`.

## Completion Check
- Every route file convention, hook, config key, segment syntax, and redirect or rewrite statement is traceable to the reference files.
- Unconfirmed routing topics are omitted or explicitly called out as not confirmed by this skill's bundled Next.js references.