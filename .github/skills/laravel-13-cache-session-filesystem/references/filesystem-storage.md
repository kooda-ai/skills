# Filesystem Storage

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x filesystem storage.

## Storage Facade And Disks
The docs show using the `Storage` facade to store content on the default disk or a specific disk:

```php
use Illuminate\Support\Facades\Storage;

Storage::put('avatars/1', $content);
Storage::disk('s3')->put('avatars/1', $content);
```

Confirmed methods and disk names from this snippet: `Storage::put(...)`, `Storage::disk('s3')`, and `put(...)`.

## Storing Uploaded Files With Custom Names
The docs show storing an uploaded file with `storeAs(...)` on the request file object:

```php
$path = $request->file('avatar')->storeAs(
    'avatars', $request->user()->id
);
```

The docs show storing an uploaded file with `Storage::putFileAs(...)`:

```php
$path = Storage::putFileAs(
    'avatars', $request->file('avatar'), $request->user()->id
);
```

Confirmed methods: `$request->file('avatar')`, `storeAs(...)`, `$request->user()->id`, and `Storage::putFileAs(...)`.

## Public Disk
The docs state the `public` disk included in the application's `filesystems` configuration file is intended for publicly accessible files.

The docs state the `public` disk uses the `local` driver by default and stores files in `storage/app/public`.

If the public disk uses the local driver and files should be accessible from the web, the docs say to create a symbolic link from `storage/app/public` to `public/storage`.

## Storage Links
The docs confirm this command:

```shell
php artisan storage:link
```

The docs confirm destroying configured symbolic links with:

```shell
php artisan storage:unlink
```

The docs show additional symbolic links in the `links` array of the `filesystems` configuration file:

```php
'links' => [
    public_path('storage') => storage_path('app/public'),
    public_path('images') => storage_path('app/images'),
],
```

Confirmed helpers: `public_path(...)` and `storage_path(...)`.

## File URLs
The docs show generating a URL with the `Storage` facade:

```php
use Illuminate\Support\Facades\Storage;

$url = Storage::url('file.jpg');
```

The docs state local drivers return a path relative to storage and S3 returns a fully qualified remote URL.

After a file is stored and the symbolic link exists, the docs show creating a URL with the `asset` helper:

```php
echo asset('storage/file.txt');
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `Storage::get`, `exists`, `missing`, `delete`, `copy`, `move`, directories, file listings, visibility, temporary URLs, download responses from storage, scoped disks, read-only disks, S3 configuration, local disk configuration, file upload validation, testing fakes, or streaming files.
