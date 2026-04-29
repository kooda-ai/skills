# Storage And Primitives

## Volumes
- The Volume guide describes Modal Volumes as a high-performance distributed file system for Modal applications.
- The easiest documented creation flow is `modal volume create NAME`.
- The guide says `Volume.from_name("name")` attaches an existing Volume, and `create_if_missing=True` creates it lazily from code.
- Attached Volumes are mounted at the path you provide in `volumes={...}`.
- `modal shell --volume ...` mounts Volumes under `/mnt`.
- The guide says Volumes are designed for up to `2.5 GB/s` bandwidth, though throughput is not guaranteed.

## Volume Access And CLI
- From local code, the docs show `vol.batch_upload()` with `put_file(...)` and `put_directory(...)`.
- The CLI subcommands shown in the docs include `cp`, `get`, `ls`, `put`, `rm`, `create`, `delete`, and `list`.
- The frontend supports downloading files up to `16 MB`; larger downloads should use the CLI.

## Commit And Reload Semantics
- The guide says Volume changes need to be committed to become visible outside the current container.
- Background commits happen every few seconds during execution, and a final commit is attempted at shutdown.
- A container sees the latest Volume state from mount time until `.reload()` is called.
- The docs show `.commit()` and `.reload()` as the explicit control points.

## Volume Performance And Consistency
- For v1 Volumes, the docs recommend keeping the file count under `50,000` and state a hard limit of `500,000` inodes.
- Concurrent modification of the same file should be avoided because last write wins.
- The docs recommend avoiding more than 5 concurrent commits for small v1 changes.
- During a reload, the Volume appears empty inside the container that initiated the reload.
- `.reload()` fails with a busy-volume error if files on the Volume are still open.
- Files written outside the mount path go to the container's local disk rather than the Volume.
- The docs say filesystem usage calls like `df` and `statfs` return placeholder values for Volumes.

## Volumes v2
- The docs mark Volumes v2 as Beta.
- `modal volume create --version=2` and `Volume.from_name(..., version=2)` are the documented creation paths.
- The v2 overview says commits and reloads are faster, total file count is unbounded, and many containers can write distinct files concurrently.
- For v2, the docs show `sync /path/to/mountpoint` as a way to persist changes from a Sandbox or shell.
- The docs say v2 is not yet recommended for mission-critical data.
- The v2 limits page documents a `1 TiB` maximum file size and `262,144` files per directory.

## Secrets
- Secrets can be created from the dashboard, the CLI, or Python code.
- `modal.Secret.from_name(...)` injects an existing Secret.
- `modal.Secret.from_dict(...)` creates an inline Secret from Python values.
- `modal.Secret.from_dotenv()` is documented when `python-dotenv` is installed.
- Multiple Secrets can be injected, and later Secrets overwrite earlier keys on collision.
- The CLI examples shown in the docs are `modal secret list`, `modal secret create`, and `modal secret delete`.
- Secret keys must contain only letters, digits, and underscores, cannot start with a digit, and can be up to `16,384` characters long.
- Secret values can be up to `32,768` characters long.

## Data And Networking Primitives From The API Reference
- `CloudBucketMount` is described in the API reference as storage backed by a third-party cloud bucket such as S3.
- `NetworkFileSystem` is described as shared writable cloud storage and marked as superseded by `modal.Volume`.
- `Dict` is described as a distributed key-value store.
- `Queue` is described as a distributed FIFO queue.
- `Proxy` is described as providing a static outbound IP address for containers.
- `forward` is described as a context manager for publicly exposing a port from a container.

## Use This Reference For
- Choosing between Volumes, Secrets, and reference-level storage primitives.
- Verifying commit and reload behavior.
- Confirming documented Volume v2 status and CLI workflows.