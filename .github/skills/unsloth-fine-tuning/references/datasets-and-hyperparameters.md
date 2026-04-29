# Datasets And Hyperparameters

## Dataset Basics
- The datasets guide says LLM datasets must be in a format that can be tokenized.
- The docs recommend deciding the dataset purpose, desired output style, and data source before formatting.
- The docs say dataset quality and quantity strongly affect the resulting fine-tune.

## Common Dataset Formats
- Continued pretraining is documented as raw text.
- Single-turn instruction tuning is documented with Alpaca-style `Instruction`, `Input`, and `Output` fields.
- Multi-turn conversation is documented with ShareGPT `from` and `value` pairs.
- The guide also documents ChatML-style `messages` with `user` and `assistant` roles.
- Vision fine-tuning is documented with multimodal message content containing text and image parts.

## Chat Templates And Formatting
- The docs show `CHAT_TEMPLATES` for listing supported chat templates.
- `get_chat_template(...)` is documented for applying the correct template to a tokenizer.
- `standardize_sharegpt(...)` is documented for converting ShareGPT-style datasets before formatting.
- The datasets guide shows applying `tokenizer.apply_chat_template(..., tokenize=False, add_generation_prompt=False)` during dataset mapping.
- The docs say Unsloth fixes chat template issues for its supported models and formats.

## Synthetic Data And Data Recipes
- The datasets guide documents Unsloth Data Recipes for turning PDFs, CSVs, and other files into usable datasets through Studio.
- The documented workflow is: create or open a recipe, add blocks, validate, preview sample output, then run a full dataset build.
- The docs also describe generating synthetic data with local LLMs or ChatGPT and recommend checking output quality carefully.

## Dataset Tips
- The guide recommends a bare minimum of about 100 rows for reasonable fine-tuning results, with more than 1,000 rows preferred for stronger performance.
- The docs say multiple datasets can be standardized and combined, or fine-tuned through a multiple-datasets notebook.
- The docs say repeatedly fine-tuning the same already fine-tuned model is possible, but combining datasets into a single fine-tune is generally better.

## Hyperparameter Guidance
- The LoRA hyperparameters guide documents a typical learning-rate range of `2e-4` to `5e-6`.
- For normal LoRA or QLoRA fine-tuning, the docs recommend `2e-4` as a starting point.
- The docs recommend `1-3` epochs for many instruction-based datasets.
- The guide states Effective Batch Size is `batch_size * gradient_accumulation_steps`.
- To avoid OOM, the docs recommend reducing `batch_size` and increasing `gradient_accumulation_steps` instead.
- The guide says Unsloth's gradient accumulation fixes make equivalent effective batch sizes align correctly.

## LoRA And QLoRA Details
- The docs suggest LoRA rank values such as `8`, `16`, `32`, `64`, or `128`, with `16` shown as a standard configuration.
- The documented target modules are `q_proj`, `k_proj`, `v_proj`, `o_proj`, `gate_proj`, `up_proj`, and `down_proj`.
- The guide recommends targeting both attention and MLP layers for best quality.
- The docs say `lora_alpha` equal to rank, or `2 * rank`, is a strong baseline.
- `lora_dropout = 0` is documented as optimized in Unsloth, though a non-zero value may help if overfitting is suspected.
- `bias = "none"` is documented as optimized.
- `use_gradient_checkpointing = "unsloth"` is documented as reducing memory usage further and helping with long-context fine-tuning.
- `use_rslora` and `loftq_config` are documented as advanced options.

## Training On Responses Only
- The guide documents `train_on_responses_only(...)` for training on assistant outputs only.
- The required `instruction_part` and `response_part` strings differ by model family.
- Vision models use equivalent response-only behavior through `UnslothVisionDataCollator` arguments.

## Overfitting And Underfitting
- The guide says training loss below `0.2` is a sign the model is likely overfitting.
- Documented overfitting mitigations include lowering learning rate, reducing epochs, increasing `weight_decay`, increasing `lora_dropout`, increasing batch size or gradient accumulation, expanding the dataset, and using evaluation-based early stopping.
- Documented underfitting mitigations include adjusting learning rate, training longer, increasing rank and alpha, using a more relevant dataset, and decreasing batch size to make updates more vigorous.

## Use This Reference For
- Choosing a documented dataset format.
- Applying Unsloth chat-template and ShareGPT conversion helpers.
- Verifying LoRA or QLoRA parameter ranges and documented tuning guidance.