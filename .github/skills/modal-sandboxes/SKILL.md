---
name: modal-sandboxes
description: 'Use when: working with Modal Sandboxes, Sandbox.create, sandbox exec, readiness probes, named sandboxes, tagging, detached sandbox lifecycles, runtime command execution, or JavaScript and Go sandbox control. Requires Context7 /websites/modal docs before adding details.'
argument-hint: 'Modal sandbox lifecycle, probe, runtime command, lookup, naming, tagging, or JS/Go sandbox task'
---

# Modal Sandboxes

## Purpose
Use this skill for documented Modal Sandbox behavior, runtime command execution, readiness probes, lookup and naming patterns, and the JS or Go SDK surfaces that control Sandboxes.

## Source Rule
1. Before giving final Sandbox guidance, query Context7 for `/websites/modal` with the exact Sandbox topic.
2. Do not add lifetime limits, readiness behavior, naming rules, tagging behavior, or JS and Go SDK capabilities unless they appear in the current Modal docs.
3. If the task needs deeper shell-tool, OS, container-runtime, or framework behavior, say that clearly and keep the Modal-specific guidance separate.
4. Keep examples close to documented `Sandbox.create`, `exec`, `wait_until_ready`, lookup, and cleanup flows.

## Reference Map
- Sandboxes, readiness probes, lifecycle limits, naming, tagging, cleanup, and JS or Go SDK control: [sandboxes-and-cross-sdk.md](./references/sandboxes-and-cross-sdk.md)

## Related Modal Skills
- Use `modal-platform` for broad Modal routing, images, scaling, deployment, and cross-surface guidance.
- Use `modal-web-endpoints` when the task is primarily about HTTP exposure rather than isolated runtime execution.
- Use `modal-storage-primitives` when the main question is about attached Volumes, Secrets, or data primitives rather than Sandbox lifecycle behavior.

## Workflow
1. Identify whether the task is command execution, long-lived entrypoint startup, readiness probing, lookup by ID or name, tagging, or JS or Go SDK control.
2. Run a narrow Context7 query for `/websites/modal`.
3. Load the reference file above.
4. Use only the documented Sandbox lifecycle and lookup APIs.
5. Keep Sandbox object lifetime separate from process lifetime and command return codes.
6. Preserve exact timeout, naming, and beta-status statements from the docs.
7. Omit non-Modal container assumptions that the docs did not confirm.

## Confirmed Core Patterns
- Modal documents Sandboxes as secure containers for executing arbitrary or untrusted code at runtime.
- `Sandbox.create(...)` is the documented constructor, and Sandboxes created from outside Modal require an App.
- The docs include timeout and idle-timeout controls, readiness probes, entrypoint-style startup, lookup by ID or name, tagging, and explicit client cleanup with `detach()`.
- Modal documents JavaScript and Go SDKs as Beta and includes Sandbox control examples in both.

## Completion Check
- A fresh Context7 lookup for `/websites/modal` was used for the exact Sandbox topic.
- Every lifetime limit, probe rule, naming rule, and SDK claim is traceable to the current Modal docs.
- Non-Modal shell or container behavior is not invented beyond what the docs state.