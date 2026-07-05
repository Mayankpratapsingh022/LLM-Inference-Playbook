# LLM Inference Playbook

A hands-on series on making LLM inference faster. It covers the theory, the systems reality, and
runnable code you can reproduce on a single rented GPU for about a dollar.

Each part comes with a write-up and a companion notebook you can open on a
[RunPod](https://www.runpod.io/) pod and step through one cell at a time. The point is not to hand
you a benchmark number to trust. It is to show you how to measure your own, including the runs
where the optimization does not pay off.

This is an ongoing series. More parts and notebooks are on the way, so watch the repo if you want
new drops as they land.

## Parts

| # | Topic | Code | Status |
| --- | --- | --- | --- |
| 1 | Speculative Decoding: draft-and-verify, EAGLE, and deploying EAGLE3 on vLLM | [`speculative-decoding/`](./speculative-decoding) | Available |
| 2 | Coming soon | | Soon |
| 3 | Coming soon | | Soon |

Other topics planned for the series: KV-cache optimization, quantization, batching and scheduling,
paged attention, and continuous batching.

## Part 1: Speculative Decoding

Speculative decoding makes a large model generate several tokens per step instead of one, without
changing its output at all. Part 1 builds the idea from the ground up: why generation is
memory-bandwidth bound, how draft-and-verify works, why it is mathematically exact, and the alpha,
tau, and K economics that decide the speedup. It then walks the method families (n-gram, Medusa,
EAGLE) and deploys EAGLE3 on vLLM against a real baseline, including an honest result where it came
out slower, and why.

Notebook: [`speculative-decoding/speculative-decoding-vllm.ipynb`](./speculative-decoding/speculative-decoding-vllm.ipynb).
It serves `meta-llama/Llama-3.1-8B-Instruct` on a single 48 GB GPU, benchmarks baseline against
EAGLE3, and reads the speedup (and the acceptance length that predicts it) off your own hardware.

## How to run the notebooks

1. Rent a single 48 GB GPU pod on RunPod (A40, L40S, RTX 6000 Ada, or A6000).
2. Open the notebook inside the pod's JupyterLab.
3. Run it top to bottom, one cell at a time, reading along with the write-up.

Each notebook is self-contained and runs the exact commands from its post.

## About

Written by Mayank as the code companion to an LLM inference optimization blog series.
Questions, corrections, and contributions are welcome via issues.
