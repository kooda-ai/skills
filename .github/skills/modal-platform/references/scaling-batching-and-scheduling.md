# Scaling, Batching, And Scheduling

## Autoscaling Basics
- Every Modal Function corresponds to an autoscaling pool of containers.
- By default, Functions scale to zero when there are no inputs to process.
- The docs list these autoscaler settings on `@app.function` and `@app.cls`: `max_containers`, `min_containers`, `buffer_containers`, and `scaledown_window`.
- `Function.update_autoscaler()` is documented for dynamic updates without redeploying.
- For `modal.Cls`, the docs show `update_autoscaler()` on a parameterized instance controlling the pool for that specific parameter set.

## Parallel Invocation And Limits
- `Function.map()` runs many inputs roughly in parallel and preserves result ordering.
- `Function.starmap()` is documented for tuple-like argument sequences.
- `return_exceptions=True` on `.map()` aggregates exceptions instead of propagating them.
- The scaling guide documents these limits per function:
  - `2,000` pending inputs.
  - `25,000` total inputs.
  - Up to `1,000,000` pending inputs for `.spawn()` jobs.
  - At most `1000` concurrently processed inputs per `.map()` invocation.

## Batch Processing And Job Queues
- The batch-processing guide documents `.spawn_map()` as the fastest way to submit many jobs for background execution.
- The guide pairs `.spawn_map()` with `modal run --detach` for work that continues after submission.
- The docs recommend storing results externally for `.spawn_map()` workflows, such as in a Volume, Cloud Bucket Mount, or a database.
- The job-processing guide documents this queue pattern:
  1. Deploy the processing function with `modal deploy`.
  2. Submit work with `Function.spawn()`.
  3. Poll with `FunctionCall.get()`.
- The docs say `.spawn()` results remain accessible for up to 7 days after completion.
- `FunctionCall.from_id()` is the documented way to reconnect to a spawned call.

## Input Concurrency
- `@modal.concurrent(max_inputs=...)` enables one container to process multiple inputs at the same time.
- The guide says input concurrency is most useful for I/O-bound workloads and continuous batching scenarios.
- `target_inputs` is documented as an autoscaler target that allows burst behavior up to `max_inputs`.
- For synchronous functions, concurrent inputs run on separate threads, so the code must be thread-safe.
- For asynchronous functions, concurrent inputs run as separate `asyncio` tasks on a single thread and should not block the event loop.
- The guide says synchronous input cancellation raises `modal.exception.InputCancellation`, while async cancellation raises `asyncio.CancelledError`.
- For logging under concurrency, the docs recommend including a unique identifier such as `modal.current_input_id()`.

## Dynamic Batching
- `@modal.batched(max_batch_size=..., wait_ms=...)` accumulates individual calls and executes them in batches.
- The docs require batched function inputs to be lists, the return value to be a list, and all input and output list lengths to match.
- Batched `Cls` methods are supported, but the guide says a class with one batched method cannot also define other batched methods or regular Modal methods.
- The docs recommend setting `max_batch_size` to the largest batch the function can handle and `wait_ms` to the difference between targeted latency and execution time.

## Async Usage
- Modal documents async variants of its APIs through the `.aio` suffix.
- The async guide shows `await my_function.remote.aio(...)` and `asyncio.gather(...)` for arbitrary parallel execution patterns.
- The docs say blocking and async Modal functions can call each other.

## Scheduling
- The cron guide documents `modal.Period(...)` and `modal.Cron(...)` as schedule types.
- `Period` schedules run relative to deployment time and reset on redeploy.
- `Cron` is documented for fixed cron syntax schedules, with optional `timezone=` support.
- The docs say schedules cannot currently be paused. Instead the schedule should be removed and the app redeployed.
- Scheduled runs can be started manually from the app dashboard with the "run now" button.

## Cold Start Guidance
- The cold-start guide splits latency into queueing for warm containers and initialization work in freshly started containers.
- The docs list `scaledown_window`, `min_containers`, and `buffer_containers` as the warm-container controls.
- `scaledown_window` is documented as configurable from `2` seconds up to `20` minutes.
- The guide recommends moving one-time setup into global scope or `@modal.enter` methods.
- Memory Snapshots are documented as a separate feature for sharing initialization work across cold starts.

## Use This Reference For
- Distinguishing autoscaling from per-container concurrency.
- Choosing between `.map()`, `.spawn()`, `.spawn_map()`, `@modal.concurrent`, and `@modal.batched`.
- Verifying schedule behavior and cold-start controls.