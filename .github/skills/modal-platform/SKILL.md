---
name: modal-platform
description: 'Use when: working with Modal, modal.com, the Modal Python SDK, Apps, Functions, Cls, Images, GPUs, Volumes, Secrets, web endpoints, deployed function invocation, batch jobs, job queues, schedules, Sandboxes, or the JavaScript and Go SDKs. Requires Context7 /websites/modal docs before adding details.'
argument-hint: 'Modal topic, guide page, API surface, decorator, CLI flow, deployment pattern, or code review target'
---

# Modal Platform

## Purpose
Use this skill to create, review, or explain Modal using only details confirmed in the current Modal documentation.

## Source Rule
1. Before giving final code, commands, decorator usage, deployment advice, or review findings, query Context7 for `/websites/modal` with the exact Modal topic.
2. Do not add object names, decorators, CLI commands, environment variables, limits, beta status, authentication behavior, or SDK capabilities unless they appear in the current Modal docs or the reference files below.
3. Keep guide-level advice and API-reference facts separate. If a guide page gives workflow advice and the API reference gives object names, preserve that distinction instead of filling gaps from memory.
4. If the Modal docs defer to another project such as FastAPI, Flask, Django, Starlette, CUDA, or a model framework, say so clearly and only add those details after querying that product's current docs if the user asks for them.
5. Do not infer behavior from GitHub source, blog posts, older Modal releases, or generic serverless expectations when the current docs did not confirm it.

## Reference Map
- Product overview, getting started, Apps, entrypoints, ephemeral vs deployed execution: [foundations-and-deployment.md](./references/foundations-and-deployment.md)
- Images, container setup, CPU and memory requests, disk, and GPU selection: [images-resources-and-gpus.md](./references/images-resources-and-gpus.md)
- Autoscaling, `.map()`, `.spawn_map()`, job queues, `@modal.concurrent`, `@modal.batched`, async usage, schedules, and cold starts: [scaling-batching-and-scheduling.md](./references/scaling-batching-and-scheduling.md)
- Web endpoints, ASGI and WSGI apps, `@modal.web_server`, HTTPS and Python invocation, and endpoint auth: [web-endpoints-and-invocation.md](./references/web-endpoints-and-invocation.md)
- Volumes, Secrets, and reference-level data and networking primitives: [storage-secrets-and-data-primitives.md](./references/storage-secrets-and-data-primitives.md)
- Sandboxes, readiness probes, naming and tagging, JS and Go SDKs, and reference surface routing: [sandboxes-cross-sdk-and-reference.md](./references/sandboxes-cross-sdk-and-reference.md)

## Related Split Skills
- Use `modal-web-endpoints` for FastAPI-backed endpoints, ASGI or WSGI apps, `@modal.web_server`, deployed function invocation, HTTPS exposure, and endpoint authentication.
- Use `modal-sandboxes` for `modal.Sandbox`, readiness probes, runtime command execution, named sandboxes, tagging, and JS or Go sandbox control.
- Use `modal-storage-primitives` for Volumes, Secrets, `CloudBucketMount`, `Dict`, `Queue`, `Proxy`, and `forward`.
- Use `unsloth-fine-tuning` when the task is specifically about Unsloth training methods, datasets, LoRA or QLoRA choices, training hyperparameters, or documented Modal-based Unsloth finetuning flows.

## Workflow
1. Identify the Modal surface first: foundations, deployment, images, resources, GPUs, scaling, batching, scheduling, web endpoints, deployed invocation, storage, secrets, data primitives, sandboxes, or JS and Go SDK usage.
2. Run a narrow Context7 query for `/websites/modal` before producing code or review findings.
3. Prefer the closest split skill above when the request clearly fits one of those narrower surfaces; otherwise continue with this umbrella skill.
4. Load the closest reference file from the map above.
5. Preserve documented names exactly: `modal.App`, `@app.function`, `@app.cls`, `@modal.method`, `@modal.enter`, `@modal.exit`, `@modal.fastapi_endpoint`, `@modal.asgi_app`, `@modal.wsgi_app`, `@modal.web_server`, `@modal.concurrent`, `@modal.batched`, `modal.Period`, `modal.Cron`, `modal.Volume`, `modal.Secret`, and `modal.Sandbox`.
6. Keep execution mode distinctions explicit: ephemeral app vs deployed app, Python invocation vs HTTPS invocation, per-container concurrency vs horizontal autoscaling, and container image build steps vs runtime hooks.
7. For background work, distinguish `.map()`, `.spawn()`, `.spawn_map()`, and scheduled execution instead of collapsing them into one generic "job" pattern.
8. Finish by checking that every command, decorator, class, method, limit, and configuration claim is traceable to the current Modal docs context or the reference files.

## Confirmed Core Patterns
- Modal describes itself as a serverless cloud and AI infrastructure platform for compute-intensive applications.
- Python is the primary language for building Modal apps, while JavaScript, TypeScript, and Go can call Modal Functions, run Sandboxes, and manage Modal resources.
- `modal.App` is the deployment unit and namespace, while Functions and Clses scale independently.
- Modal docs separate simple web endpoints, ASGI apps, WSGI apps, non-ASGI web servers, Sandboxes, container Images, persistent storage, and data primitives into distinct surfaces.
- The API reference explicitly lists `App`, `Function`, `Cls`, `Sandbox`, `Image`, `Secret`, `Volume`, `CloudBucketMount`, `Dict`, `Queue`, `Proxy`, `forward`, `Period`, `Cron`, and related decorators.
- The guides distinguish horizontal autoscaling, per-container input concurrency, dynamic batching, background job submission, scheduled execution, and cold-start mitigation as different controls.
- Volume docs emphasize explicit commit and reload semantics, while Secrets are injected as environment variables.
- Sandbox docs present Sandboxes as secure containers for arbitrary or untrusted code execution with runtime configuration, probes, naming, and tagging.

## Completion Check
- A fresh Context7 lookup for `/websites/modal` was used for the exact Modal topic.
- Every command, decorator, object name, limit, beta label, and SDK statement is traceable to the current lookup or the reference files.
- Guidance keeps Modal surfaces separate instead of mixing deployment, web serving, async jobs, and sandbox execution.
- If a detail belongs to FastAPI, Flask, Django, CUDA, or another dependency rather than Modal itself, that handoff is stated clearly instead of being filled from memory.