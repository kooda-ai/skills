# Context7 Query Prompts

Use these query shapes to refresh the source context before answering Livewire 4 lifecycle hook questions. Always keep the query scoped to `/websites/livewire_laravel_4_x`.

## Lifecycle Overview
```text
Livewire 4 lifecycle hooks documentation: complete component lifecycle hook table, mount(), hydrate(), boot(), updating(), updated(), rendering(), rendered(), dehydrate(), exception($e, $stopPropagation), when each hook runs, method signatures, parameters, and documented examples. Return documented APIs, signatures, examples, and caveats only.
```

## Mount And Boot
```text
Livewire 4 lifecycle hooks documentation for mount() and boot(): accepting parameters, initializing state, why Livewire uses mount() instead of __construct(), dependency injection in lifecycle hook methods, boot() running on initial and subsequent requests, protected properties not persisted between requests, computed property note, #[Locked] and authorization guidance for sensitive public properties. Return documented APIs, examples, and caveats only.
```

## Update Hooks
```text
Livewire 4 lifecycle hooks documentation for property update hooks: updating($property, $value), updated($property), property-specific hooks such as updatedUsername() and updatingUsername(), array property hooks such as updatedPreferences($value, $key), null key behavior when replacing the whole array, validating, authorizing, preventing updates, and normalizing property values. Return documented signatures, examples, and caveats only.
```

## Hydrate, Dehydrate, Render, Exception
```text
Livewire 4 lifecycle hooks documentation for hydrate(), dehydrate(), rendering($view, $data), rendered($view, $html), and exception($e, $stopPropagation): when hooks run, DTO transformation example, serialization and unserialization terms, Wireables or Synthesizers recommendation, render hook parameters, exception handling, and stopPropagation behavior. Return documented signatures, examples, and caveats only.
```

## Trait And Form Object Hooks
```text
Livewire 4 lifecycle hooks documentation for using hooks inside traits and form objects: camelCased trait-prefixed hook methods, HasPostForm examples, Livewire\Form property update hooks, updating($property, $value), updated($property, $value), updatingTitle($value), updatedTitle($value), updatingTags($value, $key), and updatedTags($value, $key). Return documented signatures, examples, and caveats only.
```