---
name: filament-5-components
description: 'Use when: working with Filament 5 Components, reusable Blade components, x-filament:: Blade UI, Avatar, Badge, Button, Breadcrumbs, Callout, Checkbox, Dropdown, Empty state, Fieldset, Icon button, Input, Input wrapper, Link, Loading indicator, Modal, Pagination, Section, Select, Tabs, consistent design, custom Blade views, and plugin UI. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Blade component task, reusable UI, custom Blade view, component catalog lookup, or code to review'
---

# Filament 5 Components

## Purpose
Use this skill to create, review, or explain Filament 5 reusable Blade components using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Components topic.
2. Do not add component names, props, slots, attributes, default values, color values, size values, events, JavaScript behavior, customization guidance, or conventions unless they appear in the retrieved documentation.
3. If a requested component detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Do not infer shared props from similar components. Confirm each prop or value for the exact component being used.
5. Keep examples close to documented snippets and preserve documented component tags, attribute names, slot names, event names, and value strings.

## Reference Map
- Component scope, package-component boundary, inventory, and shared usage rules: [component-overview.md](./references/component-overview.md)
- Avatars, badges, buttons, icon buttons, links, loading indicators, callouts, and empty states: [display-actions-feedback.md](./references/display-actions-feedback.md)
- Inputs, wrappers, checkbox, select, fieldset, breadcrumbs, pagination, dropdowns, modals, sections, and tabs: [forms-navigation-structure.md](./references/forms-navigation-structure.md)

## Workflow
1. Identify whether the request is about Blade UI components or one of Filament's package components.
2. For package components listed in the docs as Action, Form, Infolist, Notifications, Schema, Table, or Widget, route to the corresponding Filament 5 skill instead of treating it as a Blade component task.
3. For Blade component tasks, run a narrow Context7 query for the exact component and concern before producing code.
4. Load the relevant reference file from the map above.
5. Choose the documented component tag exactly, such as `x-filament::button`, `x-filament::modal`, `x-filament::input.wrapper`, `x-filament::input`, `x-filament::input.checkbox`, or `x-filament::input.select`.
6. Use only documented attributes and slots for that component. Preserve documented camelCase slot names such as `afterHeader` and `footerActions`.
7. For action-like components, verify the underlying tag behavior before using `tag`, `href`, `wire:click`, or button behavior.
8. For icons, colors, sizes, tooltips, badges, and layout options, confirm the exact allowed values for the specific component.
9. For inputs and selects, wrap them in `x-filament::input.wrapper` when the docs require it.
10. For modals, verify whether the task needs a trigger slot, JavaScript-controlled `id`, Livewire or Alpine dispatch, heading, description, footer, slide-over, sticky header/footer, width, close behavior, autofocus behavior, or disabled trigger behavior.
11. For component styling or replacement, use only documented component customization points. Use the Filament 5 Styling skill for CSS hooks, custom themes, assets, and published Blade view guidance.
12. Finish by checking that every component tag, attribute, slot, value, event, and code example in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Filament packages consume core components for consistent and maintainable interfaces; some are available for applications and plugins.
- Filament projects can consume internal Blade components used by Filament itself.
- Confirmed Blade components are Avatar, Badge, Button, Breadcrumbs, Callout, Checkbox, Dropdown, Empty state, Fieldset, Icon button, Input, Input wrapper, Link, Loading indicator, Modal, Pagination, Section, Select, and Tabs.
- Confirmed package components listed separately in the docs are Action, Form, Infolist, Notifications, Schema, Table, and Widget.
- Many Blade components use the `x-filament::` namespace. Input variants documented in the retrieved docs include `x-filament::input.checkbox` and `x-filament::input.select`.
- Inputs and selects are documented inside `x-filament::input.wrapper`.
- Buttons, links, icon buttons, dropdown items, and tab items have documented tag-switching behavior, but the defaults and valid examples differ by component.
- Badge slots are documented on buttons, links, icon buttons, dropdown list items, and tab items.
- Tooltip attributes are documented on buttons, links, and icon buttons.
- Modal open and close behavior is documented through the `trigger` slot or browser events named `open-modal` and `close-modal` when an `id` is present.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each Blade tag, prop, slot, attribute, default, allowed value, event, and example is traceable to retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Tailwind habits, Laravel habits, package source code, or memory.
- If the user asks for a component detail not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented tag names, slot names, attribute names, event names, and value strings intact.