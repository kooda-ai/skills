# Notifications, Changelog, Blog, And Pages

## Notifications
- Wave notifications are built on Laravel notifications with a Wave UI on top.
- The docs show `php artisan make:notification TestNotification`, changing `via()` to `['database']`, and returning `icon`, `body`, `link`, and `user` data from `toArray()`.
- Notifications are viewed at `/notifications`.
- Unread notification count is documented as `auth()->user()->unreadNotifications->count()`.

## Changelog
- Changelog entries are managed at `/admin/changelog`.
- The docs say changelog popups appear across the application until clicked or dismissed.

## Blog
- The blog is documented at `/blog`.
- The blog list view is documented at `resources/themes/{theme_folder}/blog/index.blade.php`.
- The blog post view is documented at `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php`.
- Posts are managed at `/admin/posts`, and only posts with status `PUBLISHED` appear on the front end.
- Categories are managed at `/admin/categories`.

## Pages
- Admin-created pages are managed at `/admin/pages` and become routes based on slug.
- The docs say admin-created pages fit simple content pages, while theme `pages` files fit custom layouts, custom logic, or additional styling.
