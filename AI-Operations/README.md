[⬅️ Back to Home](../README.md)
---
# AI Operations & Local inference 🧠: 

# Overview
This module serves to document the deployment and management of a local large langauge model (LLM) within the HobbitNet environment. By self hosting these models, I can ensure data sovereignity and stop any reliance on third party cloud providers, which helps me better align with my focus on data privacy. 

## Tech Stack 👨🏻‍💻: 
* **Inference Engine:** [Ollama](https://ollama.com/).
* Primary model: Gemma 3 12b (Latest generation state-of-the-art reasoning).
* Hardware Acceleration: NVIDIA CUDA (Currently running on the RTX 3070 8GB VRAM)

## Selecting my LLM model ⚖️: 
Choosing the right model for my rather limited 8gb vram card requires balancing the parameter count with available memory. I had benchmarked the following to find the sweet spot for my needs. 

### The contenders 
* **Llama 3.2 (3B):** This was my original consideration when I became initially intrigued by the idea of self hosting an LLM. i found this model to be great for speed and low-latency response, but lacked the reasoning depth for complex cybersecurity logs and other practices.
* **Gemma 2 (9B):** I had then shifted to looking into Gemma 2 due to my biased towards Google's Gemini model. I had found this model to be a strong creative performer, but it lacked the latest architectural improvements found in the 3.0 series.
* **Gemma 3 (12B):** I had ultimately landed and decided to run Gemma 3 12b, it offers the best logical reasoning and instruction following while utilizing the latest multimodal features.

> [!Note]
> **VRAM Optimization Strategy:** To achieve fluid inference with **Gemma 3 12b** on an **8GB RTX 3070**, I implemented two key optimizations:
> 1. **4-bit Quantization:** had reduced the model's memory footprint to fit within the GPU's VRAM limits.
> 2. **Context Tuning:** I capped the context window at **8k tokens** to prevent my VRAM from overflowing and to ensure the model remains entirely on the GPU for maximum speed.

## Implementation & Performance

### Remote inference architecture
As detailed in the [Networking folder](./Networking/), the Acer Predator (Linux Mint) submits prompts through a secure Tailscale tunnel.
* The offloading achievement: By successfully configuring Ollama's environment to listen on the Tailscale interface, I had successfully offloaded the heavy inference tasks from the laptop onto the windows host! 

## 🔗 Connectivity Verification
To verify that the secure tunnel and API binding were successful, I ran the following command from the **Linux** terminal:

```bash
curl http://[REDACTED_TAILSCALE_IP]:11434/api/tags
