# All Bytes Are Equal, but Some Bytes Are More Equal Than Others: Multilingual Parity in the Byte Latent Transformer


Supplementary material for my Master's thesis *All Bytes Are Equal, but Some Bytes Are More Equal Than Others: Multilingual Parity in the Byte Latent Transformer* (Dominic Fischer, University of Zurich, 2026).

## Contents

| Folder | Content |
|---|---|
| `results/base_model/` | Per-byte entropies and patching premiums under the different approaches from BLT's original entropy model, 225 FLORES+ languages (Chapter 3) |
| `results/own_models/` | Per-byte entropies and patching premiums under the different approaches from the custom three entropy models, 20 languages (Chapter 4) |
| `models/` | Our three 10M entropy models: `imbalanced`, `balanced`, `balanced-custom` (weights in `consolidated/`, training config in `config.yaml`) |
| `training_setup/` | The 20 training languages (`langs_chosen.csv`) and the custom 2-byte encoding (`custom_encoding.json`) |
| `interactive_charts/` | Interactive versions of the thesis figures |
| `FLOPs_Analysis/` | Cost comparison Thai vs. English (Section 5.1) |

## Results files

The results files contain one JSON entry per FLORES+ sentence with the following keys:

- `id`, `text`, `text_en` (English equivalent), `n_bytes` (number of bytes).
- `bytes_entropies`: one triplet per byte, `[byte, entropy, normalised entropy]`.
  - The entropy is next-byte entropy in bits.
  - For `balanced-custom`, the bytes are the custom encoding, not UTF-8.
- `chars_entropies`: entropies summed per character.
- `eval_modes` / `char_eval_modes`: patch counts and lengths per patching mode and threshold, at byte and character level.

Premium = number of patches in a language ÷ number of patches in English.

## License

MIT (see `LICENSE`). The FLORES+ sentences in `results/` remain under CC BY-SA 4.0.
