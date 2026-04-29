---
name: modal-web-endpoints
description: 'Use when: working with Modal web endpoints, modal.fastapi_endpoint, modal.asgi_app, modal.wsgi_app, modal.web_server, WebSockets, deployed function invocation, endpoint auth, HTTPS exposure, or ASGI and WSGI app serving on Modal. Requires Context7 /websites/modal docs before adding details.'
argument-hint: 'Modal web endpoint, ASGI or WSGI app, invocation mode, auth pattern, or endpoint review task'
---

# Modal Web Endpoints

## Purpose
Use this skill for documented Modal web serving patterns, endpoint exposure, endpoint authentication, and invocation choices between Python lookup and HTTPS.

## Source Rule
1. Before giving final endpoint or invocation guidance, query Context7 for `/websites/modal` with the exact web or invocation topic.
2. Do not add decorators, request-body limits, WebSocket limits, auth headers, rate limits, or invocation behavior unless they appear in the current Modal docs.
3. If the task needs deeper FastAPI, Flask, Django, Starlette, or WebSocket framework behavior, say that clearly and query that product's docs separately.
4. Keep examples close to documented Modal decorators, CLI commands, and invocation flows.

## Reference Map
- Web endpoints, ASGI and WSGI apps, `@modal.web_server`, Python and HTTPS invocation, WebSockets, and auth: [endpoints-and-invocation.md](./references/endpoints-and-invocation.md)

## Related Modal Skills
- Use `modal-platform` for broader Modal architecture, images, scaling, scheduling, and cross-surface routing.
- Use `modal-sandboxes` when the task is really about runtime sandbox execution rather than HTTP exposure.
- Use `modal-storage-primitives` when the main question is about Volumes, Secrets, or storage primitives attached to an endpoint.

## Workflow
1. Identify whether the task is a simple FastAPI-backed endpoint, a full ASGI app, a WSGI app, a non-ASGI server, endpoint authentication, or deployed function invocation.
2. Run a narrow Context7 query for `/websites/modal`.
3. Load the reference file above.
4. Use only the documented Modal decorator for the chosen serving style: `@modal.fastapi_endpoint`, `@modal.asgi_app`, `@modal.wsgi_app`, or `@modal.web_server`.
5. Keep Python lookup of deployed functions separate from HTTPS invocation.
6. Preserve documented limits, header names, and beta or version notes exactly.
7. Omit framework-specific behavior not confirmed by the Modal docs.

## Confirmed Core Patterns
- `@modal.fastapi_endpoint` is the documented shortcut for exposing a Python function as a web endpoint.
- `@modal.asgi_app`, `@modal.wsgi_app`, and `@modal.web_server` are distinct Modal serving surfaces with different expectations about the returned app or bound port.
- `modal serve` is documented for ephemeral public endpoints with live updates, while `modal deploy` is documented for persistent deployed endpoints.
- Deployed functions can be invoked with Python lookup through `modal.Function.from_name(...)` or exposed to non-Python clients through HTTPS web endpoints.
- Web endpoint auth in the docs includes proxy auth tokens via `Modal-Key` and `Modal-Secret`, plus standard framework-level bearer-token validation using a `modal.Secret`.

## Completion Check
- A fresh Context7 lookup for `/websites/modal` was used for the exact web or invocation topic.
- Every decorator, limit, header name, CLI command, and invocation rule is traceable to the current Modal docs.
- FastAPI, Flask, Django, Starlette, or WebSocket framework behavior is not inferred beyond what the Modal docs explicitly state.