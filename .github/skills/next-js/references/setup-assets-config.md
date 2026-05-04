# Setup, Assets, And Configuration

This reference captures the `create-next-app`, styling, `next/image`, `next/font`, `next/script`, environment variables, and `next.config` details bundled into this skill.

## Project Setup
The docs show `create-next-app` as the documented project bootstrap entry point, including commands for common package managers.

Use the exact documented command variant from the current lookup, such as `npx create-next-app@latest`, when the user asks for setup instructions. If the task depends on a specific prompt flow or package manager, refresh the docs for that exact setup path.

## TypeScript And Styling Setup
The current docs cover TypeScript-capable setup flows and documented styling approaches including global CSS, CSS Modules, and Tailwind CSS integration.

Keep styling guidance limited to the approach confirmed by the current lookup. If the current lookup uses `app/globals.css`, `.module.css`, or a specific Tailwind setup sequence, preserve that exact sequence.

## Image Optimization
The docs cover `next/image` for optimized images.

The current docs also cover remote image configuration and documented image options. If the task depends on remote patterns, placeholders, or caching configuration, refresh the docs for the exact `next/image` topic before answering.

## Font Loading
The docs cover `next/font/google` and `next/font/local`.

The current docs also show CSS variable-based usage patterns for fonts. Preserve the documented import paths, configuration fields, and placement when giving code examples.

## Script Loading
The docs cover `next/script` and documented loading strategies.

If the task depends on a specific strategy such as `beforeInteractive`, `afterInteractive`, `lazyOnload`, or `worker`, refresh the docs for that exact strategy before giving implementation guidance.

## Environment Variables
The docs cover environment variables through `.env` files and the `NEXT_PUBLIC_` prefix for browser-exposed values.

Do not add variable-loading order, test-environment behavior, or external loading details unless the current lookup confirms them for the exact scenario.

## next.config
The docs cover `next.config` configuration and documented options such as redirects and rewrites.

Keep config examples restricted to keys that appear in the current lookup. If the user asks about image config, output config, bundler settings, or experimental flags, refresh the docs for that exact key before answering.

## Topics Requiring Fresh Lookup
This reference does not freeze every Tailwind version detail, image prop matrix, script callback, environment-variable load order rule, or config option. If those specifics matter, explicitly say this skill does not confirm them.