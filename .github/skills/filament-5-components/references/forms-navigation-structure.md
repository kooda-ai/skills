# Forms, Navigation, and Structure Components

Use this reference after a fresh Context7 lookup for the exact Filament 5 component topic.

## Input and Input Wrapper
- `x-filament::input` wraps the native `<input>` element for entering a single line of text.
- The docs show `x-filament::input` inside `x-filament::input.wrapper` with `type="text"` and `wire:model`.
- `x-filament::input.wrapper` should wrap `x-filament::input` or `x-filament::input.select`.
- The wrapper provides a border and elements such as a prefix or suffix.
- Trigger invalid styling with `:valid="! $errors->has('name')"` on the wrapper.
- Trigger invalid styling with Alpine using `alpine-valid`.
- To disable an input, pass `disabled` to both the wrapper and the input.
- Add text before and after the input with `prefix` and `suffix` slots.
- Add icons before or after the input with `prefix-icon` and `suffix-icon` attributes.
- The docs show a colored suffix icon with `suffix-icon-color="success"`.

## Checkbox
- `x-filament::input.checkbox` renders a checkbox input for toggling a boolean value.
- The docs show it inside a `<label>` with text for accessibility.
- Trigger invalid styling with `:valid="! $errors->has('isAdmin')"`.
- Trigger invalid styling with Alpine using `alpine-valid`.
- The docs show Livewire binding with `wire:model` and Alpine binding with `x-model`.

## Select
- `x-filament::input.select` wraps the native `<select>` element.
- It provides a simple interface for selecting a single value from a list of options.
- The docs show it inside `x-filament::input.wrapper` with `wire:model` and native `<option>` elements.

## Fieldset
- Groups multiple form fields together, optionally with a label.
- Use `x-filament::fieldset`.
- Add the label with the `label` slot.

## Breadcrumbs
- Renders a simple, linear navigation showing the user's current location.
- Use `x-filament::breadcrumbs` with a `:breadcrumbs` array.
- The array keys are URLs the user can click.
- The array values are the text displayed for each link.

## Pagination
- Can be used in a Livewire Blade view only.
- Renders paginated links with `x-filament::pagination` and `:paginator`.
- The docs show passing a Laravel paginator from a Livewire component render method.
- Simple pagination and cursor pagination render previous and next buttons.
- Allow custom page sizes with `:page-options`.
- Store the selected page option in a Livewire property referenced by `current-page-option-property`.
- The docs show page options `[5, 10, 20, 50, 100, 'all']`.
- Add first and last page links with `extreme-links`.

## Dropdown
- Renders a dropdown menu with a trigger button.
- Use `x-filament::dropdown` with a `trigger` slot.
- Render items inside `x-filament::dropdown.list` using `x-filament::dropdown.list.item`.
- A dropdown item uses `<button>` by default.
- Use `tag="a"` with `href` to render a dropdown item as an anchor link.
- The default dropdown item color is gray.
- Documented dropdown item color values are `danger`, `info`, `primary`, `success`, and `warning`.
- Add an item icon with `icon`.
- By default, the icon color uses the same color as the item.
- Override item icon color with `icon-color`; documented values are `danger`, `info`, `primary`, `success`, and `warning`.
- Add a circular image to an item with `image`.
- Add a badge with the `badge` slot.
- Change the badge color with `badge-color`.
- Set dropdown placement with `placement`, such as `top-start`.
- Set dropdown width with `width`; documented options correspond to Tailwind's max-width scale: `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`, `6xl`, and `7xl`.
- Control dropdown maximum height with `max-height` using a CSS length such as `400px`.

## Modal
- Opens a dialog window or slide-over with any content.
- Use `x-filament::modal` with a `trigger` slot to render a button that opens it.
- A trigger slot is not required when opening and closing through JavaScript.
- Give the modal an `id` to control it from JavaScript.
- Dispatch `open-modal` or `close-modal` with the modal `id` to open or close it.
- The docs show Livewire dispatch as `$this->dispatch('open-modal', id: 'edit-user');`.
- The docs show Alpine dispatch as `$dispatch('open-modal', { id: 'edit-user' })`.
- Add a heading with the `heading` slot.
- Add a description below the heading with the `description` slot.
- Add an icon with `icon`.
- Default icon color is primary.
- Documented icon color values are `danger`, `gray`, `info`, `success`, and `warning`.
- Add a footer with the `footer` slot.
- Add footer actions with the `footerActions` slot.
- Change content alignment with `alignment="start"` or `alignment="center"`; modal content is aligned to start by default, or centered if the modal is `xs` or `sm` width.
- Use `slide-over` to open a slide-over dialog instead of a modal.
- Use `sticky-header` to make the modal header sticky; slide-overs have a sticky header by default.
- Use `sticky-footer` to make the modal footer sticky; slide-overs have a sticky footer by default.
- Change modal width with `width`; documented options are `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`, `6xl`, `7xl`, and `screen`.
- Disable closing by clicking away with `:close-by-clicking-away="false"`.
- Disable closing by escape with `:close-by-escaping="false"`.
- Hide the close button on modals with a header using `:close-button="false"`.
- Disable autofocus with `:autofocus="false"`.
- If a disabled trigger button should not open the modal, also use `disabled` on the `trigger` slot.

## Section
- Groups content together with an optional heading.
- Use `x-filament::section`.
- Add a heading with the `heading` slot.
- Add a description below the heading with the `description` slot.
- Add a header icon with `icon`.
- Default section icon color is gray.
- Documented icon color values are `danger`, `info`, `primary`, `success`, and `warning`.
- Default section icon size is large.
- Documented icon size values are `sm` and `md`.
- Render content at the end of the header using the `afterHeader` slot.
- Make content collapsible with `collapsible`.
- Collapse by default with `collapsed`.
- Persist collapsed state in local storage with `persist-collapsed`; the docs require a unique `id` so each section can persist its own collapse state.
- Put the header aside the content with `aside`.
- When using `aside`, put content before the header with `content-before`.

## Tabs
- Renders tabs for toggling between multiple sections of content.
- Use `x-filament::tabs` and `x-filament::tabs.item`.
- The docs show `label="Content tabs"` on the tabs component.
- Tabs do not appear active by default.
- Use `active` to make a tab appear active.
- Use `:active` for conditional active state, for example from a Livewire property.
- Use `alpine-active` for conditional active state from Alpine.js.
- Add an icon to a tab item with `icon`.
- Place the icon after the label with `icon-position="after"`.
- Add a badge to a tab item with the `badge` slot.
- A tab item uses `<button>` by default.
- Use `tag="a"` with `href` to render a tab item as an anchor link.
- Render tabs vertically with `vertical`.