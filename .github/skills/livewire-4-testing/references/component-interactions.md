# Component Interactions

## Mounting Components
- The retrieved docs initialize component tests with `Livewire::test(...)`.
- Confirmed examples include `Livewire::test('post.create')` and `Livewire::test(UpdatePost::class, ['post' => $post])`.
- Use mount parameters only in the documented second argument array form.

## PHPUnit Shape
- The retrieved docs show PHPUnit tests importing `Livewire\Livewire` and extending `Tests\TestCase`.
- The confirmed flow is: prepare model state, run `Livewire::test(...)`, chain `set()` calls, call a public action with `call()`, then assert external state such as model count.

## Interaction Helpers
- `set('property', $value)` sets one public property.
- `set(['property1' => $value1, 'property2' => $value2])` sets multiple public properties.
- `toggle('booleanProperty')` toggles a boolean property.
- `call('methodName')` calls a public method.
- `call('methodName', $param1, $param2)` calls a public method with parameters.
- `refresh()` triggers a component re-render.
- `dispatch('eventName')` dispatches an event from the test.
- `dispatch('eventName', $param1, $param2)` dispatches an event with parameters; the retrieved docs include a named-argument shape such as `postId: $post->id`.

## Rendered Output And View Data
- `assertSee('...')` checks rendered text in the component output.
- `assertViewHas('posts', function ($posts) { ... })` checks view data with a callback.
- `assertViewHas('postCount', 3)` checks a view value directly.

## Cautions
- Do not use unconfirmed output assertions or HTTP response assertions just because they exist in Laravel tests.
- Confirm class names, string component names, and mount parameter keys against the component under test and the current Context7 result.