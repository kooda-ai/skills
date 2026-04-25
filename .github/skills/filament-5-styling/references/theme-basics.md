# Theme Basics

Use this reference after a fresh Context7 lookup for the exact Filament 5 styling topic.

## Colors
- Change framework colors with `colors()` in panel configuration.
- Filament ships with 6 predefined colors used throughout the framework: `danger`, `gray`, `info`, `primary`, `success`, and `warning`.

```php
use Filament\Panel;
use Filament\Support\Colors\Color;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->colors([
            'danger' => Color::Rose,
            'gray' => Color::Gray,
            'info' => Color::Blue,
            'primary' => Color::Indigo,
            'success' => Color::Emerald,
            'warning' => Color::Orange,
        ]);
}
```

- `Filament\Support\Colors\Color` contains color options for all Tailwind CSS color palettes.
- The docs show generating a palette from a singular hex value or RGB value:

```php
$panel
    ->colors([
        'primary' => '#6366f1',
    ])

$panel
    ->colors([
        'primary' => 'rgb(99, 102, 241)',
    ])
```

- The docs also show passing a custom palette as an array of OKLCH colors:

```php
$panel
    ->colors([
        'primary' => [
            50 => 'oklch(0.969 0.015 12.422)',
            100 => 'oklch(0.941 0.03 12.58)',
            200 => 'oklch(0.892 0.058 10.001)',
            300 => 'oklch(0.81 0.117 11.638)',
            400 => 'oklch(0.712 0.194 13.428)',
            500 => 'oklch(0.645 0.246 16.439)',
            600 => 'oklch(0.586 0.253 17.585)',
            700 => 'oklch(0.514 0.222 16.935)',
            800 => 'oklch(0.455 0.188 13.697)',
            900 => 'oklch(0.41 0.159 10.272)',
            950 => 'oklch(0.271 0.105 12.094)',
        ],
    ])
```

## Fonts
- The docs state that the default font is Inter.
- Change the panel font with `font()` in panel configuration:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->font('Poppins');
}
```

- The docs state that all Google Fonts are available to use.
- Bunny Fonts CDN is used to serve fonts by default.
- To use Google Fonts CDN instead, pass the `provider` argument of `font()`:

```php
use Filament\FontProviders\GoogleFontProvider;

$panel->font('Inter', provider: GoogleFontProvider::class)
```

- To serve fonts from a local stylesheet, use `LocalFontProvider` and a `url`:

```php
use Filament\FontProviders\LocalFontProvider;

$panel->font(
    'Inter',
    url: asset('css/fonts.css'),
    provider: LocalFontProvider::class,
)
```

## Custom Themes
- Filament allows changing the CSS used to render the UI by compiling a custom stylesheet that replaces the default one.
- The docs call this custom stylesheet a theme, and state that themes use Tailwind CSS.
- Create a custom theme with:

```bash
php artisan make:filament-theme
```

- If there are multiple panels, specify the panel:

```bash
php artisan make:filament-theme admin
```

- By default, the command uses NPM to install dependencies. Use the `--pm` option for a different package manager:

```bash
php artisan make:filament-theme --pm=bun
```

- The command will install required Tailwind CSS dependencies, generate `resources/css/filament/{panel}/theme.css`, attempt to add the theme to the `vite.config.js` input array, attempt to register `->viteTheme()` in the panel provider, and offer to compile the theme with Vite.
- If automatic configuration fails because of non-standard formatting, the command displays manual instructions.
- Manual configuration adds the theme CSS file to the Laravel plugin's `input` array in `vite.config.js`:

```js
input: [
    // ...
    'resources/css/filament/admin/theme.css',
]
```

- Register the Vite-compiled theme CSS file in the panel provider:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->viteTheme('resources/css/filament/admin/theme.css');
}
```

- Compile the theme with Vite:

```bash
npm run build
```

- The docs say to check the command output for the exact file path, for example `admin/theme.css`, because it may vary depending on the panel ID.
- After setup, customize the theme by editing the CSS file in `resources/css/filament`.

## Tailwind Classes in Application Code
- A custom theme is required to use Tailwind CSS classes in custom Blade views, Livewire components, or PHP files.
- The docs state that Filament's default compiled stylesheet does not include arbitrary Tailwind classes; it only contains the styles needed for Filament's own UI components.
- The generated `theme.css` contains `@source` directives that tell Tailwind CSS where to scan for classes:

```css
@source '../../../../app/Filament/**/*';
@source '../../../../resources/views/filament/**/*';
```

- Add custom directories where Tailwind classes are used, for example:

```css
@source '../../../../app/Filament/**/*';
@source '../../../../resources/views/filament/**/*';
@source '../../../../resources/views/components/**/*';
@source '../../../../resources/views/livewire/**/*';
@source '../../../../app/Livewire/**/*';
```

- After adding directories, rebuild the theme:

```bash
npm run build
```

## Dark Mode
- Disable dark mode switching in panel configuration with `darkMode(false)`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->darkMode(false);
}
```

- By default, Filament uses the user's system theme as the default mode.
- The docs state that system mode is reactive when the user's computer mode changes.
- Force light or dark mode with `defaultThemeMode()` and `Filament\Enums\ThemeMode`:

```php
use Filament\Enums\ThemeMode;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->defaultThemeMode(ThemeMode::Light);
}
```

- The docs confirm `ThemeMode::Light` and `ThemeMode::Dark`.