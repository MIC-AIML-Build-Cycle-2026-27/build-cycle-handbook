# Development Workflow

One simple workflow for every team:

```
main ──► branch (feature/fix/research/experiment/docs) ──► Pull Request ──► Review ──► CI ──► Merge into main
```

`main` should always contain working code. All work happens on short-lived branches and comes back through a pull request.

## Step by step

### 1. Start from an issue

Pick an issue assigned to you on the project board, or create one with the right template. Assign yourself and set a milestone. Small fixes such as typos can skip this step.

### 2. Create a branch

```bash
git switch main
git pull
git switch -c feature/document-parser
```

| Prefix | Use for |
|---|---|
| `feature/<name>` | New functionality |
| `fix/<name>` | Bug fixes |
| `research/<name>` | Literature review, investigation, spikes |
| `experiment/<name>` | Model / prompt / parameter experiments |
| `docs/<name>` | Documentation only |

Use lowercase and hyphens: `feature/risk-scoring`, not `Feature/RiskScoring_v2`. Adding the issue number is optional: `fix/31-empty-input`.

### 3. Commit

Small commits with clear, imperative messages:

```
Add carrier data loader
Fix off-by-one error in date parsing
Document evaluation setup
```

### 4. Push and open a pull request

```bash
git push -u origin feature/document-parser
```

Open the PR on GitHub, fill in the template and link the issue with `Closes #<number>`. Open it as a **draft** if you want early feedback.

### 5. Review

- At least **one approval** is required.
- The project's leads are requested automatically, but **any teammate can review**, and reviewing is part of everyone's job.
- Reviewers check: does it work, is it understandable, is it tested, does it belong in this PR?
- Authors respond to every comment and push fixes to the same branch.

### 6. CI

The `CI` workflow runs on every PR. The `ci-status` check must pass before merging.

### 7. Merge

Use **Squash and merge**, then delete the branch. The linked issue closes automatically.

## Keeping your branch up to date

If `main` moves on while you work:

```bash
git switch main
git pull
git switch feature/document-parser
git merge main        # resolve conflicts if any, then commit
git push
```

Teams comfortable with rebasing can use `git rebase main` instead. Never force-push to `main`. It is blocked anyway.

## Research and experiment branches

Research and experiments do not always produce code that should be merged. That is fine.

- **Record the result in the issue** (findings, numbers, plots, conclusions), even if the branch is not merged.
- Merge into `main` only what the team will keep: reusable code, documented results, evaluation scripts.
- Notebooks: clear large outputs before committing, and move reusable logic into `src/`.
- Close experiment branches you no longer need, and link the final commit in the issue so results stay reproducible.

## Code review guidelines

**As a reviewer**

- Review within one to two days. Waiting on reviews is the most common reason teams slow down.
- Be specific: point to the line and explain *why*.
- Separate blocking comments from suggestions (prefix optional ones with "nit:" or "optional:").
- Approve when the change is good enough and moves the project forward. It does not have to be perfect.

**As an author**

- Keep PRs small and focused. Under about 400 changed lines is a good target.
- Explain what to look at in the PR description.
- Do not take feedback personally. Review is about the code.

## Continuous Integration (CI)

Every repository includes `.github/workflows/ci.yml`. It detects what is in the repository:

| If the repository has | CI runs |
|---|---|
| `requirements.txt` or `pyproject.toml` | `ruff check` (lint) and `pytest` |
| `package.json` | `npm ci`/`npm install`, then `lint`, `test`, `build` scripts if defined |
| Neither | Nothing yet. CI passes with a notice. |

Adapting it:

- **Code in a subfolder** (e.g. `backend/`): change `PYTHON_DIR` / `NODE_DIR` at the top of the workflow.
- **Other languages** (Java, C#, Go...): go to **Actions → New workflow** and use the templates under *By MIC AIML Build Cycle 2026-27*, or copy the job into `ci.yml` and add it to `ci-status`'s `needs:` list.
- **Heavy ML dependencies:** create a lighter `requirements-ci.txt` for CI and point the install step at it.
- **Keep the job named `ci-status`.** It is the required check for `main`.

CI that always passes is not useful. Once the project has real code, make sure CI runs real tests.

## Adapting the repository structure

The template gives a minimal starting layout (`src/`, `tests/`, `docs/`). Projects should adapt it:

| Project type | Typical additions |
|---|---|
| AI / ML research | `experiments/`, `evaluation/`, `notebooks/`, `configs/`, `data/` (small samples only) |
| Web application | `frontend/`, `backend/` in place of, or alongside, `src/` |
| Agent / tooling | `src/<package>/`, `sandbox/` or `environments/`, `examples/` |
| Multi-service | One folder per service, plus `docker/` or `deploy/` |

Rules of thumb:

- Make the layout obvious to a newcomer, and describe it in the README's *Repository Structure* section.
- Do not commit large datasets, model weights or secrets. Document where they come from instead.
- Change the structure when the project needs it, not before.
