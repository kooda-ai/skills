# Branding and Layout

Use this reference after a fresh Context7 lookup for the exact Filament 5 styling topic.

## Brand Name and Logo
- By default, Filament uses the app's name to render a simple text-based logo.
- Change the text used in the logo with `brandName()`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->brandName('Filament Demo');
}
```

- Render an image logo by passing a public URL to `brandLogo()`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->brandLogo(asset('images/logo.svg'));
}
```

- Render HTML, such as an inline SVG view, by passing a callback to `brandLogo()`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->brandLogo(fn () => view('filament.admin.logo'));
}
```

- The docs show an inline SVG view using `class="h-full fill-gray-500 dark:fill-gray-400"`.
- If a different logo is needed in dark mode, pass it to `darkModeBrandLogo()` in the same way.
- Customize rendered logo height with `brandLogoHeight()`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->brandLogo(fn () => view('filament.admin.logo'))
        ->brandLogoHeight('2rem');
}
```

## Favicon
- Add a favicon by passing the public URL of the favicon in panel configuration:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->favicon(asset('images/favicon.png'));
}
```

## Maximum Content Width
- By default, Filament restricts the width of page content so it does not become too wide on large screens.
- Change the maximum page content width with `maxContentWidth()`.
- The docs state that options correspond to Tailwind's max-width scale.
- The documented options are `ExtraSmall`, `Small`, `Medium`, `Large`, `ExtraLarge`, `TwoExtraLarge`, `ThreeExtraLarge`, `FourExtraLarge`, `FiveExtraLarge`, `SixExtraLarge`, `SevenExtraLarge`, `Full`, `MinContent`, `MaxContent`, `FitContent`, `Prose`, `ScreenSmall`, `ScreenMedium`, `ScreenLarge`, `ScreenExtraLarge`, and `ScreenTwoExtraLarge`.
- The default is `SevenExtraLarge`.

```php
use Filament\Panel;
use Filament\Support\Enums\Width;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->maxContentWidth(Width::Full);
}
```

## Simple Page Content Width
- Use `simplePageMaxContentWidth()` to set the max content width for pages of type `SimplePage`, such as login and registration pages.
- The default simple page maximum width is `Large`.

```php
use Filament\Panel;
use Filament\Support\Enums\Width;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->simplePageMaxContentWidth(Width::Small);
}
```