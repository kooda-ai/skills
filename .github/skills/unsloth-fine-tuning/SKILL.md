---
name: unsloth-fine-tuning
description: 'Use when: working with Unsloth fine-tuning, LoRA, QLoRA, SFT, RL, datasets, chat templates, training hyperparameters, Unsloth Studio, notebooks, vLLM export, or Modal-based Unsloth finetuning. Requires current Unsloth docs before adding details, and Modal docs for Modal-specific infrastructure.'
argument-hint: 'Unsloth training topic, dataset format, LoRA setting, notebook path, export target, or Modal finetuning task'
---

# Unsloth Fine-Tuning

## Purpose
Use this skill for documented Unsloth fine-tuning workflows, dataset preparation, LoRA or QLoRA tuning, notebook-first usage, Studio setup, export or deployment paths, and the documented Modal example for Unsloth finetuning.

## Source Rule
1. Before giving final training, dataset, hyperparameter, install, or deployment guidance, query current Unsloth docs for the exact topic.
2. If the task is specifically about running Unsloth on Modal, also query current Modal docs for the exact infrastructure surface.
3. Do not add training methods, parameter recommendations, install commands, export methods, model support claims, or Modal infrastructure details unless they appear in the current docs or the reference files below.
4. Keep Unsloth-core guidance separate from Modal infrastructure guidance. Do not present Modal behavior as if it were Unsloth behavior.
5. If a task needs deeper framework details from `transformers`, `trl`, `peft`, `wandb`, or vLLM beyond what Unsloth documents, say that clearly and query those docs separately if needed.

## Reference Map
- Installation, notebooks, Studio, supported training surfaces, and training method selection: [core-workflows-and-setup.md](./references/core-workflows-and-setup.md)
- Dataset formats, chat templates, synthetic data, and LoRA or QLoRA hyperparameter guidance: [datasets-and-hyperparameters.md](./references/datasets-and-hyperparameters.md)
- Modal-based Unsloth finetuning and documented export or vLLM deployment paths: [modal-and-deployment.md](./references/modal-and-deployment.md)

## Related Skills
- Use `modal-platform` for broader Modal questions outside the Unsloth training surface.
- Use `modal-web-endpoints` when the task becomes a serving question rather than a training question.
- Use `modal-storage-primitives` when the main issue is Volume, Secret, or cache behavior around training artifacts.

## Workflow
1. Identify whether the task is install and setup, choosing a training method, dataset preparation, LoRA or QLoRA tuning, notebook selection, Studio usage, Modal execution, or deployment after fine-tuning.
2. Query current Unsloth docs for the exact topic first.
3. If the user is training or deploying on Modal, query Modal docs for the exact infrastructure topic as well.
4. Load the closest reference file from the map above.
5. Preserve documented names exactly, including `FastLanguageModel`, `standardize_sharegpt`, `get_chat_template`, `train_on_responses_only`, `SFTTrainer`, `save_pretrained_merged`, and any documented Modal decorators or objects.
6. Keep training method boundaries explicit: SFT versus RL, LoRA versus QLoRA versus full fine-tuning, notebook workflows versus local installation, and local inference versus vLLM deployment.
7. For datasets, verify the expected format before suggesting transformations. Do not assume ChatML, ShareGPT, Alpaca, or multimodal formats are interchangeable.
8. For hyperparameters, keep Unsloth defaults and recommendations close to the documented ranges instead of inventing new heuristics.
9. For Modal-based training, keep image setup, volumes, retries, GPUs, and secrets inside the Modal boundary and the training logic inside the Unsloth boundary.
10. Finish by checking that every install command, hyperparameter recommendation, export path, and infrastructure statement is traceable to current docs.

## Confirmed Core Patterns
- Unsloth documents both Unsloth Studio and code-based Unsloth Core installation paths.
- The docs present notebooks as a primary getting-started path for beginners.
- Unsloth documents SFT, RL, LoRA, QLoRA, full fine-tuning, pretraining, and multiple modality-specific surfaces.
- Dataset formatting and chat templates are first-class parts of the documented workflow.
- Unsloth documents saving adapters and merged models for later deployment, including vLLM.
- Modal has a documented Unsloth finetuning example with custom images, volumes, retries, a GPU selection, and an `@app.function` training entry.

## Completion Check
- A fresh docs lookup was used for the exact Unsloth topic.
- For Modal-backed flows, a fresh Modal docs lookup was also used for the infrastructure parts.
- Every install command, training method, dataset format, hyperparameter note, export method, and Modal setup claim is traceable to current docs or the reference files.
- Unsloth guidance and Modal infrastructure guidance are kept clearly separated.