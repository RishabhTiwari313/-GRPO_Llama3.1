# GRPO_Llama3.1
Dataset: openai/gsm8k
DeepSeek’s learning algorithm, GRPO (Group Relative Policy Optimization), is a reinforcement learning technique that optimizes responses efficiently without requiring a value function model. This reduces memory and computational costs compared to methods like PPO (Proximal Policy Optimization).

With 15GB VRAM, Unsloth allows you to transform any model up to 15B parameters like Llama 3.1 (8B), Phi-4 (14B), Mistral (7B) or Qwen2.5 (7B) into a reasoning model

Minimum requirement: Just  7GB VRAM is enough to train your own reasoning model locally.

Previous demonstrations show that you could achieve your own "aha" moment with Qwen2.5 (1.5B) - but it required 2xA100 GPUs (160GB VRAM). Now, with Unsloth, you can achieve the same "aha" moment using just a single 7GB VRAM GPU

Previously, GRPO was only supported for full fine-tuning, but we've made it work with QLoRA and LoRA

Please note, this isn’t fine-tuning DeepSeek’s R1 distilled models or using distilled data from R1 for tuning which Unsloth already supported. This is converting a standard model into a full-fledged reasoning model using GRPO.

How GRPO Works:
The model generates groups of responses.

Each response is scored based on correctness or another metric created by some set reward function rather than an LLM reward model.

The average score of the group is computed.

Each response's score is compared to the group average.

The model is reinforced to favor higher-scoring responses.

It’s advised to apply GRPO to a model at least 1.5B in parameters to correctly generate thinking tokens as smaller models may not. Our examples use Llama 3.1 (8B), Phi-4 (14B), Mistral (7B), and Qwen 2.5 (14B).

Training loss tracking for GRPO is now built directly into Unsloth, eliminating the need for external tools like wandb etc. If you’re using a base model, ensure you have a chat template.

