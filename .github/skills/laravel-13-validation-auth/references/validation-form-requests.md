# Validation And Form Requests

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x validation and form request validation.

## Controller Validation
The docs show validating request data inside a controller with `$request->validate(...)`:

```php
/**
 * Store a new blog post.
 */
public function store(Request $request): RedirectResponse
{
    $validated = $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
    ]);

    // The blog post is valid...

    return redirect('/posts');
}
```

The docs state that if validation fails, a redirect or JSON response is automatically returned.

The docs also show array-based rule syntax:

```php
$validatedData = $request->validate([
    'title' => ['required', 'unique:posts', 'max:255'],
    'body' => ['required'],
]);
```

Confirmed rule examples from these snippets: `required`, `unique:posts`, and `max:255`.

## Form Request Generation
The docs confirm generating a form request directly:

```shell
php artisan make:request StorePostRequest
```

The docs state this command creates a custom form request class in `app/Http/Requests`.

The docs also confirm generating resource controller requests:

```shell
php artisan make:controller PhotoController --model=Photo --resource --requests
```

The docs state the `--requests` option creates `StorePhotoRequest` and `UpdatePhotoRequest` classes, or similar names based on the resource, in `app/Http/Requests`. The generated controller uses them for the `store` and `update` methods:

```php
use App\Http\Requests\StorePhotoRequest;
use App\Http\Requests\UpdatePhotoRequest;

// ...

public function store(StorePhotoRequest $request)
{
    // ...
}

public function update(UpdatePhotoRequest $request, Photo $photo)
{
    // ...
}
```

## Form Request Rules
The docs show a form request `rules()` method:

```php
/**
 * Get the validation rules that apply to the request.
 *
 * @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array<mixed>|string>
 */
public function rules(): array
{
    return [
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
    ];
}
```

## Custom Error Messages
The docs show overriding `messages()` to return custom error strings:

```php
/**
 * Get the error messages for the defined validation rules.
 *
 * @return array<string, string>
 */
public function messages(): array
{
    return [
        'title.required' => 'A title is required',
        'body.required' => 'A message is required',
    ];
}
```

## Type-Hinted Form Requests
The docs say injecting a form request into a controller method automatically triggers validation before the method body executes:

```php
/**
 * Store a new blog post.
 */
public function store(StorePostRequest $request): RedirectResponse
{
    // The incoming request is valid...

    // Retrieve the validated input data...
    $validated = $request->validated();

    // Retrieve a portion of the validated input data...
    $validated = $request->safe()->only(['name', 'email']);
    $validated = $request->safe()->except(['name', 'email']);

    // Store the blog post...

    return redirect('/posts');
}
```

Confirmed methods from this snippet: `validated()`, `safe()`, `only([...])`, and `except([...])`.

## Authorizing Form Requests
The docs state the `authorize` method within a form request determines if the authenticated user has permission to perform an action. The docs say this typically involves checking resource ownership or interacting with authorization gates and policies.

If `authorize` returns `false`, Laravel automatically returns a 403 HTTP response and prevents the controller method from executing.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using the `Validator` facade, named error bags, redirect customization, `after` validation hooks, custom attributes, custom rule objects, conditional validation, nested arrays, file validation, old input, localization, display of validation errors in Blade, JSON validation response shape, or validation rule names beyond those shown here.
