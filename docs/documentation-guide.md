# Documentation Guide

Documentation is part of the project, not something to add at the end. The test: **could a new team member set up the project and understand how it works using only the repository?**

## What goes where

| Document | Location | Contents | Update when |
|---|---|---|---|
| README | `README.md` | What the project is, how to set it up and run it, current progress, team | Setup, usage or status changes |
| Architecture | `docs/architecture.md` | Components, data flow, key decisions | The design changes |
| Contributing | `CONTRIBUTING.md` | How to work on this repository | The workflow changes |
| Weekly updates | `docs/updates/YYYY-MM-DD.md` | Progress, plans, blockers | Every week |
| Review updates | `docs/updates/review-N.md` | Summary for each review | Before each review |
| Research findings | The research issue, summarised in `docs/` | Question, sources, answer | Investigation completes |
| Experiment results | The experiment issue, plus `docs/` or `evaluation/` | Setup, results, how to reproduce | Experiment completes |
| Data | `docs/datasets.md` (or similar) | Where data comes from, license, how to get it, preprocessing | Data changes |
| Code | Docstrings / comments | Why non-obvious code works the way it does | With the code |

## Writing well

- **Lead with the point.** Start each section with the most important sentence.
- **Be concrete.** Write "Run `python -m ons.ingest data/sample.pdf`", not "Run the ingestion module".
- **Keep it current.** Wrong documentation is worse than none. Update docs in the same PR as the code change.
- **Use `TBD` honestly.** It is fine to leave a section as `TBD`, and better than filling it with guesses.
- **Prefer tables and lists** for structured information, and prose for explanations.
- **Diagrams** help for architecture and data flow. GitHub renders [Mermaid](https://docs.github.com/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams) diagrams in Markdown. Only add diagrams that explain something text cannot.
- **Avoid hype.** Describe what the system does and how well it does it. Skip words like "revolutionary" or "cutting-edge".

## Recording decisions

When the team makes an important technical choice (framework, model, data source, architecture), add a row to the *Key decisions* table in `docs/architecture.md`:

| Decision | Alternatives considered | Reason | Date |
|---|---|---|---|
| Example: Use library X for parsing | Library Y, custom parser | X handles our formats; Y lacked table support | 2026-10-20 |

It takes two minutes and saves hours of "why did we do this?" later.

## Notebooks

- Notebooks are good for exploration, but poor as the only record of results.
- Clear large outputs before committing. Never commit notebooks that contain secrets or personal data.
- Move code that the system depends on into `src/`.
- Summarise conclusions in the issue or in `docs/`.
