# Core Workflows And Setup

## Product Scope
- Unsloth docs describe Unsloth as an open-source framework for running and training models.
- The docs say Unsloth supports local training, inference, data, and deployment workflows.
- Unsloth documents support for training and inference across many model families and modalities.

## Setup Paths
- The install docs say Unsloth can be used through Unsloth Studio, the web UI, or through Unsloth Core, the code-based version.
- The installation page shows these Studio install commands:

```bash
curl -fsSL https://unsloth.ai/install.sh | sh
```

```powershell
irm https://unsloth.ai/install.ps1 | iex
```

- The docs show Studio launch with:

```bash
unsloth studio -H 0.0.0.0 -p 8888
```

- The fine-tuning guide also documents local installation through Docker or `pip install unsloth`.

## Beginner Guidance
- The fine-tuning guide recommends beginners start with the pre-made notebooks first.
- The notebooks page documents Colab and Kaggle notebook catalogs for SFT, RL, vision, embedding, TTS, and other use cases.
- The notebooks page says users can run all, add their dataset, train, and deploy, and also save locally.

## Training Surfaces
- The fine-tuning guide documents these surfaces: Supervised Fine-Tuning, preference optimization methods, reinforcement learning methods, full fine-tuning, and pretraining.
- The docs recommend starting with a small instruct model and standard SFT for many use cases.
- The docs recommend starting with QLoRA as one of the most accessible and effective methods.

## Method Selection Notes
- LoRA is documented as a parameter-efficient method using added low-rank adapter weights in 16-bit precision.
- QLoRA is documented as combining LoRA with 4-bit precision to reduce memory usage.
- Full fine-tuning is documented as requiring significantly more resources and usually being unnecessary.
- The docs say only one training method should be enabled at a time.

## Running And Deploying After Training
- The fine-tuning guide says fine-tuned models can be run again through Unsloth itself for inference.
- The guide says saving and deployment can target engines such as Ollama, vLLM, and Open WebUI.
- The docs say a fine-tuned model may be saved as a LoRA adapter and can also be pushed to Hugging Face.

## Use This Reference For
- Choosing between Studio, notebooks, and code-based setup.
- Routing between SFT, RL, LoRA, QLoRA, and full fine-tuning.
- Verifying beginner-first Unsloth workflow guidance.