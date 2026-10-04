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
│   └── qwen3_qlora_colab.ipynb     step-by-step: train and evaluate on Google Colab
├── scripts/
│   └── train_qlora.py              the same pipeline as a command-line script (GPU server, e.g. AWS)
├── data/
│   ├── README.md                   format, counts, and how the data is generated
│   ├── questions_v1.yaml           the 120 questions with their correct labels (human-readable source)
│   ├── questions_v1_train.jsonl    training split — 375 examples from 109 questions
│   ├── questions_v1_val.jsonl      validation split — 38 examples from 11 questions
│   ├── questions_v1.md             every example laid out for reading
│   └── prompts/                    the system prompts, as the model sees them
└── requirements.txt                libraries for scripts/train_qlora.py
```

## Quick start (Google Colab)

1. Click **Open in Colab** above.
2. *Runtime → Change runtime type → T4 GPU*.
3. Run the steps in order. Step 3 downloads this repository, so there is nothing to upload. Set `USE_DRIVE = True` there to keep checkpoints and results on Google Drive, so that training can resume after a disconnect.

The notebook tests the base model, trains the adapter, tests the fine-tuned model on the same validation examples, and prints a before/after table per task.

## Command line (GPU server)

```bash
pip install -r requirements.txt     # torch must already be installed (e.g. the AWS Deep Learning AMI)

python scripts/train_qlora.py prepare --train data/questions_v1_train.jsonl --val data/questions_v1_val.jsonl
python scripts/train_qlora.py eval    --val data/questions_v1_val.jsonl --tag base
python scripts/train_qlora.py train   --train data/questions_v1_train.jsonl --val data/questions_v1_val.jsonl --out adapters/qwen3-8b-v1
python scripts/train_qlora.py eval    --val data/questions_v1_val.jsonl --adapter adapters/qwen3-8b-v1 --tag tuned
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

Examples longer than 2,048 tokens would be skipped rather than truncated; in this dataset the longest is about 1,700 tokens.

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
