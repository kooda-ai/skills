# Responses, JSON, Views, And Downloads

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x basic responses, custom response objects, JSON/JSONP responses, view responses, and downloads.

## Basic Route Responses
The docs show routes returning strings:

```php
Route::get('/', function () {
    return 'Hello World';
});
```

The docs show routes returning arrays, which Laravel automatically converts into JSON payloads:

```php
Route::get('/', function () {
    return [1, 2, 3];
});
```

## Custom Response Objects
The docs show returning a response with an explicit status code and header:

```php
Route::get('/home', function () {
    return response('Hello World', 200)
        ->header('Content-Type', 'text/plain');
});
```

Confirmed helpers and methods: `response(...)` and `header(...)`.

## JSON And JSONP Responses
The docs show `response()->json(...)`:

```php
return response()->json([
    'name' => 'Abigail',
    'state' => 'CA',
]);
```

The docs state this method automatically sets the `Content-Type` header to `application/json` and encodes the provided array.

The docs show creating a JSONP response with `withCallback(...)`:

```php
return response()
    ->json(['name' => 'Abigail', 'state' => 'CA'])
    ->withCallback($request->input('callback'));
```

Confirmed methods: `json(...)`, `withCallback(...)`, and `$request->input('callback')`.

## View Responses
The docs show generating a view response with status and headers:

```php
return response()
    ->view('hello', $data, 200)
    ->header('Content-Type', $type);
```

The docs also mention the global `view` helper for simpler cases. Run a narrower lookup before using concrete `view(...)` helper examples.

## Download Responses
The docs show download responses:

```php
return response()->download($pathToFile);

return response()->download($pathToFile, $name, $headers);
```

The docs state this response forces the user's browser to download a file and accepts the file path, optional filename, and optional HTTP headers. The docs also state the filename must be ASCII compatible.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using response cookies, redirects by route/action, binary file responses, inline file responses, streamed server responses, `streamJson`, `eventStream`, `streamDownload`, cache headers, response macros, status helper methods, or custom response classes.
