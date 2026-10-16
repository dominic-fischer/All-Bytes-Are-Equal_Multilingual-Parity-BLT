# All Bytes Are Equal, but Some Bytes Are More Equal Than Others: Multilingual Parity in the Byte Latent Transformer

Supplementary material for my Master's thesis *All Bytes Are Equal, but Some Bytes Are More Equal Than Others: Multilingual Parity in the Byte Latent Transformer* (Dominic Fischer, University of Zurich, 2026).

## Contents

| Folder | Content |
|---|---|
| `results/base_model/` | Per-byte entropies and patch counts under the different patching approaches, from BLT's original entropy model, 225 FLORES+ languages (Chapter 3) |
| `results/own_models/` | Per-byte entropies and patch counts under the different patching approaches, from our three entropy models, 20 languages (Chapter 4) |
| `models/` | Our three 10M entropy models (weights in `consolidated/`, training config in `config.yaml`) |
| `training_setup/` | The 20 training languages (`langs_chosen.csv`) and the custom 2-byte encoding (`custom_encoding.json`) |
| `samples/` | Patching visualisations for one sentence in each of the 20 languages, for all four entropy models |
| `interactive_charts/` | Interactive versions of the thesis figures |
| `FLOPs_Analysis/` | Cost comparison Thai vs. English (Section 5.1) |

## Models

| Model | Training data | Encoding | Checkpoint (early stopping) |
|---|---|---|---|
| `imbalanced` | Language shares as found in FineWeb / FineWeb2 | UTF-8 | step 2600 |
| `balanced` | Equal information content per language | UTF-8 | step 7200 |
| `balanced-custom` | Equal information content per language | Random 2-byte code per character | step 6400 |

## Results files

The results files contain one JSON entry per FLORES+ sentence with the following keys:

- `id`, `text`, `text_en` (English equivalent), `n_bytes` (number of bytes).
- `bytes_entropies`: one triplet per byte, `[byte, entropy, normalised entropy]`.
  - The entropy is next-byte entropy in bits.
  - The normalised entropy is the per-sentence z-score: (entropy − mean) / std.
  - For `balanced-custom`, the bytes are the custom encoding, not UTF-8.
- `chars_entropies`: entropies summed per character.
- `eval_modes` / `char_eval_modes`: patch counts and lengths per patching mode and threshold, at byte and character level.

Premium = number of patches in a language ÷ number of patches in English.

## Samples

`samples/<model>/<lang>_0/` shows how the first FLORES+ sentence (`id` 0) is patched, for each of the 20 training languages and each of the four entropy models: `base_model`, `imbalanced`, `balanced` and `balanced-custom`. Only the anchor threshold of each patching mode is included, i.e. the threshold calibrated so that English reaches the same compression rate as under BLT's default threshold.

Each folder contains one HTML file per patching mode, showing the entropy curve, the threshold and the resulting patch boundaries. Character-level modes are in `char_level/` subfolders. Download the files and open them in a browser.

## Acknowledgements

The entropy models were trained and evaluated with the [BLT codebase](https://github.com/facebookresearch/blt) (Pagnoni et al., 2025), including its original patching functions. BLT is licensed under CC BY-NC 4.0.

## License

MIT (see `LICENSE`). The FLORES+ sentences in `results/` remain under CC BY-SA 4.0.