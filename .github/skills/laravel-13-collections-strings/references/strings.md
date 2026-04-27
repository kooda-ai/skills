# Strings

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x string helpers and fluent string methods.

## Fluent Str Methods
The docs show importing `Illuminate\Support\Str` and using `Str::of(...)` for fluent string operations:

```php
use Illuminate\Support\Str;

$after = Str::of('This is my name')->after('This is');
$afterLast = Str::of('App\\Http\\Controllers\\Controller')->afterLast('\\');
$apa = Str::of('a nice title uses the correct case')->apa();
$append = Str::of('Taylor')->append(' Otwell');
$ascii = Str::of('ü')->ascii();
$basename = Str::of('/foo/bar/baz.jpg')->basename('.jpg');
$before = Str::of('This is my name')->before('my name');
$beforeLast = Str::of('This is my name')->beforeLast('is');
$between = Str::of('This is my name')->between('This', 'name');
$betweenFirst = Str::of('[a] bc [d]')->betweenFirst('[', ']');
$camel = Str::of('foo_bar')->camel();
$charAt = Str::of('This is my name.')->charAt(6);
$classBasename = Str::of('Foo\\Bar\\Baz')->classBasename();
```

Confirmed import: `Illuminate\Support\Str`.

## The str Helper
The docs state `str(...)` returns a new `Illuminate\Support\Stringable` instance for the given string and is equivalent to `Str::of(...)`.

The docs show:

```php
$string = str('Taylor')->append(' Otwell');

// Output:
// 'Taylor Otwell'
```

The docs state calling `str()` without an argument returns an instance of `Illuminate\Support\Str`.

The docs show:

```php
$snake = str()->snake('FooBar');

// Output:
// 'foo_bar'
```

## String Validation Methods
Context7 returned a string validation snippet with a malformed import. Run a narrower lookup before copying the import from that snippet.

The returned examples show these fluent validation methods:

```php
$isMatch = Str::of('foobar')->is('foo*');
$isAscii = Str::of('Taylor')->isAscii();
$isEmpty = Str::of('  ')->trim()->isEmpty();
$isJson = Str::of('[1,2,3]')->isJson();
$isUlid = Str::of('01gd6r360bp37zj17nxb55yv40')->isUlid();
$isUrl = Str::of('http://example.com')->isUrl(['http', 'https']);
$isUuid = Str::of('a0a2a2d2-0b87-4a18-83f2-2529882be2de')->isUuid(version: 4);
```

Confirmed methods from the returned examples: `is(...)`, `isAscii()`, `trim()`, `isEmpty()`, `isJson()`, `isUlid()`, `isUrl(...)`, and `isUuid(...)`.

## Str::chopEnd
The docs state `Str::chopEnd(...)` removes the last occurrence of the given value only if the value appears at the end of the string.

The docs list parameters `string` and `value`, where `value` may be a string or array.

The docs show:

```php
Str::chopEnd('app/Models/Photograph.php', '.php'); // 'app/Models/Photograph'
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using string helpers not listed here, including random strings, slugging, pluralization, casing methods not returned in the snippets, UUID or ULID generation, markdown helpers, word wrapping, fluent string macros, or exact return types beyond `Stringable` / `Str` statements returned for this slice.
