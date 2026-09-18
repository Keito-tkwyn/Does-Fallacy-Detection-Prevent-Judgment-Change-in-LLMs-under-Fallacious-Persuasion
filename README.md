# QA Datasets and Persuasion Prompts

This repository contains the QA datasets and persuasion prompts used in our experiments on judgment change in large language models (LLMs) under persuasion containing logical fallacies.

The repository contains two main directories:

```text
.
├── QAdataset/
│   ├── boolQ.csv
│   ├── boolQ_val.csv
│   ├── MMLU.jsonl
│   └── MMLU_val.jsonl
│
└── persuasion_prompts/
    ├── boolQ/
    │   ├── [fallacy_type].txt
    │   ├── ...
    │   ├── dummy.txt
    │   ├── all_fallacies.txt
    │   └── val.txt
    │
    └── MMLU/
        ├── [fallacy_type].txt
        ├── ...
        ├── dummy.txt
        ├── all_fallacies.txt
        └── val.txt
```

## QA Datasets

The `QAdataset/` directory contains the QA examples used in our experiments.

We use questions from two datasets:

* **BoolQ**, a binary QA task
* **MMLU**, a four-choice multiple-choice QA task

For each dataset, we use a total of **500 questions**. These are divided into 400 questions for the main analyses and 100 held-out questions for evaluating the vector intervention.

| File             | Number of questions | Usage                                           |
| ---------------- | ------------------: | ----------------------------------------------- |
| `boolQ.csv`      |                 400 | Behavior-level evaluation and internal analyses |
| `boolQ_val.csv`  |                 100 | Vector intervention evaluation                  |
| `MMLU.jsonl`     |                 400 | Behavior-level evaluation and internal analyses |
| `MMLU_val.jsonl` |                 100 | Vector intervention evaluation                  |

The `_val` files contain the held-out subset used for the vector intervention experiments.

### BoolQ data format

The BoolQ files are stored in CSV format.

Each example consists of:

* a question
* the correct answer

The answer is either `True` or `False`.

Conceptually, each row has the following structure:

```text
(question, answer)
```

### MMLU data format

The MMLU files are stored in JSONL format.

Each example contains the following fields:

| Field       | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| `question`  | The question text                                           |
| `choices`   | The four answer choices                                     |
| `answer`    | The correct answer                                          |
| `incorrect` | A predefined incorrect answer used as the persuasion target |

The `incorrect` field specifies the incorrect answer toward which the model is intended to be persuaded.

The fallacy-based persuasion prompts for each MMLU question are generated to support this predefined incorrect answer.

For example, if the correct answer is `b` and `incorrect` is `d`, the persuasion prompts corresponding to that question are constructed to support answer `d`.

## Persuasion Prompts

The `persuasion_prompts/` directory contains the persuasion prompts corresponding to the QA examples.

Separate directories are provided for BoolQ and MMLU:

```text
persuasion_prompts/
├── boolQ/
└── MMLU/
```

Both directories follow the same structure.

### Fallacy-specific prompt files

For each of the **13 logical fallacy types**, a separate text file is provided:

```text
[fallacy_type].txt
```

Each file contains **500 persuasion prompts**, with one prompt corresponding to each of the 500 QA examples.

The prompts are constructed to support an incorrect answer while containing the designated logical fallacy.

For MMLU, the supported incorrect answer corresponds to the answer specified by the `incorrect` field in the QA data.

Across the 13 fallacy types, each dataset therefore contains:

```text
13 fallacy types × 500 questions = 6,500 fallacy-based prompts
```

### `dummy.txt`

`dummy.txt` contains **500 prompts without logical fallacies**.

Unlike the fallacy-based prompts, which support an incorrect answer, the prompts in `dummy.txt` support the **correct answer** to the corresponding question.

These prompts are used as the no-fallacy control condition.

### `all_fallacies.txt`

`all_fallacies.txt` contains the prompts corresponding to the 400-question subset used for the behavior-level evaluation and internal analyses.

It combines all 13 fallacy conditions and the no-fallacy control condition:

```text
14 conditions × 400 questions = 5,600 prompts
```

The 14 conditions consist of:

* 13 logical fallacy conditions, each supporting an incorrect answer
* 1 no-fallacy (`dummy`) condition supporting the correct answer

### `val.txt`

`val.txt` contains the prompts corresponding to the held-out 100-question subset used for evaluating the vector intervention.

It contains the same 14 conditions:

```text
14 conditions × 100 questions = 1,400 prompts
```

The 14 conditions again consist of the 13 fallacy conditions and the no-fallacy control condition.

## Data Summary

For each of BoolQ and MMLU, the persuasion prompt directory contains:

| Data                      | Number of prompts |
| ------------------------- | ----------------: |
| 13 fallacy-specific files |             6,500 |
| `dummy.txt`               |               500 |
| `all_fallacies.txt`       |             5,600 |
| `val.txt`                 |             1,400 |

`all_fallacies.txt` and `val.txt` are reorganized subsets of the prompts contained in the 13 fallacy-specific files and `dummy.txt`. They are provided for convenience and do not contain independently generated additional prompts.

The 500 QA examples and their corresponding prompts are divided as follows:

```text
500 questions
├── 400 questions → main analyses
│   └── 14 × 400 = 5,600 prompts in all_fallacies.txt
│
└── 100 questions → vector intervention evaluation
    └── 14 × 100 = 1,400 prompts in val.txt
```

## Intended Use

These data were prepared for experiments examining how LLM judgments change after receiving persuasive prompts containing logical fallacies.

The 400-question subset is used for behavior-level evaluation and analyses of internal model representations. The held-out 100-question subset is used to evaluate vector-based interventions.

The released data can also be used for research on topics such as:

* judgment change in LLMs
* persuasion under flawed reasoning
* logical fallacy detection
* robustness of model judgments
* analysis of internal model representations

## Citation

If you use this dataset or the persuasion prompts in your research, please cite our paper:

```bibtex
@article{TODO,
  title   = {TODO},
  author  = {TODO},
  year    = {2026}
}
```

## License

Please refer to the license information of this repository and the original BoolQ and MMLU datasets when using the released data.
