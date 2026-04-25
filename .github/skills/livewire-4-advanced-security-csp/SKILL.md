---
name: livewire-4-advanced-security-csp
description: 'Use when: working with Livewire 4 Security and CSP, public property tampering, #[Locked], Eloquent model property locking, validation, authorization, snapshot checksums, CorruptComponentPayloadException, csp_safe, CSP-safe mode, unsafe-eval, nonce, strict-dynamic, Alpine CSP limitations, and CSP troubleshooting. Requires Context7 Livewire 4.x docs before adding details.'
argument-hint: 'Livewire 4 public-property security, locked property, snapshot checksum, CSP-safe mode, or CSP troubleshooting concern'
---

# Livewire 4 Advanced Security CSP

## Purpose
Use this skill to create, review, or explain Livewire 4 security and Content Security Policy behavior using only details confirmed in the Livewire 4.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/livewire_laravel_4_x` with the exact Security, CSP, public property, locked property, snapshot checksum, Alpine CSP, or CSP troubleshooting topic.
2. Do not add security guarantees, attack claims, CSP headers, supported expression syntax, unsupported expression syntax, workaround patterns, performance claims, or testing steps unless they appear in the retrieved documentation.
3. If a requested security or CSP detail is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the detail out.
4. Preserve documented attribute names, exception names, configuration keys, header directives, directive values, method names, and example expressions exactly.
5. Do not infer behavior from generic Laravel security habits, Livewire 3, browser CSP references outside the Livewire docs, package source code, or memory.

## Covered Topics
- Public property tampering and validation or authorization
- `#[Locked]`
- Automatic Eloquent model property locking
- Snapshot checksums and `CorruptComponentPayloadException`
- Dehydrated state exposure concerns
- `config/livewire.php` `csp_safe`
- CSP-safe mode and Alpine impact
- Supported and unsupported CSP-safe expressions
- CSP header examples
- CSP testing and troubleshooting

## Workflow
1. Identify the concern: public property value, action parameter, model identifier, dehydrated model data, snapshot checksum, strict CSP header, `unsafe-eval`, Alpine expression, inline expression limitation, CSP workaround, or CSP violation.
2. Run a narrow Context7 query for the exact Livewire 4 security or CSP topic before producing code or review findings.
3. For public properties, treat values as client-controlled state and validate or authorize before persistence or sensitive operations when the docs require it.
4. Use `#[Locked]` only when the docs-confirmed task needs a public property protected from client-side modification.
5. For Eloquent public properties, include automatic locking only when the current docs confirm the exact behavior.
6. For dehydrated Eloquent values, mention exposed property names, model class names, model IDs, eager-loaded relationships, `Relation::morphMap()`, query-constraint limitations, large collection performance, or computed-property alternatives only when confirmed by the lookup.
7. For snapshots, explain checksum validation and `CorruptComponentPayloadException` only as documented.
8. For CSP-safe mode, set `'csp_safe' => true` in `config/livewire.php` only as documented.
9. State that CSP-safe mode affects Alpine.js only when the docs confirm the current task involves Alpine expressions.
10. For CSP headers, preserve the documented example shape: remove `'unsafe-eval'`, use nonce-based script loading with `'nonce-[random]'`, and consider `'strict-dynamic'` only as documented.
11. For supported CSP-safe syntax, use documented basic Livewire expressions, method calls with parameters, property access and updates, and basic Alpine expressions only.
12. For unsupported CSP-safe syntax, flag documented complex JavaScript expressions, template literals, advanced syntax, and dynamic property access only when relevant.
13. For CSP workarounds, move complex Alpine expressions into `Alpine.data()` or methods only as documented.
14. For CSP testing, use documented checks: enable CSP headers, inspect browser dev tools for CSP violations, verify expressions work, and check that no `unsafe-eval` violations appear.
15. Finish by checking that every security recommendation, attribute, exception, configuration key, CSP directive, expression rule, and troubleshooting step is traceable to the current Context7 result.

## Confirmed Core Patterns
- Public properties are accessible and modifiable on both the server and the client side.
- Public property values should be treated like request input before persistence or sensitive operations.
- `#[Locked]` prevents a public property from being modified on the client side.
- Livewire automatically locks public Eloquent model properties and ensures the ID is not changed.
- Livewire uses snapshot checksums to verify that browser-side snapshots have not been altered.
- A checksum mismatch throws `CorruptComponentPayloadException` and the request fails.
- Livewire offers a CSP-safe build for environments with strict Content Security Policy headers that prohibit `'unsafe-eval'`.
- CSP-safe mode is enabled with `'csp_safe' => true` in `config/livewire.php`.
- CSP-safe mode also affects Alpine.js functionality in the application.
- The docs show a CSP header example using `default-src 'self'; script-src 'nonce-[random]' 'strict-dynamic'; style-src 'self' 'unsafe-inline';`.

## Completion Check
- A fresh Context7 lookup for `/websites/livewire_laravel_4_x` was used for the exact security or CSP topic.
- No security guarantee, property-locking behavior, snapshot behavior, CSP header, CSP expression rule, workaround, performance note, or testing step absent from the retrieved Livewire 4.x docs was added.
- `#[Locked]`, `CorruptComponentPayloadException`, `'csp_safe'`, `'unsafe-eval'`, `'nonce-[random]'`, and `'strict-dynamic'` are spelled exactly as documented.
- CSP guidance separates documented supported syntax from documented unsupported syntax.
- Unconfirmed security assumptions are explicitly left out or followed by a narrower Context7 lookup.
