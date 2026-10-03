# Quran app models

Models for a free Quran app in development (iPhone, iPad, Mac and Android). The app isn't released yet.

## Khutbah captions: Arabic FastConformer, fine-tuned on Friday khutbahs (round 2)

Live Arabic captions of Friday khutbahs, recognised on the device.

- **Files** (release `khutbah-asr-r2`):
  - `model.int8.onnx`: 131,652,238 bytes, SHA-256 `05fda48e4bd229237573bda7f021d49de8e9967311a15162ca57ac0048b26357`
  - `vocab.txt`: 12,924 bytes, SHA-256 `b5d39b52143723e71d997ed5dd8a68aa5facbd0a7c84a47669f83b0033d33164`
- **Format:** int8 ONNX (CTC head), the same inputs, outputs and vocabulary as the ONNX export of NVIDIA's `stt_ar_fastconformer_hybrid_large_pc_v1.0`.
- **Base model:** [nvidia/stt_ar_fastconformer_hybrid_large_pc_v1.0](https://huggingface.co/nvidia/stt_ar_fastconformer_hybrid_large_pc_v1.0) by NVIDIA, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- **Changes:** this is a modified version. The CTC path was fine-tuned on about 25 hours of Friday khutbahs from Masjid al-Haram and al-Masjid an-Nabawi, then quantised to int8. The audio is public recordings, paired with the khutbahs' published texts.
- **Results:** word error rate, %, live captioning (8 s chunks, 2 s look-ahead), pooled over four held-out khutbahs:

| | clean | through a loudspeaker | heavy reverb |
|---|---|---|---|
| base model | 9.1 | 10.6 | 46.2 |
| this model | 8.2 | 10.5 | 31.1 |

On five held-out real khutbahs (first 20 minutes each): 14.2% for the base model, 11.5% for this one.

**Licence:** CC BY 4.0, as a modified version of NVIDIA's model. Credit NVIDIA for the base model.
