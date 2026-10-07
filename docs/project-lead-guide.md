# Project Lead Guide

Each project has **two Project Leads**. Your job is to **guide and coordinate** the team so that it builds the project, and so that everyone on it gets real opportunities to contribute and learn. You are not expected to build the project yourself.

## Responsibilities

| Area | What it means in practice |
|---|---|
| **Scope and direction** | Finalise what the project will and will not do. Agree on the technical approach with the team. Write it in the README and `docs/architecture.md`. |
| **Task breakdown** | Turn the scope into issues that are small enough to finish in a few days, each with a clear definition of done. |
| **Assignments** | Assign each issue to a person. Make sure everyone has meaningful work, not only the most experienced members. |
| **Weekly targets** | Set what the team aims to finish each week and check it at the end of the week. |
| **Progress tracking** | Keep the project board accurate. Update the department board and post the weekly update. |
| **Unblocking** | Notice when someone is stuck and help directly, pair them with someone, or escalate. |
| **Integration** | Make sure separately built parts actually connect. Plan integration work explicitly; it does not happen by itself. |
| **Quality** | Make sure PRs are reviewed, tests are written, and documentation keeps up with the code. |
| **Reviews** | Prepare the team for each review: what to show, who presents, what evidence to bring. |
| **Communication** | Report progress and blockers to Department Leads early. Bad news early is far better than surprises at review time. |

## A practical weekly rhythm

You can adapt this, but some regular rhythm helps.

| When | What |
|---|---|
| Start of week | Short planning sync (15–30 min): review the board, agree the week's targets, assign issues, set milestones. |
| During the week | Review PRs promptly. Check in with anyone whose issue has not moved. Watch for `status: blocked`. |
| End of week | Write the weekly update ([template](../templates/weekly-update.md)) in `docs/updates/`. Update your team's row on the department board. |

## Splitting the two lead roles

Two leads work best when they divide responsibilities clearly instead of both doing everything. One option:

| Lead A | Lead B |
|---|---|
| Technical direction, architecture, integration | Planning, board, weekly updates, review preparation |
| Reviews core / ML PRs | Reviews docs / testing / evaluation PRs |

Agree on the split together and write it in the README.

## Writing good issues

A good issue answers three questions:

1. **What** needs to be done? (one clear outcome)
2. **Why** does it matter? (which part of the project it supports)
3. **How will we know it is done?** (acceptance criteria / definition of done)

Size issues so they take **1–5 days**. If an issue keeps growing, split it.

Tag each issue with a `type:` label, an `area:` label if useful, a milestone and an assignee. See [GitHub Guide → Labels](github-guide.md#labels).

## Making sure everyone contributes

- Give every member at least one issue they **own**, not only small fixes.
- Rotate who does integration, testing and documentation, so it does not always fall on the same people.
- Pair newer members with more experienced ones on their first PRs.
- Use `good first issue` for tasks suited to people new to the codebase.
- Check the **Insights → Contributors** graph occasionally. It is not a performance measure, but it shows quickly if someone has been left out.

## Preparing for reviews

About a week before each review:

1. Read the review page: [Review 1](review-1.md), [Review 2](review-2.md), [Final Review](final-review.md).
2. Check the milestone: which issues are still open? Which can realistically close, and which move to the next milestone?
3. Make sure the README's *Current Progress* section is accurate.
4. Fill in the [review update template](../templates/review-update.md).
5. Rehearse the demo at least once on a clean setup.
6. After the review, tag a release if the team wants one (see [Releases](github-guide.md#releases)).

## Repository admin tasks for leads

As maintainers of your repository you are responsible for:

- [ ] Replacing placeholders in the README (Project Leads, Team, board link)
- [ ] Adding your usernames to `.github/CODEOWNERS` if you prefer individual owners to the leads team
- [ ] Creating the team project board and linking it in the README
- [ ] Keeping milestones and labels in order
- [ ] Deciding, with the team, the folder structure that suits the project
- [ ] Making sure CI is meaningful once real code exists (see [Development Workflow → CI](development-workflow.md#continuous-integration-ci))

## When to escalate

Contact the Department Leads if:

- The team is likely to miss a review's core expectations
- Scope needs to change significantly
- A member has been inactive for an extended period
- There is a conflict the leads cannot resolve
- Anything sensitive was committed to a repository (see [Security](github-guide.md#security))
