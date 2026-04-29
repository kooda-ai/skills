# Images, Resources, And GPUs

## Images
- Modal code runs in containers, and Images are the filesystem snapshots those containers start from.
- By default, Modal Functions and Sandboxes run in a Debian Linux container with a basic Python installation matching the same local Python minor version.
- The docs present Image definition as method chaining from a base such as `modal.Image.debian_slim()`.

## Documented Image Customization Methods
- `Image.uv_pip_install(...)` is presented as the simplest and most common way to add Python packages.
- The docs recommend tightly pinning dependencies for reproducibility.
- `Image.pip_install(...)` is documented as a fallback if `uv_pip_install` causes issues.
- `Image.add_local_dir(...)` and `Image.add_local_file(...)` forward local files into the container.
- The docs say `copy=True` on `add_local_*` forces files into the built Image instead of startup-time injection.
- `Image.add_local_python_source(...)` is for locally importable pure Python project code, not third-party packages.
- `Image.imports()` is documented for imports that only exist in the remote environment.
- `Image.apt_install(...)` installs Linux packages.
- `Image.env(...)` sets environment variables.
- `Image.run_commands(...)` runs shell commands at build time.
- `Image.run_function(...)` runs Python code during image build and accepts the same kinds of runtime attachments documented for `@app.function`, including Volumes, Secrets, and GPU configuration.
- `Image.micromamba()` with `.micromamba_install(...)` is the documented mamba-based path.

## Image Build Notes
- The docs show that setup steps can request GPUs during build, for example on `pip_install(..., gpu="H100")`.
- Image caching is per layer, so changing one layer causes rebuilds for subsequent layers.
- `force_build=True` can be passed to image-building methods to force rebuilds.
- `MODAL_FORCE_BUILD=1` is documented for rebuilding all attached images.
- `MODAL_IGNORE_CACHE=1` is documented for rebuilding from the top without breaking the stored cache.
- The docs describe an Image Builder Version configured at the workspace level in Modal settings.

## CPU, Memory, And Disk
- Each Function or Sandbox container defaults to `0.125` CPU cores and `128` MiB of memory.
- `cpu` requests use floating-point physical cores, not vCPUs.
- The docs say Modal sets thread-count environment variables such as `OPENBLAS_NUM_THREADS`, `OMP_NUM_THREADS`, and `MKL_NUM_THREADS` based on the CPU request.
- `memory` requests use integer MiB values.
- CPU and memory can both be passed as `(request, limit)` tuples to configure soft or hard limits.
- `ephemeral_disk` is the documented way to request larger disk quotas.
- The docs say the per-container disk quota defaults to `512` GiB and can be raised up to `3.0` TiB.
- Disk billing is documented as increasing the memory request at a `20:1` ratio.

## GPU Configuration
- The GPU guide documents these request strings: `T4`, `L4`, `A10`, `L40S`, `A100`, `A100-40GB`, `A100-80GB`, `RTX-PRO-6000`, `H100`, `H100!`, `H200`, `B200`, and `B200+`.
- Multiple GPUs per container are requested by appending `:n`, such as `H100:8`.
- The docs say Modal supports GPU fallback lists, for example `gpu=["H100", "A100-40GB:2"]`.
- `gpu="H100"` may be automatically upgraded to an H200 unless `gpu=H100!` is used.
- `gpu="B200+"` allows Modal to run on either B200 or B300, and the docs say B300 requires CUDA `13.0+`.
- The guide notes that requesting more than two GPUs per container usually increases wait times.

## Use This Reference For
- Choosing between Image build methods.
- Verifying resource request syntax and default resource sizes.
- Confirming documented GPU strings, fallback behavior, and image rebuild controls.