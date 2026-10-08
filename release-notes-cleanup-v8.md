# DictateSI cleanup model v8

**File:** `dictatesi-cleanup-v8-q4_k_m.gguf`  
**Size:** 986,048,480 bytes  
**SHA-256:** `76f0a8ac8f4cd10c529677242f00646f58e0c55082c919cf99075f55b02b46fa`

Verify a download: `shasum -a 256 dictatesi-cleanup-v8-q4_k_m.gguf`

## Provenance

- Base model: [Qwen/Qwen2.5-1.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct), revision `989aa7980e4cf806f80c7fef2b1adb7bc71aa306` (Apache-2.0).
- Method: LoRA (rank 8, every linear projection in all 28 layers, dropout 0.1) on 6,440 synthetic raw-dictation to clean-text pairs written in DictateSI's own prompt format; 1,300 iterations, AdamW, learning rate 5e-5, loss on the assistant turn only. Adapters fused into the base weights, exported to GGUF f16 with llama.cpp, quantized to Q4_K_M with an importance matrix computed from 400 training examples.
- What it learned: remove fillers, stutters, and false starts; write money, percentages, dates, times, dosages, and ages the standard way; apply spoken self-corrections; keep spoken shorthand whose magnitude was not said exactly as spoken; keep every name and figure exactly.

## Measured

Scored with DictateSI's evaluation harness through the app's real pipeline (same prompts, structure formatter, and content guard), greedy decoding.

- Primary set, 40 dictations: 37 exact matches. For comparison, the stock Qwen2.5-1.5B-Instruct Q4_K_M scores 12 exact (word error rate 0.138).
- Held-out set, 23 dictations written after the training data was finalized, including three paragraphs of 60 to 120 words: 18 exact matches.
- Release gate, both sets: zero invented or merged figures, zero lost names, zero leftover fillers or correction cues, zero dropped content.
- About 0.20 s per dictation on an Apple M5 Pro with Metal.

Seven earlier training runs were rejected by the same gate before this one passed.

## License

Apache License 2.0, as a derivative of Qwen2.5. See LICENSE and NOTICE in this repository.
