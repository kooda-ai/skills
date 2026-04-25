# Weak Spots to Recheck

These areas were intentionally kept cautious because Context7 results can be sparse or topic-specific.

- Custom login, registration, password reset, and email verification page examples: Context7 confirmed the general pattern and the custom profile page example, but re-query before naming base classes or writing full examples for non-profile auth pages.
- Tenant profile registration in panel configuration: `tenantRegistration()` was directly confirmed; re-query `tenantProfile()` before using it in final code.
- Tenant billing menu customization: re-query before using the `billing` array key, because Context7 returned it in the billing-specific result.
- Tenant security internals such as automatic association, `withoutGlobalScope(filament()->getTenancyScopeName())`, and custom tenant global-scope middleware: query narrowly before using these details.
- Any UserResource-specific implementation: use this skill for access/auth touchpoints, then load the Filament 5 Resources, Forms, Tables, or Actions skill for CRUD UI details.
