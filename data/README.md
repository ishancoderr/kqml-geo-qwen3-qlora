# Training data — version 1

## Files

| File | Content |
|---|---|
| `questions_v1.yaml` | The 120 questions: each with its category and correct extraction. The human-readable source of everything else. |
| `questions_v1_train.jsonl` | Training split: 375 examples from 109 questions |
| `questions_v1_val.jsonl` | Validation split: 38 examples from 11 questions (every 10th question of each group) |
| `questions_v1.md` | Every example laid out for reading: what the model sees and what it must answer |
| `prompts/*.txt` | The 16 system prompts, written once each |

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

## Counts

| Group | Classify label | Questions |
|---|---|---|
| data | DIRECT_LOOKUP (2 end as NEEDS_YEAR: no year given) | 22 |
| geometry | GEOMETRY_LOOKUP | 22 |
| operation | SPATIAL_OPERATION: Union, Intersection, Difference, SymDifference, BufferWithin | 22 |
| relationship | SPATIAL_ADJACENCY 8, SPATIAL_DIRECTION 8, SPATIAL_DISTANCE 6 | 22 |
| delegation | SPATIAL_RELATIONSHIP_BUFFER | 22 |
| unrelated | UNRELATED | 10 |

| Split | classify | extract | sql | total |
|---|---|---|---|---|
| train | 109 | 100 | 166 | 375 |
| val | 11 | 10 | 17 | 38 |

Exact duplicates were removed (every "which states …" question fetches the same sixteen shapes), keeping training examples first, so no validation example repeats a training example.

## How the data is made

The files here are generated in the [Agent-001](https://github.com/ishancoderr/Agent-001) repository (branch `sql-writer`, folder `finetune/`), because generating them needs the agent's own code:

1. A person writes the questions and correct extractions in `questions_v1.yaml`.
2. `python -m finetune.build_examples` derives every call the pipeline would make: the cleaned question text, the system prompts (from the agent's real prompt loaders) and the input of every SQL step. The correct SQL is generated from the agent's schema files and must pass the agent's SQL validator.
3. `python -m finetune.check_dataset` runs every label through the agent's own parser and SQL validator, and checks for duplicates, conflicting labels, outdated prompts and length.

To make a new version, edit the YAML in Agent-001, run both commands, and copy the outputs here.

## Labels follow the agent's code

Where the thesis's scenario document and the code differ, the labels follow the code: `marriages` rather than `married`, tables `states` / `state_demographics`, and SQL with `:named` placeholders instead of literal values.
