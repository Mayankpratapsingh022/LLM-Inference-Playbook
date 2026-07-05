# LLM Inference Playbook

A hands-on series on **making LLM inference faster** — the theory, the systems reality, and
runnable code you can reproduce on a single rented GPU for about a dollar.

Each part pairs a deeply illustrated write-up with a companion notebook you can open on a
[RunPod](https://www.runpod.io/) pod and step through cell by cell. The goal is not to hand you
a benchmark number to trust, but to teach you how to measure your own — including the runs where
the optimization *doesn't* pay off.

> 🚧 **This is an ongoing series.** More parts and notebooks are on the way. Star / watch the
> repo to get new drops as they land.

## Parts

| # | Topic | Code | Status |
| --- | --- | --- | --- |
| 1 | **Speculative Decoding** — draft-and-verify, EAGLE, and deploying EAGLE3 on vLLM | [`speculative-decoding/`](./speculative-decoding) | ✅ Available |
| 2 | Coming soon | | 🔜 Soon |
| 3 | Coming soon | | 🔜 Soon |

More topics planned across the series: KV-cache optimization, quantization, batching and
scheduling, paged attention, continuous batching, and other production inference tricks.

## Part 1 — Speculative Decoding

Speculative decoding makes a large model generate several tokens per step instead of one,
**without changing its output at all**. Part 1 builds the idea from the ground up (why generation
is memory-bandwidth bound, the draft-and-verify mechanism, why it's mathematically exact, and the
`alpha` / `tau` / `K` economics that decide the speedup), walks the method families
(n-gram, Medusa, EAGLE), and then actually deploys **EAGLE3 on vLLM** against a real baseline —
including an honest result where it came out *slower*, and why.

- 📓 Notebook: [`speculative-decoding/speculative-decoding-vllm.ipynb`](./speculative-decoding/speculative-decoding-vllm.ipynb)
- Serve `meta-llama/Llama-3.1-8B-Instruct` on a single 48 GB GPU, benchmark baseline vs EAGLE3,
  and read the speedup (and the acceptance length that predicts it) off your own hardware.

## How to run the notebooks

1. Rent a single **48 GB GPU** pod on RunPod (A40, L40S, RTX 6000 Ada, or A6000).
2. Open the notebook inside the pod's JupyterLab.
3. Run it top to bottom, one cell at a time, reading along with the write-up.

Each notebook is self-contained and runs the exact commands from its post.

## About

Written by Mayank as the code companion to an LLM inference optimization blog series.
Contributions, corrections, and questions are welcome via issues.
