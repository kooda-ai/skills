# Styling and Navigation Configuration

Use this reference after a fresh Context7 lookup for the exact Filament 5 styling or navigation topic.

## Colors, Fonts, and Theme Mode
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
- The docs also show generating a palette from a hex or RGB value with `colors(['primary' => '#6366f1'])` or `colors(['primary' => 'rgb(99, 102, 241)'])`.
- A custom palette may be passed as an array of OKLCH colors.
- Change the font with `font('Poppins')`; the docs state Google Fonts are available.
- Bunny Fonts CDN is used to serve fonts by default.
- Use Google Fonts CDN with `font('Inter', provider: GoogleFontProvider::class)` and `Filament\FontProviders\GoogleFontProvider`.
- Serve fonts from a local stylesheet with `font('Inter', url: asset('css/fonts.css'), provider: LocalFontProvider::class)` and `Filament\FontProviders\LocalFontProvider`.
- Disable dark mode switching with `darkMode(false)`.
- Force the default theme mode with `defaultThemeMode(ThemeMode::Light)` or `defaultThemeMode(ThemeMode::Dark)` using `Filament\Enums\ThemeMode`.
- By default, Filament uses the user's system theme, and system mode is reactive when the computer mode changes.

## Custom Themes
- Create a custom theme with `php artisan make:filament-theme`.
- For multiple panels, pass the panel name: `php artisan make:filament-theme admin`.
- Use a different package manager with `php artisan make:filament-theme --pm=bun`.
- The command installs Tailwind CSS dependencies, generates `resources/css/filament/{panel}/theme.css`, attempts to add the theme to the Vite input array, attempts to register `viteTheme()` in the panel provider, and offers to compile the theme with Vite.
- Manual Vite setup adds the theme CSS to the Laravel plugin `input` array in `vite.config.js`, for example `resources/css/filament/admin/theme.css`.
- Register the theme CSS with `viteTheme('resources/css/filament/admin/theme.css')`.
- Compile the theme with `npm run build`.
- A custom theme is required to use Tailwind CSS classes in custom Blade views, Livewire components, or PHP files; Filament's default compiled stylesheet only contains styles needed by Filament UI components.
- Generated theme CSS includes `@source '../../../../app/Filament/**/*';` and `@source '../../../../resources/views/filament/**/*';`.
- Add more `@source` directives for custom directories, then rebuild with `npm run build`.

## Brand and Favicon
- Change the text logo with `brandName('Filament Demo')`.
- Render an image logo with `brandLogo(asset('images/logo.svg'))`.
- Render HTML, such as an inline SVG view, with `brandLogo(fn () => view('filament.admin.logo'))`.
- Provide a separate dark-mode logo with `darkModeBrandLogo()`.
- Customize rendered logo height with `brandLogoHeight('2rem')`.
- Add a favicon with `favicon(asset('images/favicon.png'))`.

## Navigation Items
- By default, Filament registers navigation items for resources, custom pages, and clusters.
- Change a Resource/Page navigation label with `protected static ?string $navigationLabel = 'Custom Navigation Label';` or `getNavigationLabel(): string`.
- Change a Resource/Page icon with `protected static string | BackedEnum | null $navigationIcon = Heroicon::OutlinedDocumentText;` using `Filament\Support\Icons\Heroicon`.
- Change the active icon with `protected static string | BackedEnum | null $activeNavigationIcon = Heroicon::OutlinedDocumentText;`.
- If all items in the same navigation group set `$navigationIcon = null`, those items are joined with a vertical bar below the group label.
- Sort navigation items with `protected static ?int $navigationSort = 3;`; lower sort values appear first.
- Add a badge with `getNavigationBadge(): ?string`.
- Badge colors returned from `getNavigationBadgeColor(): ?string` may be `danger`, `gray`, `info`, `primary`, `success`, or `warning`.
- Add a badge tooltip with `$navigationBadgeTooltip` or `getNavigationBadgeTooltip(): ?string`.
- Hide a Resource/Page navigation item with `protected static bool $shouldRegisterNavigation = false;` or `shouldRegisterNavigation(): bool`.
- The docs state those methods only control whether the item appears in navigation, not direct access.

## Navigation Groups and Custom Navigation
- Group navigation items with `protected static string | UnitEnum | null $navigationGroup = 'Settings';`.
- Group items under a parent with `protected static ?string $navigationParentItem = 'Notifications';`.
- If the parent item has a navigation group, the child must define the same group so the parent can be identified.
- The docs suggest considering clusters if reaching for a third level of navigation.
- Customize navigation groups with `navigationGroups()` and `Filament\Navigation\NavigationGroup` objects.
- `NavigationGroup::make()->label('Shop')->icon(Heroicon::OutlinedShoppingCart)` sets a label and icon.
- `collapsed()` makes a group collapsed by default.
- Reorder groups by passing only labels to `navigationGroups(['Shop', 'Blog', 'Settings'])`.
- Disable collapsible groups globally with `collapsibleNavigationGroups(false)`.
- Disable collapse for one group with `NavigationGroup::make()->collapsible(false)`.
- Add group DOM attributes with `extraSidebarAttributes()` and `extraTopbarAttributes()`.
- Register navigation groups with an enum; enum case order controls group order.
- Implement `Filament\Support\Contracts\HasLabel` on the enum for labels and `Filament\Support\Contracts\HasIcon` for icons.
- Register custom navigation items with `navigationItems([NavigationItem::make('Analytics')->url('https://filament.pirsch.io', shouldOpenInNewTab: true)->icon(...)->group('Reports')->sort(3)])`.
- Conditionally hide a `NavigationItem` with `visible()` or `hidden()`.
- For full custom navigation, call `navigation(function (NavigationBuilder $builder): NavigationBuilder { ... })`.
- In custom navigation, `items()` registers custom items and `groups()` registers custom groups.
- Disable navigation with `navigation(false)` or with a closure returning a boolean.

## Sidebar, Topbar, and Breadcrumbs
- Use top navigation with `topNavigation()`; Filament otherwise uses sidebar navigation by default.
- Make the desktop sidebar collapsible with `sidebarCollapsibleOnDesktop()`.
- Fully collapse the desktop sidebar with `sidebarFullyCollapsibleOnDesktop()`.
- Customize sidebar width with `sidebarWidth('40rem')`.
- When using `sidebarCollapsibleOnDesktop()`, customize the collapsed icon width with `collapsedSidebarWidth('9rem')`.
- Disable the topbar with `topbar(false)`.
- Replace sidebar and topbar Livewire components with `sidebarLivewireComponent(Sidebar::class)` and `topbarLivewireComponent(Topbar::class)`.
- Disable breadcrumbs with `breadcrumbs(false)`.
- Reload sidebar and topbar by dispatching `refresh-sidebar` or `refresh-topbar` browser events.
- From a Livewire component, use `$this->dispatch('refresh-sidebar')`.
- From an action closure, inject `Livewire\Component $livewire` and call `$livewire->dispatch('refresh-sidebar')`.
- From JavaScript, use Alpine `$dispatch('refresh-sidebar')` or `window.dispatchEvent(new CustomEvent('refresh-sidebar'))`.