# DictateSI model files

This repository exists to host model files for [DictateSI](https://dictatesi.com),
the on-device dictation app for macOS. The files are attached to tagged
GitHub Releases; nothing of value lives in the repository tree itself.

## How the app uses these files

DictateSI downloads a model once, on first use, from a tagged release URL that
is compiled into the app together with the file's SHA-256. The download is
staged, hashed, and compared with the compiled-in value before it is installed;
a mismatch is deleted and never loaded. Releases here are therefore
append-only: a new model gets a new tag and a new filename, and an existing
asset is never replaced.

Each release's notes carry the file's SHA-256 so anyone can verify a download
by hand:

```
shasum -a 256 dictatesi-cleanup-v8-q4_k_m.gguf
```

## What the models are

- **Cleanup models** (`dictatesi-cleanup-*.gguf`): Qwen2.5-1.5B-Instruct,
  fine-tuned by DictateSI on synthetic raw-dictation to clean-text pairs so
  that it removes fillers and false starts, applies written conventions for
  money, dates, percentages, and dosages, keeps every name and figure exactly
  as spoken, and understands spoken self-corrections. Quantized to GGUF
  Q4_K_M for llama.cpp. Each release's notes state the measured results on
  DictateSI's evaluation sets and the base model revision it was trained from.

Speech recognition models (whisper.cpp) are not hosted here; the app downloads
them from the whisper.cpp project's own pinned revision.

## License

The cleanup models are derived from
[Qwen2.5-1.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct),
released by Alibaba Cloud under the Apache License 2.0. The fine-tuned weights
in this repository are likewise released under the Apache License 2.0; see
`LICENSE` and `NOTICE`. The DictateSI application itself is proprietary and is
not part of this repository.
