# Component Overview

Use this reference after a fresh Context7 lookup for the exact Filament 5 Components topic.

## Component Scope
- Filament packages consume a set of core components that aim to provide a consistent and maintainable foundation for interfaces.
- Some of these components are available for use in applications and Filament plugins.
- The docs list package components separately from Blade components.

## Package Components
The docs list these package components as usable outside a panel:

- Action
- Form
- Infolist
- Notifications
- Schema
- Table
- Widget

When the user asks about one of these package components, use the more specific Filament 5 skill for that package when available.

## Blade Component Inventory
The docs list these Blade components as consumable by Filament projects:

- Avatar
- Badge
- Button
- Breadcrumbs
- Callout
- Checkbox
- Dropdown
- Empty state
- Fieldset
- Icon button
- Input
- Input wrapper
- Link
- Loading indicator
- Modal
- Pagination
- Section
- Select
- Tabs

## Usage Guardrails
- Use the documented `x-filament::` component tag exactly.
- Do not infer a prop, slot, color, size, default, or event from one component to another.
- Use documented slots exactly as named. The docs include camelCase slot names such as `afterHeader` and `footerActions`.
- Keep Livewire examples, Alpine examples, and native HTML tag switching exactly aligned with the component page that documents them.
- For CSS hooks, custom themes, assets, or publishing Blade views, use the Filament 5 Styling skill after a fresh Context7 lookup.

## Shared Values Confirmed Across Specific Components
- `primary`, `danger`, `gray`, `info`, `success`, and `warning` appear as documented color values on several components, but each component documents its own defaults and allowed values.
- `icon` and `icon-position="after"` are documented for badges, buttons, links, and tabs items.
- Badge slots are documented for buttons, links, icon buttons, dropdown list items, and tabs items.
- `tag="a"` with `href` is documented for buttons, icon buttons, dropdown list items, and tabs items.
- `tag="button"` is documented for links.
