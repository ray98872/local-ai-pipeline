# Local AI Asset Pipeline

A local-first pipeline for generating game assets — images, music and pixel art — running entirely
on a single **AMD Radeon RX 9070 XT**. No cloud, no API bills. This repo is the public write-up.

**Live page:** https://ray98872.github.io/local-ai-pipeline/

## Highlights

- **Three modalities, one GPU** — SDXL image generation, Stable Audio Open music, and AI pixel
  art, all served from the same Radeon
- **NVIDIA-targeted, AMD-powered** — the stack assumes CUDA; a launcher detects the GPU at startup
  and installs the matching PyTorch backend (**DirectML** for the Radeon on Windows), with CUDA,
  ROCm and CPU as automatic fallbacks
- **ComfyUI node graphs** — image generation is a wired graph: SDXL base → upscale → detail passes
  → refiner, built from nine custom node packs (Impact Pack, Ultimate SD Upscale, KJNodes, rgthree,
  Easy-Use, Essentials, LoRA Manager and more)
- **Generation inside Aseprite** — `aisprite`, a Flask server (`sd_server` on `127.0.0.1:5000`),
  loads SDXL via diffusers and serves sprites straight onto the canvas; two LoRAs
  (`Super_PixelArt_Sprite_XL`, `pixel_f2`) applied through peft keep the style consistent
- **Offline & free** — once weights are cached the pipeline needs no network, and there's no
  per-generation cost

## The stack

| Layer | Tools |
|---|---|
| Image | ComfyUI · SDXL base + refiner · CyberRealistic XL · custom checkpoints · VAE + text encoders |
| Detail & scale | Impact Pack · Ultimate SD Upscale · KJNodes · rgthree · Essentials · LoRA Manager · Easy-Use |
| Music | Stable Audio Open (prompt → KSampler → MP3) |
| Pixel art | aisprite (Flask + diffusers) · Aseprite plugin · pixel-art LoRAs (peft) |
| Backend | PyTorch + diffusers on DirectML / CUDA / ROCm / CPU |

## Files

- `index.html` — the standalone showcase page

The 30-second audio sample is served from the portfolio root (`/someaudioimade.mp3`),
so the clip lives in one place and is shared with the card on the main site.

---

Part of [ray98872](https://github.com/ray98872)'s portfolio.
