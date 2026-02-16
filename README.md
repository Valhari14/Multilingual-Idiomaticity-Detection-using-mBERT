# Multilingual Idiomaticity Detection (SemEval-2022 Task 2A)

This repository contains baseline and ablation experiments for multilingual idiomaticity detection (SemEval-2022 Task 2A) using mBERT in zero-shot and one-shot settings.

## Contents

- `mBERT_ZeroShot.ipynb`: Zero-shot baseline (context: Previous + Target + Next).
- `mBERT_OneShot_Organized.ipynb`: One-shot baseline (Target sentence + MWE).
- `Ablation/`: Context and input-format ablations.
- `Data/`: Task data files.

## Task Overview

- **Task**: Binary classification of MWEs as idiomatic vs literal.
- **Languages**: English (EN) and Portuguese (PT) 
- **Settings**:
  - **Zero-shot**: MWEs in training do not appear in dev/test.
  - **One-shot**: One idiomatic and one literal example per MWE added to training.
- **Metrics**: Macro F1 / Macro Precision / Macro Recall.

## Data

Data files are in `Data/`:
- `train_zero_shot.csv`
- `train_one_shot.csv`
- `dev.csv`, `dev_gold.csv`

## Results Summary (Dev Set)

Macro-F1 scores (zero-shot vs one-shot):

| Slice | Zero-Shot | One-Shot |
| --- | --- | --- |
| English | 0.7102 | 0.8677 |
| Portuguese | 0.6213 | 0.8558 |
| Idiomatic | 0.6870 | 0.8627 |
| Literal | 0.7011 | 0.8717 |
| Overall | 0.6940 | 0.8672 |

Key observations:
- One-shot substantially improves over zero-shot, indicating that example-driven supervision is critical for idiomatic MWEs.
- Portuguese is weaker in zero-shot, consistent with lower data volume and higher morphological complexity.
- Full-context concatenation is not always beneficial; target-focused inputs and explicit MWE marking perform better in ablations.

## Setup

Recommended Python: 3.9+

Install dependencies (inside notebook or in terminal):

```
pip install torch transformers pandas scikit-learn sentencepiece datasets
```

## How to Run

1. **Zero-shot baseline**
   - Open `mBERT_ZeroShot.ipynb` and run all cells.
   - Set `CONTEXT_MODE` for ablations (FULL / TARGET_ONLY / TARGET_PREV / TARGET_NEXT).

2. **One-shot baseline**
   - Open `mBERT_OneShot_Organized.ipynb` and run all cells.
   - Control ablations with:
     - `CONTEXT_MODE` (NO_CONTEXT / WITH_CONTEXT)
     - `USE_SENTENCE2` (True/False)

3. **Ablation notebooks**
   - Each configuration has a dedicated notebook in `Ablation/`.


## Citation / Acknowledgements

- SemEval-2022 Task 2A: Multilingual Idiomaticity Detection
