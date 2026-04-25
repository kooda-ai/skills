# Completion Checklist

Use this checklist before giving final Filament 5 Users guidance.

- A fresh Context7 query was run against `/websites/filamentphp_5_x` for the exact Users subtopic.
- Every command, class, interface, trait, method, static property, parameter name, import, route slug, and security statement appears in the Context7 result or a loaded reference file that was built from Context7 results.
- The answer does not infer behavior from Filament 4.x, older docs, Laravel habits, package source code, or memory.
- Custom authentication page examples are limited to classes and snippets confirmed by the current lookup.
- Panel access (`FilamentUser`, `canAccessPanel()`) is not mixed up with Resource CRUD authorization policies.
- Tenancy answers mention the documented security risk before giving implementation details.
- Tenant-aware Resource advice is scoped to Users/tenancy touchpoints unless the Filament 5 Resources, Forms, Tables, or Actions skill has also been loaded.
- Guest access guidance removes auth-dependent panel components rather than leaving profile, avatars, or account widgets enabled.
- MFA guidance includes the relevant database columns, User model interfaces/traits, and `profile()` UI dependency when those are part of the task.
