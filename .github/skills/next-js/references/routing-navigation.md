# Routing And Navigation

This reference captures the App Router routing, layouts and pages, linking and navigating, dynamic routes, redirects, rewrites, and proxy details bundled into this skill.

## App Router Structure
The current docs describe App Router routing as file-system based. A `page` file creates UI for a route, and a `layout` file shares UI across routes.

The docs show a required root layout for the `app` directory. Keep route examples aligned to documented file names such as `app/page.tsx`, `app/layout.tsx`, or the JavaScript equivalents when the current lookup uses them.

## Dynamic Routes
The docs cover dynamic segments with folder conventions such as `[slug]`, catch-all routes with `[...slug]`, and optional catch-all routes with `[[...slug]]`.

The current docs also show `params` as an async value in App Router examples. If the user asks for typed route params or route generation behavior, refresh the docs with a narrower query before adding detail.

## Route Groups And Parallel Routes
The docs cover route groups using folders like `(marketing)` that organize routes without affecting the URL path.

The docs cover parallel routes using named slots such as `@analytics`. When a slot can be unmatched on navigation, the docs also cover `default` files as fallbacks.

## Special Files
The current docs cover special files including:

- `loading` for route loading UI.
- `error` for route-level error boundaries.
- `not-found` for not-found UI.
- `default` for unmatched parallel-route fallbacks.

Use only the exact file names and behavior confirmed by the current lookup. If the task depends on nesting order or special-file precedence, refresh the docs for that exact topic.

## Proxy, Redirects, And Rewrites
The docs cover `proxy` as the request interception surface and show `NextRequest` and `NextResponse` in that area.

The docs also cover redirects and rewrites in `next.config.js`. The documented `rewrites()` and `redirects()` patterns should be used as-is, including documented `source`, `destination`, and `permanent` fields when they appear in the current lookup.

Do not add matcher rules, conditional logic, locale behavior, or ordering details unless the current lookup confirms them.

## Navigation APIs
The docs cover:

- `Link` for client-side navigation.
- `useRouter` for programmatic navigation.
- `usePathname` and `useSearchParams` for reading route state in client code.

If the user asks about prefetch behavior, selected layout segments, scroll behavior, or route interception details, refresh the docs for that exact API before answering.

## Topics Requiring Fresh Lookup
This reference does not lock in every detail for intercepting routes, locale routing, route segment config, pages router behavior, or advanced proxy matching. If those details are needed, explicitly say this skill does not confirm them.