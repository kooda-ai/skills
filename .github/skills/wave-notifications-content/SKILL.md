---
name: wave-notifications-content
description: 'Use when: working with Wave notifications, changelog, blog, pages, content-management routes, admin content CRUD surfaces, and the documented distinction between admin-managed content pages and theme page files. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave notifications, changelog, blog, pages, or content-management task'
---

# Wave Notifications And Content

## Purpose
Use this skill for Wave notifications, changelog, blog, content pages, and the documented content-management surfaces exposed by the admin and theme layers.

## Source Rule
1. Before giving final notification or content guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add notification structure, changelog behavior, blog paths, page-management routes, or content view paths unless they appear in the current Wave docs.
3. If the task needs deeper Laravel notifications or broader Blade/theme behavior, say that the Wave docs defer to those products.
4. Keep examples close to documented routes, file paths, and admin flows.

## Reference Map
- Notifications, changelog, blog, content pages, and admin content surfaces: [notifications-changelog-blog-pages.md](./references/notifications-changelog-blog-pages.md)

## Related Wave Skills
- Use `wave-content-api` when the task moves into API keys, JWT token flows, register/login token endpoints, or API testing.
- Use `wave-customization-theming` when the task is about changing how blog, changelog, page, or notification views look inside a theme.
- Use `wave-access-control-admin` when content visibility or management depends on roles, permissions, subscriber checks, or admin gating.
- Use `wave-volt-pages` when the question is really about theme page files and custom routed pages rather than admin-managed content.

## Workflow
1. Identify whether the task is notifications, changelog, blog, content pages, or choosing between admin-managed pages and theme page files.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only the documented Wave routes, file paths, and admin content flows.
5. Preserve the documented distinction between admin-managed content pages and theme page files.
6. Omit anything not confirmed by the current Wave docs.

## Confirmed Core Patterns
- Wave notifications are built on Laravel notifications with a Wave UI on top.
- Notifications are viewed at `/notifications`.
- The docs show a `database` notification flow and a `toArray()` payload with keys such as `icon`, `body`, `link`, and `user`.
- Changelog entries are managed at `/admin/changelog`.
- The docs say changelog popups appear across the application until clicked or dismissed.
- The blog is documented at `/blog`.
- The blog list view is documented at `resources/themes/{theme_folder}/blog/index.blade.php`.
- The blog post view is documented at `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php`.
- Posts are managed at `/admin/posts`, and only posts with status `PUBLISHED` appear on the front end.
- Categories are managed at `/admin/categories`.
- Admin-created pages are managed at `/admin/pages` and become routes based on slug.
- The docs say admin-created pages fit simple content pages, while theme `pages` files fit custom layouts, custom logic, or additional styling.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact content topic.
- Every route, file path, admin surface, and behavior statement is traceable to the current Wave docs.
- Deeper Laravel notifications or theme behavior is not inferred beyond what the Wave docs confirm.
