# Content Surfaces And API Flows

## Notifications
- Wave notifications are built on Laravel notifications with a Wave UI.
- The docs show `php artisan make:notification TestNotification`, `via()` returning `['database']`, and `toArray()` returning keys such as `icon`, `body`, `link`, and `user`.
- Notifications are viewed at `/notifications`.
- Unread count is documented as `auth()->user()->unreadNotifications->count()`.

## Changelog, Blog, And Pages
- Changelog entries are managed at `/admin/changelog`.
- The docs say changelog popups appear across the application until clicked or dismissed.
- The blog is documented at `/blog`.
- The blog list view is documented at `resources/themes/{theme_folder}/blog/index.blade.php`.
- The blog post view is documented at `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php`.
- Posts are managed at `/admin/posts`, and only posts with status `PUBLISHED` appear on the front end.
- Categories are managed at `/admin/categories`.
- Admin-created pages are managed at `/admin/pages` and become routes based on slug.
- The docs distinguish admin-created content pages from theme `pages` files used for custom layouts or logic.

## API
- API keys are created at `/settings/api`.
- Documented token endpoints include `/api/token?key=API_KEY_HERE`, `/api/login?...`, `/api/refresh`, and `/api/register?...`.
- The built-in API is documented as a stateless JWT API.
- The docs say Sanctum may be used alongside the current JWT implementation.
- The docs suggest Insomnia and the documented `wave-3-api-endpoints.json` export for API testing.
