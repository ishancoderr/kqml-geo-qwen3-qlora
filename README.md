# kqml-geo-qwen3-qlora

QLoRA fine-tuning of Qwen3-8B for query classification, parameter extraction and PostGIS SQL generation in a KQML-based multi-agent system for retrieving missing geospatial data.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ishancoderr/kqml-geo-qwen3-qlora/blob/main/notebooks/qwen3_qlora_colab.ipynb)

This repository contains the data, notebook and script used to fine-tune **Qwen3-8B** with **QLoRA** (4-bit NF4 base weights + LoRA adapters) on a single NVIDIA T4 GPU. It is part of a master's thesis on multi-agent retrieval of missing geospatial data, where two agents ([Agent-001](https://github.com/ishancoderr/Agent-001), Agent-002) each hold part of the German federal states' demographic data and geometries and exchange what the other is missing over KQML.

## What the model learns

Each agent calls a language model three times. One fine-tuned model is trained on all three tasks together:

| Task | Input | Output |
|---|---|---|
| **classify** | the user's question | one of 8 categories, e.g. `{"query_type": "DIRECT_LOOKUP"}` |
| **extract** | the question + the category's prompt | its parameters: places, years, attributes, spatial relationship, … |
| **sql** | one retrieval step's parameters | one PostGIS `SELECT` with `:named` placeholders the agent binds |

The categories are DIRECT_LOOKUP, GEOMETRY_LOOKUP, SPATIAL_OPERATION, SPATIAL_ADJACENCY, SPATIAL_DIRECTION, SPATIAL_DISTANCE, SPATIAL_RELATIONSHIP_BUFFER and UNRELATED.

## Repository layout

```
├── notebooks/
│   ├── 01_eval_base_model.ipynb    test the base Qwen3-8B on the validation examples
│   ├── 02_train_qlora.ipynb        train the QLoRA adapter
│   ├── 03_eval_finetuned_model.ipynb  test base + adapter, compare with 01
│   └── qwen3_qlora_colab.ipynb     all of it in one notebook (version 1 data)
├── scripts/
│   └── train_qlora.py              the same pipeline as a command-line script (GPU server, e.g. AWS)
├── data/
│   ├── README.md                   format, counts, and how the data is generated
│   ├── questions_v3.yaml           version 3 (current): 347 questions with their correct labels
│   ├── questions_v3_train.jsonl    training split — 1,016 examples from 315 questions
│   ├── questions_v3_val.jsonl      validation split — 103 examples from 32 questions
│   ├── questions_v3.md             every example laid out for reading
│   ├── questions_v3_sql.md         only the SQL examples, grouped by SQL step — for checking the SQL
│   ├── prompts_v3/                 the 17 system prompts of version 3, as the model sees them
│   ├── questions_v2*, prompts_v2/  version 2 (332 questions), kept for reference
│   ├── questions_v1*, prompts_v1/  version 1 (120 questions), kept for reference
└── requirements.txt                libraries for scripts/train_qlora.py
```

## Quick start (Google Colab) — three notebooks

Run them in order, each in its own Colab session (*Runtime → Change runtime type → T4 GPU*). Each downloads this repository itself, so there is nothing to upload. Keep `DATA_VERSION = "v3"` and `USE_DRIVE = True` the same in all three — they find each other's outputs on Google Drive through them.

| | Notebook | Does | Writes to `MyDrive/kqml_finetune/` |
|---|---|---|---|
| 1 | [01 — base model](https://colab.research.google.com/github/ishancoderr/kqml-geo-qwen3-qlora/blob/main/notebooks/01_eval_base_model.ipynb) | plain Qwen3-8B answers the validation examples | `results/qwen3-8b-v3/eval_base.jsonl` |
| 2 | [02 — train](https://colab.research.google.com/github/ishancoderr/kqml-geo-qwen3-qlora/blob/main/notebooks/02_train_qlora.ipynb) | trains the LoRA adapter (2 epochs); resumes from the last epoch after a disconnect, and refuses to resume a checkpoint of a different run | `adapters/qwen3-8b-v3/`, `results/…/training_log.json` |
| 3 | [03 — fine-tuned model](https://colab.research.google.com/github/ishancoderr/kqml-geo-qwen3-qlora/blob/main/notebooks/03_eval_finetuned_model.ipynb) | base + adapter answers the same examples; table base vs. fine-tuned per task and category. `ADAPTER_FROM` tests one checkpoint instead | `results/qwen3-8b-v3/eval_tuned.jsonl` |

The two test notebooks save every answer as soon as it is made: after a disconnect, run the notebook again and it continues after the last saved answer. `LIMIT = 10` in their Step 4 makes a quick trial run first.

The single notebook `qwen3_qlora_colab.ipynb` does all three stages in one session, on the version 1 data.

## Command line (GPU server)

```bash
pip install -r requirements.txt     # torch must already be installed (e.g. the AWS Deep Learning AMI)

python scripts/train_qlora.py prepare --train data/questions_v3_train.jsonl --val data/questions_v3_val.jsonl
python scripts/train_qlora.py eval    --val data/questions_v3_val.jsonl --tag base
python scripts/train_qlora.py train   --train data/questions_v3_train.jsonl --val data/questions_v3_val.jsonl --out adapters/qwen3-8b-v3
python scripts/train_qlora.py eval    --val data/questions_v3_val.jsonl --adapter adapters/qwen3-8b-v3 --tag tuned
```

## Method

| Setting | Value | Why |
|---|---|---|
| Base model | `Qwen/Qwen3-8B` | Apache-2.0, fits a 16 GB T4 in 4-bit, answers directly with thinking turned off |
| Quantisation | 4-bit NF4, double quantisation | the "Q" in QLoRA |
| LoRA | rank 16, alpha 32, dropout 0.05, on all 7 linear layers | about 0.5% of parameters trainable |
| Training | 3 epochs, learning rate 2e-4, cosine schedule, effective batch 8 (1 × 8 accumulation) | small dataset; the epoch with the lowest validation loss is kept |
| Precision | float16 on a T4, bfloat16 on Ampere or newer | the T4 has no real bfloat16 |
| Prompt format | Qwen3 chat template, `enable_thinking=False` | identical prompt at training and inference |
| Loss | on the answer only, the prompt is masked | the model learns the answer, not to repeat the prompt |

Examples longer than 2,048 tokens would be skipped rather than truncated; in version 3 the longest is 1,830 tokens (counted with the Qwen3 tokenizer and chat template), so none is skipped.

## Evaluation

The base and the fine-tuned model answer every validation example with greedy decoding:

- **valid JSON** — the answer has the required output format;
- **correct** — classify and extract must equal the correct JSON exactly; SQL must equal the correct statement ignoring spacing and letter case.

The SQL check is strict: a correct statement written differently counts as wrong. Running the predicted SQL against the database is the stronger check.

## Results

*To be filled in after the first run.*

| Model | classify | extract | sql |
|---|---|---|---|
| Qwen3-8B (base) | | | |
| Qwen3-8B + QLoRA | | | |

## Notes

- The trained adapter (about 175 MB) is not stored in this repository: GitHub rejects files over 100 MB. Keep it on Google Drive or publish it on the Hugging Face Hub.
- The 20 scenario questions of the thesis's missingness specification are deliberately not in the training data; they are reserved for testing.
- The training data is generated by Agent-001 from its own prompts and schema; see [data/README.md](data/README.md).
