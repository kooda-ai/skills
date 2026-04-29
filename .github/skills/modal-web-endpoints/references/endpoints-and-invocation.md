# Endpoints And Invocation

## Simple Endpoints
- `@modal.fastapi_endpoint` is the documented shortcut for turning a Python function into a web endpoint.
- The web-endpoints guide says this decorator was previously named `@modal.web_endpoint` before `v0.73.82`.
- The docs show `modal serve file.py` for ephemeral public endpoints with live updates when supporting files change.
- The docs show `modal deploy` for persistent deployed endpoints.

## FastAPI Semantics
- `@modal.fastapi_endpoint` wraps the function in a FastAPI application.
- The guide says the function's Image must have FastAPI installed.
- Query parameters are passed as function arguments.
- `method="POST"` can be used for JSON request bodies, and the docs recommend typed Pydantic models for validation and documentation.

## ASGI, WSGI, And Non-ASGI Servers
- `@modal.asgi_app()` is the documented path for returning an ASGI application.
- `@modal.wsgi_app()` is the documented path for returning a WSGI application.
- `@modal.web_server(port)` is documented for exposing a port from a process that speaks HTTP but does not expose an ASGI or WSGI app.
- The docs say `@modal.web_server` applications should bind to `0.0.0.0` rather than `127.0.0.1`.
- The ASGI section notes support for ASGI lifespan, though the docs recommend `@modal.enter` for container lifecycle hooks.

## Parametrized Endpoints
- Web endpoints can be parameterized through class syntax using `modal.parameter()`.
- The guide says parameter values are supplied in the endpoint URL as query parameters.

## WebSockets And Limits
- Functions exposed with `@modal.web_server`, `@modal.asgi_app`, or `@modal.wsgi_app` support WebSockets.
- The docs say Modal supports RFC 6455 WebSockets, but not RFC 8441 or RFC 7692.
- WebSocket messages can be up to `2` MiB each.
- The performance section says request bodies can be up to `4` GiB and response bodies are unlimited in size.
- The docs say new workspaces have a rate limit of `200` function inputs or web endpoint requests per second with a burst multiplier of 5 seconds, and excess web requests return `429`.

## Endpoint Authentication
- Modal docs say web endpoints can be protected with proxy auth tokens using the `Modal-Key` and `Modal-Secret` headers.
- The guide also documents standard bearer-token auth implemented in the web framework, with the token injected through a `modal.Secret`.
- The docs show `request.client.host` for reading the client IP address in FastAPI.

## Invoking Deployed Functions
- The invocation guide documents `modal.Function.from_name(app_name, function_name)` for Python lookup of deployed functions.
- Lifecycle-enabled classes are looked up with `modal.Cls.from_name(...)` and then constructed before calling a method.
- The same lookup path can use `.remote()`, `.map()`, and `.spawn()`.
- The docs say the Python SDK reads auth from `~/.modal.toml`, typically created with `modal token new`, or from `MODAL_TOKEN_ID` and `MODAL_TOKEN_SECRET`.

## Python Versus HTTPS Invocation
- The docs recommend Python invocation when the caller is already running Python.
- HTTPS invocation is documented as the path for browsers and non-Python clients, using deployed web endpoint URLs.
- The guide explicitly says JavaScript and Go callers should prefer the official SDKs rather than HTTPS when possible.

## Use This Reference For
- Choosing the correct web exposure decorator.
- Verifying endpoint limits and auth patterns.
- Distinguishing Python lookup of deployed functions from HTTPS invocation.