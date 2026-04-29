# Sandboxes, Cross-SDK, And Reference Routing

## Sandboxes
- The guide describes Sandboxes as secure containers for executing arbitrary or untrusted code at runtime.
- Documented Sandbox use cases include running AI-generated code, isolating untrusted execution, checking out repositories and running commands, and creating arbitrary dependency environments.
- The Python guide shows `Sandbox.create(...)` as the constructor.

## App Association And Lifetime
- When created from outside a Modal container, a Sandbox requires an App.
- The docs show `modal.App.lookup(name, create_if_missing=True)` as a way to look up or create that App.
- Sandboxes default to a maximum lifetime of 5 minutes.
- `timeout=` on `Sandbox.create(...)` can be set up to 24 hours.
- The docs recommend Filesystem Snapshots for state preservation beyond 24 hours.

## Commands, Activity, And Return Codes
- `sb.exec(...)` runs commands inside the Sandbox.
- A Sandbox counts as active when it has a running command, receives stdin writes, or has an open TCP connection through a Tunnel.
- Unix-style exit codes are available on both the `ContainerProcess` and the Sandbox object itself.

## Readiness Probes
- The docs mark readiness probes as Beta.
- `modal.Probe.with_tcp(port)` is the documented probe for waiting on a listening server.
- `modal.Probe.with_exec(...)` is the documented probe for arbitrary readiness commands.
- `wait_until_ready()` blocks until the configured probe succeeds.
- Probe checks run for at most 5 minutes before `wait_until_ready()` raises `TimeoutError`.

## Runtime Configuration And Lookup
- The guide says Sandboxes support nearly all configuration options found on regular Functions.
- The docs show Images, Volumes, and Secrets on `Sandbox.create(...)`.
- A Sandbox can be created with an entrypoint command by passing command arguments directly to `Sandbox.create(...)`.
- `Sandbox.from_id(...)` reconnects to an existing Sandbox.
- Named Sandboxes are unique per deployed app while running, and `Sandbox.from_name(...)` looks up a running named Sandbox.
- Sandbox names may contain alphanumeric characters, dashes, periods, and underscores, and must be shorter than 64 characters.
- Sandboxes support arbitrary key-value tags and `Sandbox.list(...)` filtering.
- The guide recommends calling `.detach()` when the client is done interacting with a Sandbox.

## JavaScript And Go SDKs
- Modal documents JavaScript and Go SDKs as Beta.
- The JS and Go SDKs are documented for calling deployed Modal Functions, running Sandboxes, and interacting with resources such as Volumes, Secrets, and Queues.
- The docs say Python remains the primary language for defining Modal Functions.
- The JavaScript package is documented as `modal` on npm.
- The Go package is documented at `github.com/modal-labs/modal-client/go`.
- The docs point installation details to the JavaScript and Go READMEs.

## API Reference Surface Routing
- The API reference overview explicitly lists these construction and execution surfaces:
  - `App`, `App.function`, `App.cls`
  - `Function`, `Cls`
  - `parameter`, `enter`, `exit`, `method`
  - `fastapi_endpoint`, `asgi_app`, `wsgi_app`, `web_server`
  - `batched`, `concurrent`
  - `Cron`, `Period`, `Retries`
  - `Sandbox`, `ContainerProcess`, `FileIO`
  - `Image`, `Secret`
  - `Volume`, `CloudBucketMount`, `NetworkFileSystem`
  - `Dict`, `Queue`
  - `Proxy`, `forward`

## Use This Reference For
- Sandbox lifecycle, readiness, naming, lookup, and cleanup questions.
- Routing JS and Go SDK questions without inventing Python-only behavior.
- Quickly identifying which Modal object or decorator family a user is actually asking about.