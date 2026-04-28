---
name: wave-content-api
description: 'Use when: working with Wave notifications, changelog, blog, pages, content management routes, API keys, JWT access tokens, register/login token endpoints, Insomnia testing of the Wave API, and Wave content or API features from the docs. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave notifications, changelog, blog, pages, API, or content-management task'
---

# Wave Content And API

## Purpose
Use this skill for the content and API features documented by Wave: notifications, changelog, blog, pages, API keys, JWT token flows, and API testing.

## Source Rule
1. Before giving final content or API guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add notification structure, content routes, page view paths, API endpoints, token flows, or testing guidance unless it appears in the current Wave docs.
3. If the task needs deeper Laravel notifications or API framework behavior, say that clearly and only extend after querying the relevant docs.
4. Keep examples close to documented paths, endpoints, and code snippets.

## Reference Map
- Notifications, changelog, blog, pages, API keys, and JWT token flows: [content-surfaces-and-api-flows.md](./references/content-surfaces-and-api-flows.md)

## Related Wave Skills
- Use `wave-notifications-content` when the task is specifically about notifications, changelog, blog, content pages, or content-management routes without the API layer.
- Use `wave-access-control-admin` when content or API access depends on roles, permissions, subscriber checks, or admin-managed gating.
- Use `wave-customization-theming` when the task is about changing how blog, page, changelog, or notification views look inside a theme.
- Use `wave-auth-users` when API or notification questions are really about user identity, registration, or profile-linked behavior.

## Workflow
1. Identify whether the task is notifications, changelog, blog, pages, API keys, tokens, registration/login via API, or API testing.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Hand off to `wave-notifications-content` when the request is about notifications, changelog, blog, or content pages rather than API behavior.
5. Use only the documented Wave routes, endpoints, and content admin flows.
6. Preserve the documented distinction between admin-managed content pages and theme page files.
7. Omit anything not confirmed by the current Wave docs.

## Confirmed Core Patterns
- Wave notifications are built on Laravel notifications with a Wave UI on top.
- The docs show `php artisan make:notification TestNotification`, changing `via()` to `['database']`, and returning `icon`, `body`, `link`, and `user` data from `toArray()`.
- Notifications are viewed at `/notifications`.
- The unread notification count is documented as `auth()->user()->unreadNotifications->count()`.
- Changelog entries are managed at `/admin/changelog`.
- The docs say changelog popups appear across the application until clicked or dismissed.
- The blog is documented at `/blog`.
- The blog list view is documented at `resources/themes/{theme_folder}/blog/index.blade.php`.
- The blog post view is documented at `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php`.
- Posts are managed at `/admin/posts`, and only posts with status `PUBLISHED` appear on the front end.
- Categories are managed at `/admin/categories`.
- Admin-created pages are managed at `/admin/pages` and become routes such as `/hello-world` based on slug.
- The docs say admin-created pages fit simple content pages, while theme `pages` files fit custom layouts, custom logic, or additional styling.
- API keys are created at `/settings/api`.
- The docs show token endpoints at `/api/token?key=API_KEY_HERE`, `/api/login?email=admin@admin.com&password=password`, `/api/refresh`, and `/api/register?name=John Doe&username=jdoe&email=jdoe@gmail.com&password=pass`.
- The built-in Wave API is documented as a stateless JWT API.
- The docs say Sanctum may be used alongside the current JWT implementation.
- The docs suggest Insomnia and the documented `wave-3-api-endpoints.json` export for API testing.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact content or API topic.
- Every route, endpoint, file path, token flow, and content-management statement is traceable to the current Wave docs.
- Deeper Laravel notification or API framework behavior is not inferred beyond what the Wave docs confirm.
