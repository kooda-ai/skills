# Navigation, URL State, And Redirects

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 navigation, redirect, persisted element, script evaluation, progress bar, or URL query parameter topic.

## `wire:navigate`
- Add `wire:navigate` to anchor tags to have Livewire intercept link clicks and navigate without a full page reload.
- The docs show `Route::livewire('/', 'pages::dashboard')`, `Route::livewire('/posts', 'pages::show-posts')`, and `Route::livewire('/users', 'pages::show-users')` as page routes used with `wire:navigate` links.
- When a `wire:navigate` link is clicked, Livewire prevents the browser's standard visit, requests the page in the background, shows a loading bar at the top of the page, and replaces the current page URL, `<title>`, and `<body>` with the new page.
- Use `wire:navigate.hover` to prefetch after a user has hovered over a link for `60` milliseconds.
- The docs warn that hover prefetching can increase server usage because not all hovered links are clicked.

## Redirects
- Use `$this->redirect('/posts')` inside a component action to redirect to another page.
- Livewire handles redirects on the frontend because Livewire requests are not standard full-page browser requests.
- Redirect to a full-page component route by using the route path, such as `$this->redirect('/posts')` for `Route::livewire('/posts', 'pages::show-posts')`.
- Use `return $this->redirect('/posts', navigate: true)` to load the redirected page with Livewire navigation instead of a full page request.
- Use `$this->redirectRoute('profile')` to redirect to a named route.
- Pass route parameters as the second argument to `redirectRoute`, such as `$this->redirectRoute('profile', ['id' => 1])`.
- Use `$this->redirectIntended('/default/url')`; the optional first argument is a fallback URL if no previous page can be determined.
- Use `$this->redirectAction([UserController::class, 'index'])` to redirect to a controller action, and pass parameters as the second argument.
- Use `session()->flash()` before redirecting when the redirected page should display Laravel session flash data.

## Active Links
- Livewire automatically adds a `data-current` attribute to any `wire:navigate` link that matches the current page.
- Style active links through the `data-current` attribute or Tailwind data attribute variants.
- Add `wire:current.ignore` to disable the automatic current-link behavior for a `wire:navigate` link.
- Use `wire:current="font-bold text-zinc-800"` to add CSS classes to the currently active link.
- The docs prefer `data-current` for simplicity because it does not require an additional directive and works with Tailwind data attribute variants.

## Persisted Elements And Scroll
- Use `@persist('name')` around matching elements on the current page and next page so Livewire reuses the existing DOM element during `wire:navigate` navigation.
- The docs show persisting an `<audio>` element with `@persist('player')`.
- The docs state that the persisted element must be placed outside Livewire components, commonly in the main layout such as `resources/views/layouts/app.blade.php`.
- By default, Livewire preserves the page scroll position when navigating back and forth between pages.
- Add `wire:navigate:scroll` to a persisted scroll container when the element's own scroll position should be preserved.

## JavaScript Navigation Hooks
- Each page navigation triggers `livewire:navigate`, `livewire:navigating`, and `livewire:navigated`.
- These events are dispatched for manual navigation using `Livewire.navigate()`, redirects with navigation enabled, and browser back and forward button presses.
- `livewire:navigate` can be cancelled with `event.preventDefault()`.
- The `livewire:navigate` event detail includes `url`, `history`, and `cached`.
- `livewire:navigating` runs when new HTML is about to be swapped onto the page and provides `e.detail.onSwap()`.
- `livewire:navigated` is the final step of navigation and is also triggered on page load instead of `DOMContentLoaded`.
- Document-level event listeners persist across pages; the docs show using `{ once: true }` to remove a listener after it runs.
- Call `Livewire.navigate('/new/url')` in JavaScript to manually visit a new page.

## Script Evaluation And Assets
- When using `wire:navigate`, `DOMContentLoaded` only fires on the first page visit; use `livewire:navigated` for code that should run on the initial page visit and after later Livewire navigations.
- Matching `<script>` tags in the `<head>` are loaded only on the initial page visit.
- New `<head>` scripts on later pages are evaluated before navigation completes.
- Body scripts are re-evaluated because Livewire replaces the entire `<body>` on every new page.
- Add `data-navigate-once` to a body script that should only run on the initial page visit.
- Add `data-navigate-track` to a `<script>` tag in the head so Livewire can trigger a full page reload when a tracked asset's query string changes.
- Laravel Vite asset tags receive `data-navigate-track` automatically in the documented example.
- Livewire only reloads for `[data-navigate-track]` when the element's query string changes, not when the URI itself changes.
- For Fathom Analytics, the docs show adding `data-spa="auto"` to the script tag so page visits are tracked during `wire:navigate` navigation.

## Navigation Progress Bar
- When a page takes longer than `150ms` to load, Livewire shows a progress bar at the top of the page.
- Configure the navigation progress bar in `config/livewire.php` with `'navigate' => ['show_progress_bar' => false, 'progress_bar_color' => '#2299dd']`.

## URL Query Parameters
- Add `#[Url]` from `Livewire\Attributes\Url` above a public property to sync it with the browser query string.
- URL query parameters are documented for state such as filtering, sorting, and pagination so visitors can share and bookmark specific page states.
- When a property uses `#[Url]`, Livewire stores updated values in the query string and initializes the property from existing query string values on page load.
- With `#[Url] public $search = ''`, typing `bob` can produce a URL such as `https://example.com/users?search=bob`.
- A nullable type hint such as `public ?string $search` makes an empty query string entry like `?search=` become `null` instead of an empty string.
- Use `#[Url(as: 'q')]` to change the query string key from the property name to an alias.
- Use `#[Url(except: '')]` to control which value is excluded from the query string.
- Use `#[Url(keep: true)]` to display a query string entry on page load even when the value is empty.
- Use `#[Url(history: true)]` to make Livewire use `history.pushState` instead of `history.replaceState` for query string updates.
- Define query string options with a protected `queryString()` method when dynamic options are needed.
- Trait query string hooks are documented with methods such as `queryStringWithSorting()` returning options for properties like `sortBy` and `sortDirection`.