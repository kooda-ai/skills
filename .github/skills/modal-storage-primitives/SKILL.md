---
name: modal-storage-primitives
description: 'Use when: working with Modal Volumes, Volumes v2, Secrets, CloudBucketMount, Dict, Queue, Proxy, forward, volume commits and reloads, modal volume CLI, or storage and networking primitives documented by Modal. Requires Context7 /websites/modal docs before adding details.'
argument-hint: 'Modal volume, secret, data primitive, CLI workflow, or storage consistency task'
---

# Modal Storage And Primitives

## Purpose
Use this skill for documented Modal storage and primitive surfaces, especially Volumes, Secrets, and the reference-level data and networking primitives.

## Source Rule
1. Before giving final storage or primitive guidance, query Context7 for `/websites/modal` with the exact Volume, Secret, or primitive topic.
2. Do not add CLI commands, limits, commit or reload rules, beta status, or primitive behavior unless they appear in the current Modal docs.
3. Keep guide-level Volume and Secret workflows separate from API-reference summaries of lower-level primitives.
4. Keep examples close to documented `Volume.from_name`, `Secret.from_name`, CLI commands, and reference object names.

## Reference Map
- Volumes, Volumes v2, Secrets, CLI flows, commit and reload semantics, and reference-level data and networking primitives: [storage-and-primitives.md](./references/storage-and-primitives.md)

## Related Modal Skills
- Use `modal-platform` for broader Modal architecture, images, scaling, deployment, and routing.
- Use `modal-web-endpoints` when storage questions are incidental to an endpoint-serving task.
- Use `modal-sandboxes` when the primary issue is Sandbox lifecycle or runtime execution rather than attached storage behavior.

## Workflow
1. Identify whether the task is Volume creation, Volume consistency, Volumes v2, Secret injection, CLI usage, or choosing between lower-level primitives.
2. Run a narrow Context7 query for `/websites/modal`.
3. Load the reference file above.
4. Use documented Modal storage names and CLI commands exactly.
5. Keep `Volume`, `Secret`, `CloudBucketMount`, `Dict`, `Queue`, `Proxy`, and `forward` distinct instead of treating them as interchangeable storage.
6. Preserve exact commit, reload, and limit statements from the docs.
7. Omit storage behavior not confirmed by the Modal docs.

## Confirmed Core Patterns
- Modal Volumes are documented as a distributed file system with explicit commit and reload behavior.
- Secrets are documented as environment-variable injection surfaces created from the dashboard, CLI, or Python code.
- The API reference separately lists `CloudBucketMount`, `Dict`, `Queue`, `Proxy`, and `forward` as distinct primitives.
- Volumes v2 are documented as Beta with different scale and consistency characteristics from v1.

## Completion Check
- A fresh Context7 lookup for `/websites/modal` was used for the exact storage or primitive topic.
- Every CLI command, limit, commit rule, beta note, and primitive name is traceable to the current Modal docs.
- Guide-level Volume or Secret behavior is not mixed with unrelated reference objects unless the docs explicitly connect them.