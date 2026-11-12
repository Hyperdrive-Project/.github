<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/Hyperdrive-Project/recipes/raw/main/assets/banner-dark.svg">
  <img src="https://github.com/Hyperdrive-Project/recipes/raw/main/assets/banner-light.svg" alt="Hyperdrive. Compute at warp speed. 7,264 tok/s per GPU on B300; 5.0x the stock model-card recipe on B200; 2.13x the stock vLLM recipe on DGX Spark; 84 ms to first token for Bolt voice." width="100%">
</picture>

Hyperdrive tunes open models to run faster, from datacenter GPUs to the machine on your desk. Each recipe takes one
model on one machine end to end: the serving engine, kernels, speculative decoding, batching and memory. It ships with
the configs, patches, benchmark protocol and quality gate, so anyone can check every number.

### Recipes

| Model | GPU | Engine | Result | vs baseline |
|---|---|---|---|---|
| [Nemotron 3.5 Super VL](https://github.com/Hyperdrive-Project/recipes/tree/main/nemotron-super-vl) | B300 | TensorRT-LLM | **7,264** tok/s per GPU, 160 users | **5.8x** the stock B200 recipe |
| | B200 | TensorRT-LLM | **6,280** tok/s per GPU | **5.0x** the stock model-card recipe |
| | B200 | SGLang | **3,705** tok/s per GPU | **+58%** vs cookbook defaults |
| | DGX Spark | TensorRT-LLM | **77.8** tok/s at 8 users | up to **2.13x** the stock vLLM recipe |
| [Nemotron 3.5 Bolt](https://github.com/Hyperdrive-Project/recipes/tree/main/bolt-flare-voice) | DGX Spark | Flare | **84 ms** to first token | **2.6x** faster for real-time voice |
| [Qwen3.8 Flash-Next](https://github.com/Hyperdrive-Project/recipes/tree/main/qwen-flash-next) | DGX Spark | vLLM | **49.8 / 25.7 / 16.2** tok/s at 4K / 50K / 100K | fastest full-quality entry in SparkBench PBM |

### How we work

- **Measured against a named baseline.** Every speedup names what it beats: a published recipe or the next full-quality leaderboard entry, on the same model and hardware.
- **Quality is a gate, not a footnote.** All experts, lossless speculation, and a reasoning-on math / code / tools
  check against the baseline. Where a recipe changes numerics (FP4 Mamba weights in v3, BF16 Mamba state in SGLang),
  it says so and passed the gate. For v3, a no-weight-change v2 ships alongside.
- **Built on open source, and giving back.** Our recipes sit on TensorRT-LLM, vLLM, SGLang, Flare and FlashInfer, and
  fixes we find go back upstream.
- **Reproducible from one clone.** Pinned images and revisions, unique prompts, and dates on every result.

Run it yourself, or let your coding agent do it:

```bash
git clone https://github.com/Hyperdrive-Project/recipes && cd recipes
./hyperdrive detect      # finds your GPU and the recipes for it
```

### Coming soon

- **FancyCake** · finds your GPU and model, then optimizes their kernels automatically. Its first kernel already ships in our Qwen recipe.
- **Hyperspeed** · video diffusion at warp speed: 4-5x faster than stock LTX-2.5 at 1080p on one RTX 5090.

⭐ Star [recipes](https://github.com/Hyperdrive-Project/recipes) to hear first.
