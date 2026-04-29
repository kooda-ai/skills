# Foundations And Deployment

## Product Scope
- Modal docs describe Modal as a serverless cloud and AI infrastructure platform for compute-intensive applications.
- The introduction says Modal supports low-latency inference, large-scale batch workflows, training or fine-tuning, secure Sandboxes for AI-generated code, and GPU-backed Notebooks.
- The guide says Modal takes your code, puts it in a container, and executes it in the cloud with automatic scaling.

## Language Support
- Python is the primary language for building Modal applications and implementing Modal Functions.
- The introduction also says JavaScript, TypeScript, and Go can call Modal Functions, run Sandboxes, and manage Modal resources.

## Getting Started
- The getting-started flow shown in the docs is:

```bash
pip install modal
modal setup
```

- The docs say that if `modal setup` does not work, `python -m modal setup` is an alternative.
- The introduction shows a minimal Python file that can be run with `modal run path/to/file.py`.

## Apps, Functions, And Clses
- `modal.App` represents an application running on Modal.
- Apps group one or more Functions for atomic deployment and act as a shared namespace.
- Functions and Clses are associated with an App.
- A deployed Function scales independently from other Functions and defaults to scale-to-zero when idle.

## Ephemeral Apps
- An ephemeral App is created by `modal run` or `app.run()`.
- Ephemeral Apps stop when the calling program exits or when the server detects the client is no longer connected.
- The docs say `--detach` can keep an ephemeral App running after the client exits.
- When using `app.run()` inside Python, the docs show `modal.enable_output()` as the way to surface Modal logs and progress output.

## Deployed Apps
- A deployed App is created with `modal deploy`.
- The docs say a deployed App persists until stopped in the web UI or with `modal app stop`.
- Functions in a deployed App run on a schedule only when they have an attached schedule. Otherwise they are invoked manually by web endpoints or Python lookup.
- Re-deploying an App with the same name updates it in place.

## Entrypoints
- `@app.local_entrypoint()` registers the local code that runs first under `modal run`.
- Primitive-typed entrypoint arguments are automatically parsed as CLI options.
- If the entrypoint or function accepts a variable-length argument list, Modal skips CLI parsing and forwards CLI arguments as strings.
- The docs show that `modal run script.py::app.f` can target a specific remote function when multiple entrypoints or functions exist.

## Naming Note
- The docs say `modal.Stub` was the previous name for `modal.App`.
- From Modal 1.0.0 onwards, using `modal.Stub` results in an error.

## Use This Reference For
- Explaining what Modal is and what it runs.
- Choosing between ephemeral and deployed execution.
- Verifying entrypoint behavior and core App terminology.