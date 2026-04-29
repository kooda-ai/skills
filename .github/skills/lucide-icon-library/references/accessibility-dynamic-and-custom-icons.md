# Accessibility, Dynamic Loading, And Custom Icons

Use this file when the user asks about accessible icons, icon buttons, dynamic icon loading, Lucide Lab, or custom icon composition.

## Accessibility Rules Confirmed In The Docs
- Multiple package docs say icons are hidden from screen readers by default and become meaningful when given an accessible name.
- Core web docs show `aria-label` on a meaningful icon and indicate this removes the default `aria-hidden` behavior.
- Astro docs show both `<title>` children and `aria-label` for making an icon accessible.
- Preact docs show both `<title>` and `aria-label` on icons.
- Angular docs show `title` on `<svg lucide...>` and show button labels placed on the button element.
- The general accessibility docs say icon buttons should be labeled on the button, not on the decorative icon.
- The general accessibility docs show visually hidden text patterns such as `sr-only` and `visually-hidden`.
- The general accessibility docs also say not to add `aria-label` to a decorative icon when the parent button already has visible text.

## Dynamic Loading Cautions
- React docs provide `DynamicIcon` from `lucide-react/dynamic` and caution about build time increases and network request overhead.
- Vue docs show a generic computed loader that imports `* as icons` and explicitly caution that importing all icons can significantly increase build size and negatively impact performance.
- Solid docs show a generic dynamic component over `icons` and note that it imports all icons and may negatively impact bundle size.
- Preact docs show a generic component over `icons` and caution about build size and performance.
- React Native docs show a generic component over `lucide-react-native/icons` and caution about build size and performance.
- Svelte docs show generic icon components and also show direct icon imports for faster builds.

## Lucide Lab And Custom Icons
- Core web docs show registering Lucide Lab icons with `createIcons()`.
- React docs show rendering custom icons with `Icon` and `iconNode`.
- Vue docs show rendering custom icons with `Icon` and `iconNode`.
- Svelte docs show rendering custom icons with `Icon` and `iconNode`.
- Solid docs show rendering custom icons with `Icon` and `iconNode`.
- Preact docs show rendering custom icons with `Icon` and `iconNode`.
- React Native docs show rendering custom icons with `Icon` and `iconNode`.
- Astro docs show rendering custom icons with `Icon` and `iconNode`.

## Composition Patterns In Docs
- Multiple framework docs show nesting one Lucide icon inside another by placing a child icon inside the parent icon and positioning it with `x` and `y`.
- Multiple docs say nested icon coordinates should stay inside the outer icon's `24x24` viewBox.
- Multiple docs show adding a native SVG `circle` as a notification badge.
- Multiple docs show adding native SVG `text` inside the icon for labels or overlays.

## Review Guardrails
- If the user asks for accessibility help, check whether the icon is decorative or meaningful before adding a label.
- If the icon is the only visible content inside a button, use the documented button-label patterns.
- If the approach imports all icons, surface the build-size warning exactly when the docs do.
