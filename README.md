# Lumen models

The on-device models [Lumen](https://github.com/05Narwhal/lumen) (JL Studios) downloads on first launch. Lumen fetches the files attached to the `models-v1` release and checks each against the SHA-256 compiled into the app before it uses it. The download sends nothing but the request itself.

This repository contains no code: just this README and the release files.


## clip-vit-b32-image-fp16.onnx — `clip-vit-b32-fp16@1`

- **What:** the image tower of OpenAI CLIP ViT-B/32, exported through OpenCLIP 2.26.1, weights in fp16.
- **Source:** OpenAI CLIP weights (https://github.com/openai/CLIP), checkpoint SHA-256 40d365715913c9da98579312b702a82c18be219cc2a73407c4526f58eba950af.
- **Licence:** MIT (OpenAI CLIP). OpenCLIP (export tooling): MIT.
- **SHA-256:** 0e08a2484ca1a1a5bc12cfd31f6cc6e8744c919bd6a132400d7cbcb8f44deeb1 · 176,214,230 bytes.
- **Used for:** one 512-d embedding per photo (memory curation, slideshow grouping, transitions, music mood).
- **Why fp16:** dynamic int8 moved embeddings to cosine 0.970 of fp32 — too far for thresholds at 0.85 and 0.96.

## Aesthetic head (inside models.json, no file)

- **What:** LAION aesthetic predictor linear head for CLIP ViT-B/32, `sa_0_4_vit_b_32_linear.pth` (512 weights + bias).
- **Source:** https://github.com/LAION-AI/aesthetic-predictor · **Licence:** MIT.

## Prototypes (`src-tauri/crates/photos-ml/prototypes.json`)

- Fixed phrases embedded offline with the same CLIP model's text tower. Derived data; MIT as above.

## beat-this-small.onnx — `beat-this-small@1`

- **What:** the `small0` checkpoint of *Beat This!* (Foscarin, Schlüter, Widmer, ISMIR 2024), beat and downbeat activations (sigmoid applied in the export).
- **Source:** https://github.com/CPJKU/beat_this · checkpoint https://cloud.cp.jku.at/public.php/dav/files/7ik4RrBKTS273gp/small0.ckpt
- **Licence:** MIT. The README: "The code and the published model weights are released under the MIT license. Note that some of the training files are fully copyrighted or under limited Creative Commons licenses, and it is up to the user to assess whether this may impact their use case." Lumen ships the weights only, never training data; the weights' own licence is MIT, which passes ML design §2.8.
- **SHA-256:** 8ce9ac22967ff53551f5f319ff11c2e442fc5c9b372205c13f3ff786b56c998c · 9,274,894 bytes.
- **Verdict (2026-09-22):** shipped. ONNX output matches PyTorch within 2.2e-6 on the reference signal.

## Excluded

- **madmom** beat/downbeat weights: CC BY-NC-SA (non-commercial) — fails §2.8.
