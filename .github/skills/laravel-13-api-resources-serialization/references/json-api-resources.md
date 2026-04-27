# JSON:API Resources

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x JSON:API resources and release notes.

## Generating JSON:API Resources
The docs show generating a JSON:API resource with the `make:resource` command and `--json-api` flag:

```shell
php artisan make:resource PostResource --json-api
```

The docs state the generated class extends `Illuminate\Http\Resources\JsonApi\JsonApiResource`.

## JSON:API Resource Class
The docs show a generated JSON:API resource class:

```php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Request;
use Illuminate\Http\Resources\JsonApi\JsonApiResource;

class PostResource extends JsonApiResource
{
    /**
     * The resource's attributes.
     */
    public $attributes = [
        // ...
    ];

    /**
     * The resource's relationships.
     */
    public $relationships = [
        // ...
    ];
}
```

Confirmed properties: `$attributes` and `$relationships`.

## JSON:API Behavior
The docs state Laravel provides `JsonApiResource` for creating responses that comply with the JSON:API specification.

The docs state `JsonApiResource` extends the standard `JsonResource`.

The docs state `JsonApiResource` automatically manages resource object structure, relationships, sparse fieldsets, and includes.

The docs state `JsonApiResource` sets the `Content-Type` header to `application/vnd.api+json`.

The Laravel 13 release notes state first-party JSON:API resources simplify compliant responses and mention object serialization, relationship inclusion, sparse fieldsets, link generation, and compliant response headers.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using concrete `$attributes` values, concrete `$relationships` values, relationship inclusion syntax, sparse fieldset request syntax, link generation APIs, compliant response examples, resource identifiers, pagination, errors, or JSON:API behavior beyond the documented summary here.
