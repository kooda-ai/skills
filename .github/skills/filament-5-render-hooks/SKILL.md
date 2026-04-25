---
name: filament-5-render-hooks
description: 'Use when: working with Filament 5 Advanced Render Hooks, FilamentView::registerRenderHook(), FilamentView::renderHook(), PanelsRenderHook, TablesRenderHook, ActionsRenderHook, WidgetsRenderHook, Panel renderHook(), scoped hooks, hook data, plugin Blade injection, page/resource/relation/table-widget hooks, auth/topbar/sidebar/content/body/head/table/action-modal/widget hook points. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Render hook task, hook point to choose, plugin Blade injection, scoped hook, data-aware hook, or code to review'
---

# Filament 5 Advanced Render Hooks

## Purpose
Use this skill to create, review, or explain Filament 5 render hooks using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact render-hook topic.
2. Do not add render-hook behavior, hook names, namespaces, callback signatures, return types, scope behavior, data keys, panel configuration shortcuts, or plugin guidance unless they appear in the retrieved documentation or the loaded reference files.
3. If the current Context7 lookup conflicts with a reference file, the current Context7 lookup wins.
4. If a requested hook point, data key, or scope behavior is not confirmed, run a narrower Context7 lookup or say that the current documentation context did not confirm it.
5. Keep examples close to documented snippets and preserve documented class names, enum names, method names, argument names, and callback signatures.

## Reference Map
- Core registration, panel shortcut, scoping, data passing, custom hook rendering, and decision flow: [render-hooks.md](./references/render-hooks.md)
- Available documented hook families and hook constants: [available-render-hooks.md](./references/available-render-hooks.md)

## Workflow
1. Identify the target surface: Panel Builder, Table Builder, Actions modal content/schema, Widgets table widget, or a custom plugin-exposed hook.
2. Run a narrow Context7 query for the exact render-hook task before producing code.
3. Load [render-hooks.md](./references/render-hooks.md) for API patterns and [available-render-hooks.md](./references/available-render-hooks.md) when choosing hook constants.
4. Choose the registration path: `FilamentView::registerRenderHook()` from a service provider or middleware, or panel-specific `$panel->renderHook()` from panel configuration when the docs confirm the panel shortcut is appropriate.
5. Choose the callback return pattern from the docs: a `string` returned from `Blade::render(...)`, or an `Illuminate\Contracts\View\View` returned from `view(...)`.
6. Select the hook enum family exactly as documented: `Filament\View\PanelsRenderHook`, `Filament\Tables\View\TablesRenderHook`, `Filament\Actions\View\ActionsRenderHook`, or `Filament\Widgets\View\WidgetsRenderHook`.
7. Apply scoping only where documented. Use a class string or array of class strings with the `scopes` argument; use resource class scoping only for Panel Builder hooks documented as allowing resource-wide scope.
8. For hooks that need context, use documented callback injection: `array $scopes` for active scopes, `array $data` for data passed at the render point, and documented data entries such as table `filterIndicators`, table `column` / `isReordering`, or action `action` only when the lookup confirms them.
9. For plugin-exposed hooks, render them in Blade with `FilamentView::renderHook(...)`; pass `scopes:` and `data:` only as documented.
10. Finish by checking that every hook constant, class import, method call, callback parameter, return type, data key, and code example is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Render hooks render Blade content at specific points within Filament framework views.
- The docs describe render hooks as useful for plugins that inject HTML into the framework and for users who should avoid publishing Filament views because of increased breaking-change risk.
- `FilamentView::registerRenderHook()` is called from a service provider or middleware.
- The first argument to `registerRenderHook()` is the render hook name, and the second argument is a callback returning rendered content.
- Documented callback examples return either `string` from `Blade::render(...)` or `Illuminate\Contracts\View\View` from `view(...)`.
- Panel configuration can register panel-specific hooks with `Panel::renderHook()`.
- Some render hooks can be scoped to a specific page or Livewire component, and some Panel Builder hooks can be scoped to all pages in a resource.
- Render hooks can receive data from the point where the hook is rendered by accepting an `array $data` parameter in the callback.
- Plugin developers can expose hooks by outputting `FilamentView::renderHook(...)` in Blade without separately registering the hook.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup and the loaded reference files.
- Every method, enum, constant, namespace, callback parameter, return type, scope target, data key, and Blade expression is traceable to Filament 5.x documentation.
- Unconfirmed hook constants are not inferred from Filament 4.x, older examples, package source code, Laravel habits, Livewire habits, or memory.
- If the user asks for a hook point not present in the current Context7 result or reference map, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, enum names, method names, argument names, callback signatures, and hook constants intact.