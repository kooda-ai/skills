# Rendering, Props, And Keys

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 nesting topic.

## Extraction Decision
- Before extracting template content into a nested Livewire component, ask whether the content needs to be live.
- If the content does not need Livewire dynamic behavior, the docs recommend a simple Blade component instead.
- Only create a nested Livewire component when it benefits from Livewire's dynamic nature or gives a direct performance benefit.
- If the goal is isolated re-rendering inside one component without child component overhead, the docs recommend considering islands.

## Nesting A Component
- Nest a Livewire child by placing its tag in a parent Blade view, such as `<livewire:todos />`.
- On the page's initial render, the parent encounters the child tag and renders it in place.
- On a later network request to the parent, the nested component skips rendering because it is now its own independent component on the page.

## Passing Props To Children
- Dynamic prop syntax supports PHP expressions, such as `<livewire:todo-count :todos="$this->todos" />`.
- The child can receive passed data through `mount($todos)`.
- The `mount()` method can be omitted when the public property and parameter names match.
- Static string props omit the colon, such as `label="Todo Count:"`.
- Boolean true values can be passed by specifying only the key, such as `inline`.
- When the variable name and prop name are the same, shortened syntax can prefix the variable with a colon, such as `<livewire:todo-count :$todos />`.

## Rendering Children In A Loop
- When rendering a child component within a loop, include a unique key value for each iteration.
- The docs show `:wire:key="$todo->id"` on a nested component inside a loop.
- Component keys let Livewire track components on later renders, especially when already-rendered components are re-ordered.
- The docs state that keys are not optional for Livewire child components in loops and that Livewire will behave incorrectly without them.

## Forcing Child Re-rendering
- Livewire generates a key for each nested Livewire component behind the scenes.
- When a parent later encounters a child whose key is already in the parent's child list, Livewire skips rendering that child because nested components are independent.
- If the child key is not in the list, Livewire creates a new child instance and renders it in place.
- To force a child component to re-render, change its key.
- The docs show basing a key on passed data, such as `<livewire:todo-count :todos="$todos" :wire:key="$todos->pluck('id')->join('-')" />`.
- When the key changes, the child component is re-initialized from scratch and the old component is discarded.