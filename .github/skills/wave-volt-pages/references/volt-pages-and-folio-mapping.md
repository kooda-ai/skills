# Volt Pages And Folio Mapping

## Theme Pages
- Theme `pages` directories are mapped to routes using Laravel Folio.
- The docs show examples such as:
  - `pages/index.blade.php` => `/`
  - `pages/about.blade.php` => `/about`
  - `pages/about/index.blade.php` => `/about`
  - `pages/blog/index.blade.php` => `/blog`
  - `pages/blog/[post].blade.php` => `/blog/{post}`
  - `pages/contact.blade.php` => `/contact`

## Volt In Theme Pages
- The docs say those page files can contain single-file Volt components.
- The Wave docs show a single-file Volt page example inside the theme page structure.

## Adding Functionality
- The `your-functionality` docs recommend single-file Volt pages in `resources/themes/{theme}/pages` for new functionality.
- The docs say you may still move complex logic into services or controllers to keep the page maintainable.

## Filament With Volt
- The `Using Filament With Volt` guide demonstrates Filament tables and forms directly inside Wave theme pages.
- The guide shows rendering `{{ $this->table }}` and `{{ $this->form }}` within a Volt page.
