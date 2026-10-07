# Evaluation Guide

Every Build Cycle project must show **evidence that it works**, and **how well**. This guide covers how to approach evaluation. Each team decides its actual metrics and datasets with its Project Leads, because they depend on the project.

## Testing vs evaluation

| | Testing | Evaluation |
|---|---|---|
| **Question** | Does the code do what we intended? | How well does the system solve the problem? |
| **Examples** | Unit tests, integration tests, end-to-end smoke tests | Accuracy-style metrics, comparison with a baseline, user or expert assessment, error analysis |
| **Runs** | On every PR, in CI | Periodically, with documented scripts and data |
| **Output** | Pass / fail | Numbers, tables, plots, qualitative findings |

Both are required by the Final Review.

## Testing

- Start with **unit tests** for the core logic: parsing, scoring, transformations, decision rules.
- Add an **end-to-end smoke test** for the main workflow on a tiny sample input, small enough for CI.
- For components that call LLMs or external APIs, test your own logic around them by **mocking** the call. Do not spend API credits in CI.
- Test **edge cases**: empty input, malformed input, very large input, missing fields.

## Designing an evaluation

Decide these **before** running experiments, ideally by Review 2, and write them down in `docs/` or `evaluation/`:

1. **What question is the evaluation answering?** Tie it to the project's objective.
2. **What data?** Where it comes from, how big it is, whether it represents real use, and its license.
3. **What metric(s)?** Choose metrics that match the question. Explain why they are appropriate, and what a good value means.
4. **What baseline?** Compare against something: a simple heuristic, an existing tool, a previous version, or human performance. A number without a baseline is hard to interpret.
5. **How is it reproduced?** A script, a config and the exact commit, so someone else gets the same numbers.

## Honest reporting

- Report results on data the system was **not tuned on**. Keep a held-out set if you tune anything (prompts included).
- Report **failure cases and limitations**, not only averages. Show examples where the system goes wrong.
- Report **variance** where results are not deterministic (e.g. LLM outputs): run more than once.
- Do not cherry-pick. If you ran five configurations, say so.
- A clear negative or mixed result is a valid outcome. Inflated claims are not.

## Projects involving people or sensitive data

Some projects work with data about real people or with outputs that could affect people. Examples are speech or language samples, personal documents, and user preferences. For these:

- Do not commit raw personal data to the repository. Document where it is stored and who can access it.
- Make sure there is appropriate consent for any data collected, and follow any university or club policies. Ask the Department Leads if unsure.
- Be explicit about **what the system is and is not**. For example, a *screening* tool produces signals for further review by qualified people. It is not a diagnosis.
- Evaluate and report how the system performs across different groups where relevant, and note gaps in the data.

## Where to put it

```
evaluation/            # or docs/evaluation.md for smaller projects
├── README.md          # question, data, metrics, baseline, how to run
├── run_eval.*         # script(s) that produce the results
├── configs/           # settings used for each reported run
└── results/           # small result files (tables, plots)
```

Link the latest results from the README's *Evaluation* section.
