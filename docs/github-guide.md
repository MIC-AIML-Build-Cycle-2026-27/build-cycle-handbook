# GitHub Guide

How the organisation uses GitHub features. For the day-to-day branch and PR flow, see [Development Workflow](development-workflow.md).

- [Organisation layout](#organisation-layout)
- [Issues](#issues)
- [Labels](#labels)
- [Project boards](#project-boards)
- [Milestones](#milestones)
- [Pull requests](#pull-requests)
- [Branch protection](#branch-protection)
- [CODEOWNERS](#codeowners)
- [GitHub Actions](#github-actions)
- [Releases](#releases)
- [Licensing](#licensing)
- [Security](#security)
- [Git basics cheat sheet](#git-basics-cheat-sheet)

## Organisation layout

| Repository | Purpose |
|---|---|
| `ONS`, `ASRA`, `PRISM`, `Repository-Fixer`, `Hallucination-Scorer`, `Code-Evolver`, `DLD-Screening`, `Software-Investigator` | One repository per project |
| `build-cycle-handbook` | This handbook |
| `project-template` | Template for new project repositories |
| `.github` | Organisation profile page and shared workflow templates |

Each project lives in its **own** repository. Do not put several projects in one repository.

## Issues

Issues are the unit of work. Every repository has templates:

| Template | Use when |
|---|---|
| **Feature** | Adding new functionality |
| **Bug report** | Something is broken |
| **Task** | Setup, refactoring, integration, chores |
| **Research / Investigation** | A question must be answered before deciding how to build something |
| **Experiment** | Testing a model, prompt or approach and recording results |
| **Documentation** | Writing or fixing docs |

Good issue habits:

- One outcome per issue. Size it to **1–5 days** of work.
- Always have an assignee once work starts.
- Write findings and decisions in the issue, so they are not lost in chat.
- Use task lists (`- [ ]`) for small sub-steps, and sub-issues for bigger ones.

## Labels

Every project repository uses the same small set of labels. Issue templates apply the `type:` label automatically.

| Group | Labels | Meaning |
|---|---|---|
| **type** | `type: feature`, `type: bug`, `type: task`, `type: research`, `type: experiment`, `type: docs` | What kind of work it is |
| **area** | `area: frontend`, `area: backend`, `area: ml`, `area: ai`, `area: data`, `area: devops`, `area: testing` | Which part of the system. `ml` = model training/inference. `ai` = LLMs, agents, prompting. |
| **status** | `status: in-progress`, `status: needs-review`, `status: blocked` | Use sparingly. The project board is the main source of status. `blocked` is the important one. |
| **priority** | `priority: high`, `priority: medium`, `priority: low` | Relative urgency within the team |
| **other** | `good first issue`, `help wanted`, `duplicate`, `wontfix` | GitHub conventions |

There are **no milestone labels** (`review-1`, etc.). Use GitHub [milestones](#milestones) instead, so information is not duplicated.

Teams may add labels for their own needs (e.g. `area: retrieval`). Keep the shared ones unchanged so cross-team views stay consistent.

## Project boards

### Team boards (one per project)

Each team has a GitHub Project (the *Projects* tab) with these columns:

```
Backlog → Todo → In Progress → Review → Testing → Done
```

| Column | Meaning |
|---|---|
| **Backlog** | Ideas and future work, not yet planned |
| **Todo** | Planned for the current week or milestone, ready to start |
| **In Progress** | Someone is actively working on it |
| **Review** | PR open, waiting for review |
| **Testing** | Merged or ready to merge, being verified / evaluated |
| **Done** | Finished and verified |

Recommended board setup:

- Add the repository's issues and PRs (enable the *Auto-add to project* workflow for the repository).
- Enable the built-in workflows: *Item closed → Done* and *Pull request merged → Done*.
- Add fields: **Milestone**, **Assignees**, **Labels**, and optionally **Priority** and **Size**.
- Useful views: *Board* (by status), *Table grouped by assignee*, *Table filtered to current milestone*.

### Department board (one for the whole cycle)

A single board where **each item represents a team**, not individual tasks. It gives Department Leads an overview without cluttering team boards.

| Field | Values |
|---|---|
| Project | ONS, ASRA, PRISM, ... |
| Phase | Foundation, POC, Core Build, MVP, Integration & Evaluation, Finalisation |
| Health | On track, At risk, Off track |
| Next review | Review 1, Review 2, Final Review |
| Blockers | Free text |
| Last update | Date |

| Goes on the **team board** | Goes on the **department board** |
|---|---|
| Individual issues and PRs | One item per team |
| Daily / weekly task movement | Phase, health and blockers, updated weekly |
| Assignments to members | Cross-team dependencies and escalations |

Project Leads update their team's item on the department board after each weekly update.

## Milestones

Every project repository has three milestones:

| Milestone | Due |
|---|---|
| Review 1 | 3 Nov 2026 |
| Review 2 | 24 Dec 2026 |
| Final Review | 30 Jan 2027 |

How to use them:

- Set a milestone on **every issue** that is planned for a review. Leave unplanned ideas without one (they stay in the Backlog).
- **PRs** do not need a milestone if they close an issue that has one. Set one on PRs without a linked issue.
- The milestone page shows progress (% of issues closed). Use it to prepare for reviews.
- After a review, move unfinished issues to the next milestone deliberately. Do not let them carry over silently.

## Pull requests

- Use the PR template. Fill in what changed, why, how it was tested and any results.
- Link the issue with `Closes #<number>`.
- Prefer **Squash and merge**. Delete the branch after merging.
- Use **draft PRs** for work in progress you want feedback on.

## Branch protection

`main` in every project repository is protected by a ruleset:

| Rule | Setting |
|---|---|
| Pull request required before merging | Yes |
| Required approvals | 1 |
| Dismiss stale approvals when new commits are pushed | No (keeps things light) |
| Required status check | `ci-status` |
| Direct pushes to `main` | Blocked |
| Force pushes | Blocked |
| Branch deletion | Blocked |
| Bypass | Organisation admins (Department Leads), for emergencies only |

**Relaxing the rules:** for very small or experimental repositories (for example a one-person spike or a throwaway prototype), Department Leads may reduce the required approvals to 0 or drop the CI requirement. Keep *no force pushes* and *no deletion* everywhere.

The ruleset is under **Settings → Rules → Rulesets** in each repository.

## CODEOWNERS

`.github/CODEOWNERS` automatically requests reviewers when a PR touches certain files. Each project repository lists its leads team:

```
*  @MIC-AIML-Build-Cycle-2026-27/ons-leads
```

Leads can add individual usernames or route folders to specific people:

```
/evaluation/  @<add GitHub username>
```

Code owner approval is **not** required. Any one approval is enough. CODEOWNERS only makes sure the right people are notified.

## GitHub Actions

- Each repository ships with an adaptive `CI` workflow (Python and Node.js). See [Development Workflow → CI](development-workflow.md#continuous-integration-ci).
- Templates for **Python, Node.js, Java (Maven/Gradle) and .NET** are available in every repository under **Actions → New workflow → By MIC AIML Build Cycle 2026-27**.
- Store secrets in **Settings → Secrets and variables → Actions**, never in the workflow file.
- Free GitHub-hosted runners have no GPU. Keep CI to fast checks (lint, unit tests, small smoke tests). Run training and large evaluations elsewhere and commit the results and scripts.

## Releases

Releases mark meaningful checkpoints. **Recommended**, not mandatory:

| Version | Checkpoint |
|---|---|
| `v0.1.0` | Review 1 (POC) |
| `v0.5.0` | Review 2 (MVP) |
| `v1.0.0` | Final Review |

To create one: **Releases → Draft a new release → choose a tag (e.g. `v0.1.0`) on `main` → Generate release notes → Publish.**

If semantic versioning does not fit your project (for example a research project whose output is a report and evaluation results), tag the review state anyway (`review-1`, `review-2`, `final`), so reviewers can see exactly what was presented.

## Licensing

> **Status: decision pending. Department Leads must confirm.**
>
> Each repository currently has a placeholder `LICENSE` file. Until a real license is added, the code is publicly visible, but nobody is legally allowed to reuse it.

Things to check before choosing:

1. **University / club IP policy.** Some universities claim rights over work produced with their resources or under official programmes. Check whether MIC or the university has a policy before licensing anything.
2. **Who holds copyright.** By default, each contributor owns the copyright to what they wrote. An open-source license is how they allow others, including future Build Cycle teams, to reuse it.
3. **Third-party code, models and datasets.** Their licenses may restrict what you can do (e.g. non-commercial datasets, model licenses with use restrictions). These obligations apply regardless of the license you choose.

Recommended default, once the IP question is cleared:

| License | Implications | Fit |
|---|---|---|
| **MIT** (recommended default) | Anyone can reuse, modify and distribute the code, including commercially, as long as they keep the copyright notice. No warranty. | Simple, widely understood, good for portfolios and for future teams building on the work |
| Apache-2.0 | Like MIT, plus an explicit patent grant and requirements to note changes | Good if a project may have patentable ideas or industry partners |
| GPL-3.0 | Derivative works must also be open source under GPL | Only if the team specifically wants to prevent closed-source reuse |
| No license / "All rights reserved" | Code visible but not reusable | Only if IP policy requires it |

Projects involving **external partners, proprietary data or sensitive domains** (e.g. any project using real company documents or speech data from real people) should confirm with Department Leads before choosing a license, and must document dataset licenses separately.

To add a license: replace the contents of `LICENSE` with the full license text, put the correct year and copyright holder (e.g. `Copyright (c) 2026 <project contributors>`), and update the README's *License* section.

## Security

All repositories are **public**.

- **Never commit** API keys, passwords, tokens, `.env` files, private keys, or personal data. The template `.gitignore` blocks common cases, but it is not a guarantee.
- Use environment variables locally (`.env`, ignored by git) and **GitHub Actions secrets** in CI.
- Commit a `.env.example` listing the variable names, with dummy values.
- **If a secret is committed:** revoke or rotate it with the provider **immediately**, then tell your Project Leads. Removing it from the code does not undo the exposure.
- **Report vulnerabilities privately** via *Security → Report a vulnerability* on the repository, or contact the Department Leads. Do not open a public issue.
- **Personal data:** projects working with data about real people must not commit raw data. This includes speech recordings, documents with names, and user profiles. Document where the data is stored and how consent and access are handled.
- Enable **two-factor authentication** on your GitHub account.
- Be careful running code from unknown repositories. Do not enable editor settings that automatically run tasks when a folder is opened (e.g. VS Code `task.allowAutomaticTasks`).

## Git basics cheat sheet

| Task | Command |
|---|---|
| Clone | `git clone https://github.com/MIC-AIML-Build-Cycle-2026-27/<repo>.git` |
| Update main | `git switch main && git pull` |
| New branch | `git switch -c feature/<name>` |
| See changes | `git status`, `git diff` |
| Stage and commit | `git add <files>` then `git commit -m "Add X"` |
| Push a new branch | `git push -u origin feature/<name>` |
| Bring in latest main | `git merge main` (while on your branch) |
| Undo unstaged changes to a file | `git restore <file>` |
| Unstage a file | `git restore --staged <file>` |
| See history | `git log --oneline --graph` |

New to Git? Work through <https://docs.github.com/get-started/start-your-journey> and ask your Project Leads or teammates. Everyone was new to it once.
