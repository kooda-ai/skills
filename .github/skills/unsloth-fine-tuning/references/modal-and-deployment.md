# Modal And Deployment

## Modal Example Scope
- Modal documents an example called Efficient LLM Finetuning with Unsloth.
- The example presents Unsloth finetuning on Modal using a single GPU, custom image setup, Volumes, retries, and a CLI-driven local entrypoint.

## Image And Import Setup
- The Modal example builds a custom Debian-based image and installs `accelerate`, `datasets`, `hf-transfer`, `huggingface_hub`, `peft`, `transformers`, `trl`, `unsloth[cu128-torch270]`, `unsloth_zoo`, and `wandb`.
- The example sets `HF_HOME` to `/model_cache`.
- The example explicitly imports `unsloth` before `transformers`, `peft`, and `trl` so that Unsloth patches are applied first.

## Volume And Cache Setup
- The example uses separate Volumes for pretrained model cache, dataset cache, and checkpoints.
- The docs describe the cache volumes as reusable across experiments.
- Processed datasets are cached and committed back to the dataset cache Volume.

## GPU And Execution Setup
- The example uses `L40S` as its documented GPU choice.
- The example sets a timeout and configures retries using `modal.Retries(...)`.
- The training function is documented with `single_use_containers=True` to get a fresh container on retry.
- A `wandb-secret` is attached through `modal.Secret.from_name(...)`.

## Training Flow On Modal
- The Modal example uses `FastLanguageModel.from_pretrained(...)` to load the model.
- The example uses `standardize_sharegpt(...)` for dataset normalization.
- LoRA setup is done through `FastLanguageModel.get_peft_model(...)`.
- The training loop is built around `SFTTrainer` and `TrainingArguments`.
- The docs show checkpoint discovery and resume behavior before training.
- The example saves the final model and tokenizer into a checkpoint Volume path.

## CLI-Driven Local Entrypoint
- The example uses `@app.local_entrypoint()` so that arguments become CLI flags under `modal run`.
- The docs show running the example with:

```bash
modal run 06_gpu_and_ml/unsloth_finetune.py
```

- The docs also show tweaking hyperparameters directly via CLI flags such as `--max-steps`.

## Deployment After Fine-Tuning
- Unsloth's vLLM deployment guide documents `vllm serve` as a deployment path after fine-tuning.
- The guide documents `save_pretrained_merged(..., save_method="merged_16bit")` for vLLM-oriented export.
- It also documents saving only the LoRA adapters, either with `save_pretrained(...)` and `tokenizer.save_pretrained(...)` or through `save_pretrained_merged(..., save_method="lora")`.
- The guide documents `merged_4bit` export but explicitly discourages it unless the user understands the downstream use case.
- After export, the guide shows serving the fine-tuned model with `vllm serve finetuned_model`.

## Use This Reference For
- Running documented Unsloth fine-tuning on Modal.
- Keeping Modal infrastructure concerns separate from Unsloth training logic.
- Choosing a documented post-training export path for vLLM serving.