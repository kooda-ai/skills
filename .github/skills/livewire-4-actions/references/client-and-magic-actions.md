# Client And Magic Actions

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 Alpine, JavaScript, magic action, or `$wire` topic.

## Calling PHP Actions From Alpine
- Livewire exposes a magic `$wire` object to Alpine inside Livewire components.
- `$wire.save()` calls the corresponding `save()` PHP action on the backend component.
- Parameters passed to `$wire.actionName(...)` are passed to the PHP method.
- Invoked `$wire` actions return a promise while the network request is processing.
- When the server response is received, the promise resolves with the backend action return value.
- The docs say that for actions primarily consumed by JavaScript, consider `#[Json]` so data returns through promise resolution or rejection, validation errors reject the promise, and re-rendering is skipped.

## JavaScript Actions
- JavaScript actions run entirely on the client side without making a server request.
- The docs describe JavaScript actions for simple UI updates that do not require server communication and optimistic UI updates before making a server request.
- Define a JavaScript action with `$js()` inside a component `<script>` tag.
- Call a JavaScript action from Blade with syntax such as `wire:click="$js.bookmark"`.
- Call a JavaScript action from Alpine with syntax such as `$wire.$js.bookmark()`.
- A PHP action can call a JavaScript action with `$this->js('onPostSaved')`.
- The documented class-based component requirement is to wrap script tags with `@script` and `@endscript` so JavaScript is scoped to the component.

## Magic Actions
The docs list these magic actions for use within event listeners in Blade templates:

- `$parent`: access parent component properties and call parent component actions from a child component.
- `$set`: update a component property directly from the Blade template, such as `$set('query', '')`.
- `$refresh`: re-render the component.
- `$toggle`: toggle a boolean property, such as `$toggle('sortAsc')`.
- `$dispatch`: dispatch a Livewire event directly in the browser.
- `$event`: access the JavaScript event object from the listener.

Magic actions can also be called from Alpine through `$wire`, such as `$wire.$refresh()`.

## Action-Related `$wire` API
The Livewire JavaScript docs list these `$wire` action-related APIs:

- Public component methods are exposed and callable on `$wire`.
- `$wire.$parent` accesses the parent component's `$wire` object if one exists.
- `$wire.$get(name)` gets a property by name.
- `$wire.$set(name, value, live = true)` sets a property by name.
- `$wire.$toggle(name, live = true)` toggles a boolean property.
- `$wire.$call(method, ...params)` calls a method.
- `$wire.$js(name, callback)` defines a JavaScript action.
- `$wire.$js.actionName = () => { ... }` is also documented for defining a JavaScript action.
- `$wire.$island(name, options = {})` scopes the next action to a named island.
- `$wire.$refresh()` refreshes a component by sending a message to the server and re-rendering HTML.
- `$wire.$commit()` is documented as an alias for `$refresh()`.
- `$wire.$on(event, callback)` listens for an event dispatched from the component or its children.
- `$wire.$hook(name, callback)` listens for a lifecycle hook from the component or request.
- `$wire.$dispatch(event, params = {})` dispatches an event from this component.
- `$wire.$dispatchTo(otherComponentName, event, params = {})` dispatches an event to another component.
- `$wire.$dispatchSelf(event, params = {})` dispatches an event onto this component and no others.
- `$wire.intercept(...)` registers an action interceptor for the component instance.
- `$wire.interceptAction(...)` is documented as an alias for `intercept`.
- `$wire.interceptMessage(...)` registers a message interceptor.
- `$wire.interceptRequest(...)` registers a request interceptor.