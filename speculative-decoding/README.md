# Part 1: Speculative Decoding

Part 1 of the [LLM Inference Playbook](../README.md).

Speculative decoding uses a small, fast draft model to guess the next few tokens and lets the large
target model verify them all in a single pass. Several tokens get accepted for the price of one
forward pass, and the output does not change at all.

## The notebook

[`speculative-decoding-vllm.ipynb`](./speculative-decoding-vllm.ipynb) deploys the production
method, EAGLE3, on vLLM and benchmarks it against a plain baseline:

- Target: `meta-llama/Llama-3.1-8B-Instruct`
- Hardware: a single 48 GB GPU (A40, L40S, RTX 6000 Ada, or A6000), `-tp 1`, no quantization
- What it does: serve baseline, benchmark, serve with EAGLE3, benchmark, compare
- What it measures: tokens/sec, acceptance length (tau), and latency percentiles

It reports the run honestly. On this small-model, single-GPU setup EAGLE3 came out slower
(tau = 1.81), and the notebook explains why. A small target on a fast GPU is the hard case for
speculation, and the acceptance length tells you so at a glance.

## Running it

1. Rent a single 48 GB GPU pod on [RunPod](https://www.runpod.io/).
2. Open this notebook in the pod's JupyterLab.
3. Run it top to bottom, one cell at a time.

You need a Hugging Face account with access to the gated Llama-3.1-8B model, so accept the license
on its model page first. The notebook logs in with `huggingface_hub.login()` when you run it, and
no token is stored in the file.
