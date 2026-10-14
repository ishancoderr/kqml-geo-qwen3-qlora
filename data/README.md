# Training data

Two versions are kept. **Version 2 is the current one**; version 1 stays for reference and for the single notebook `qwen3_qlora_colab.ipynb`.

## Files

| File | Content |
|---|---|
| `questions_v2.yaml` | The 332 questions: each with its category and correct extraction. The human-readable source of everything else. |
| `questions_v2_train.jsonl` | Training split: 975 examples from 301 questions |
| `questions_v2_val.jsonl` | Validation split: 101 examples from 31 questions (every 10th question of each group) |
| `questions_v2.md` | Every example laid out for reading: what the model sees and what it must answer |
| `prompts_v2/*.txt` | The 17 system prompts of version 2, written once each |
| `questions_v1*`, `prompts_v1/` | Version 1: 120 questions, 375 + 38 examples, 16 prompts |

Each JSONL line carries its full system prompt, so a data file never depends on the prompt folders — they are there for reading.

## One question becomes several examples

Each line of a JSONL file is **one call** the agent makes to the language model:

```
1 question → 1 classify example
           → 1 extract example                       (not for UNRELATED)
           → one SQL example per retrieval step       (not for UNRELATED or NEEDS_YEAR)
```

```json
{"messages": [
   {"role": "system",    "content": "<the prompt for this call>"},
   {"role": "user",      "content": "Query: How many residents did Brandenburg have in 2020?"},
   {"role": "assistant", "content": "{\"spatial\": [\"Brandenburg\"], \"temporal\": [2020], \"attributes\": [\"population\"], \"entity_type\": \"state\"}"}
 ],
 "meta": {"qid": "d10", "group": "data", "split": "val", "task": "extract", "category": "DIRECT_LOOKUP"}}
```

`meta` is used only to split and score the data; it is not part of what the model is trained on.

## Version 2 counts

| Group | Classify label | Questions |
|---|---|---|
| data | DIRECT_LOOKUP — incl. 7 without a year (must end as NEEDS_YEAR) and 6 combined totals ("combined population of X and Y") | 66 |
| geometry | GEOMETRY_LOOKUP | 51 |
| operation | SPATIAL_OPERATION — Union, Intersection, Difference, SymDifference, BufferWithin; 15 merge-then-cities, 4 merge-then-data | 70 |
| relationship | SPATIAL_ADJACENCY, SPATIAL_DIRECTION, SPATIAL_DISTANCE | 58 |
| delegation | SPATIAL_RELATIONSHIP_BUFFER — cities within N km, 8 cities inside a state, 8 cities in a direction | 62 |
| unrelated | UNRELATED | 25 |
| | **total** | **332** |

| Split | classify | extract | sql | total |
|---|---|---|---|---|
| train | 301 | 278 | 396 | 975 |
| val | 31 | 29 | 41 | 101 |

Longest example: 1,830 tokens (Qwen3 tokenizer, chat template, thinking off) — under the 2,048 limit, so none is skipped. Longest answer: 275 tokens.

Exact duplicates were removed (every "which states …" question fetches the same sixteen shapes), keeping training examples first, so no validation example repeats a training example and no question has examples in both splits.

## What version 2 adds over version 1

- 212 new questions, including edge cases at the end of every group;
- **combined totals** — the places' values added together, and a total only when every place has a value;
- **merge, then the merged area's data** (SPATIAL_OPERATION with attributes and years);
- **cities inside one state** (the zone search with distance 0) and **cities in a compass direction** of a place (a new SQL step, `sector`);
- direction sectors passed to SQL as bound values (`:az_start`, `:az_end`) instead of written into the prompt;
- the zone search's SQL step is asked a neutral question ("Which of our cities lie inside this zone?") rather than the user's wording.

## How the data is made

The files here are generated in the [Agent-001](https://github.com/ishancoderr/Agent-001) repository (branch `sql-writer`, folder `finetune/`), because generating them needs the agent's own code:

1. A person writes the questions and correct extractions in `questions_v2.yaml`, following [HOW_TO_WRITE_QUESTIONS.md](https://github.com/ishancoderr/Agent-001/blob/sql-writer/finetune/HOW_TO_WRITE_QUESTIONS.md) (format per category, naming rules, how to add questions). Drafted with Claude Code; to be reviewed by the thesis author.
2. `python -m finetune.build_examples finetune/questions_v2.yaml` derives every call the pipeline would make: the cleaned question text, the system prompts (from the agent's real prompt loaders) and the input of every SQL step. The correct SQL is generated from the agent's schema files and must pass the agent's SQL validator.
3. `python -m finetune.check_dataset finetune/questions_v2.jsonl` runs every label through the agent's own parser and SQL validator, and checks for duplicates, conflicting labels, outdated prompts and length.

To make a new version, edit the YAML in Agent-001, run both commands, and copy the outputs here. **The model learns the prompts exactly as they are** — when the agent's prompts change, the data must be rebuilt and the model trained again.

## Not in the training data

The unseen test questions (`test_set_v2.txt` in Agent-001) and the twenty scenario questions of the thesis's missingness specification are deliberately not here — they are for the final evaluation.

## Labels follow the agent's code

Where the thesis's scenario document and the code differ, the labels follow the code: `marriages` rather than `married`, tables `states` / `state_demographics`, and SQL with `:named` placeholders instead of literal values.
