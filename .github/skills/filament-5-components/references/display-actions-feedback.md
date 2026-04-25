# Display, Actions, and Feedback Components

Use this reference after a fresh Context7 lookup for the exact Filament 5 component topic.

## Avatar
- Renders a circular or square image, often for a user or entity profile picture.
- Basic usage: `x-filament::avatar` with `src` and `alt`.
- Avatars are fully rounded by default.
- Set `:circular="false"` to make the avatar square.
- Default size is medium.
- Documented size values are `sm`, `md`, and `lg`.
- Custom size classes may be passed to `size`, such as `w-12 h-12`.

## Badge
- Renders a small box with text.
- Basic usage: `x-filament::badge`.
- Default size is medium.
- Documented size values are `xs` and `sm`.
- Default color is primary.
- Documented color values are `danger`, `gray`, `info`, `success`, and `warning`.
- Add an icon with `icon`.
- Place the icon after the text with `icon-position="after"`.

## Button
- Renders a clickable button that can perform an action.
- Basic usage: `x-filament::button` with attributes such as `wire:click`.
- The underlying HTML tag is `<button>` by default.
- Use `tag="a"` with `href` to render an anchor link.
- Default size is medium.
- Documented size values are `xs`, `sm`, `lg`, and `xl`.
- Default color is primary.
- Documented color values are `danger`, `gray`, `info`, `success`, and `warning`.
- Add an icon with `icon`.
- Place the icon after the text with `icon-position="after"`.
- Use `outlined` for the outlined design; the docs show it can combine with colors.
- Add a tooltip with `tooltip`.
- Add a badge with the `badge` slot.
- Change the badge color with `badge-color`.

## Icon Button
- Renders a clickable icon button that can perform an action.
- Basic usage: `x-filament::icon-button` with `icon`, an action such as `wire:click`, and `label`.
- The underlying HTML tag is `<button>` by default.
- Use `tag="a"` with `href` to render an anchor link.
- Default size is medium.
- Documented size values are `xs`, `sm`, `lg`, and `xl`.
- Default color is primary.
- Documented color values are `danger`, `gray`, `info`, `success`, and `warning`.
- Add a tooltip with `tooltip`.
- Add a badge with the `badge` slot.
- Change the badge color with `badge-color`.

## Link
- Renders a clickable link that can perform an action.
- Basic usage: `x-filament::link` with `:href`.
- The underlying HTML tag is `<a>` by default.
- Use `tag="button"` for button behavior, for example with `wire:click`.
- Default size is medium.
- Documented size values are `sm`, `lg`, `xl`, and `2xl`.
- Default font weight is `semibold`.
- Documented weight values are `thin`, `extralight`, `light`, `normal`, `medium`, `semibold`, `bold`, `extrabold`, and `black`.
- A custom CSS class may be passed to `weight`, such as `md:font-[650]`.
- Default color is primary.
- Documented color values are `danger`, `gray`, `info`, `success`, and `warning`.
- Add an icon with `icon`.
- Place the icon after the text with `icon-position="after"`.
- Add a tooltip with `tooltip`.
- Add a badge with the `badge` slot.
- Change the badge color with `badge-color`.

## Loading Indicator
- Renders an animated SVG to indicate progress.
- Basic usage: `x-filament::loading-indicator` with classes such as `h-5 w-5`.
- Filament renders the indicator through `Filament\Support\Contracts\LoadingIndicator`, bound to `Filament\Support\View\DefaultLoadingIndicator` by default.
- Replace it by binding a different class to `LoadingIndicator` in a service provider.
- A custom implementation must implement `toHtml(ComponentAttributeBag $attributes): string`.
- The docs state the attributes already contain `fi-icon fi-loading-indicator` and size hook classes, so they can be forwarded to the root element.
- The resolved instance is cached for the lifetime of the PHP process; under Laravel Octane, register the binding in a service provider rather than rebinding at runtime.

## Callout
- Draws attention to important information or messages.
- Basic usage: `x-filament::callout` with `icon`, `color`, and `heading` and `description` slots.
- Status colors documented for callouts are `danger`, `info`, `success`, and `warning`.
- The docs also show `color="primary"` as a custom background color example.
- Add an icon with `icon`.
- By default, icon color inherits from the callout color.
- Override icon color with `icon-color`.
- Default icon size is large.
- Documented icon size values are `sm` and `md`.
- Add footer content with the `footer` slot; the docs show text and a Filament button.
- Add top-right controls with the `controls` slot; the docs show an icon button.
- A callout may be rendered without an icon.
- A callout may be rendered with only a heading and no description.

## Empty State
- Communicates that there is no content to display yet and can guide the user toward the next action.
- A heading is required through the `heading` slot.
- Add supporting text with the `description` slot.
- Add an icon with `icon`.
- Default icon color is primary.
- Documented icon color values are `gray`, `danger`, `info`, `success`, and `warning`.
- Default icon size is large.
- Documented icon size values are `sm` and `md`.
- Add footer actions with the `footer` slot; the docs show a Filament button.
- By default, empty states have a background color, shadow, and border.
- Remove the container with `:contained="false"`.
