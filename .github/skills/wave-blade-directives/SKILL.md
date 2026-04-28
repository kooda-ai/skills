---
name: wave-blade-directives
description: 'Use when: working with Wave Blade directives such as @auth, @guest, @admin, @subscriber, @notsubscriber, @subscribed, @home, and documented directive usage in Wave views. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave Blade directive, subscriber check, admin check, or directive usage task'
---

# Wave Blade Directives

## Purpose
Use this skill for the Wave-specific Blade directives documented by Wave and for choosing the right documented directive in Wave views.

## Source Rule
1. Before giving final directive guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave directive topic.
2. Do not add directive names, argument behavior, or usage rules unless they appear in the current Wave docs.
3. If the task needs broader Blade behavior outside the Wave-specific directives, say that the Wave docs defer to Laravel Blade.
4. Keep examples close to documented directive names and usage patterns.

## Reference Map
- Documented Wave Blade directives and their usage boundaries: [wave-blade-directives.md](./references/wave-blade-directives.md)

## Related Wave Skills
- Use `wave-access-control-admin` when the directive question is really about roles, permissions, subscriber gating, or admin access rules.
- Use `wave-auth-users` when the task is about auth flows, profile pages, or user-facing account behavior rather than directive syntax.
- Use `wave-volt-pages` when the directive is being used inside a Wave theme page and the question depends on page routing or Volt structure.

## Workflow
1. Identify which documented directive is relevant: auth, guest, admin, subscriber, not-subscriber, subscribed-to-plan, or home-route checks.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only the documented directive names and documented argument expectations.
5. If the task moves beyond Wave’s custom directives, hand off to Laravel Blade documentation instead of inferring.
6. Omit anything not confirmed by the current Wave docs.

## Confirmed Core Patterns
- Wave documents `@auth`, `@guest`, `@admin`, `@subscriber`, `@notsubscriber`, `@subscribed('Plan Name')`, and `@home`.
- The docs say `@subscribed()` expects the full plan name.
- The docs say `@else` may be used with these directive conditions.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact directive topic.
- Every directive name, usage statement, and argument expectation is traceable to the current Wave docs.
- Broader Blade behavior is not inferred beyond what the Wave docs confirm.
