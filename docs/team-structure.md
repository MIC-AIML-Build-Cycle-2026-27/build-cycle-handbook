# Team Structure

## Roles

| Role | Responsibilities |
|---|---|
| **Department Leads** | Run the Build Cycle as a whole. Organise reviews, maintain this handbook and the GitHub organisation, resolve cross-team issues. |
| **Project Leads** (2 per team) | Guide and coordinate the team: scope, task breakdown, assignments, progress tracking, integration, review preparation. Not expected to build the project themselves. See the [Project Lead Guide](project-lead-guide.md). |
| **Team Members** | Own and deliver tasks: research, code, experiments, tests, documentation and reviews of teammates' PRs. |

Project Leads decide member allocations, individual responsibilities, weekly targets and review-specific requirements for their team.

## Teams

| # | Project | Project Leads | Members |
|---|---|---|---|
| 1 | ONS | TBD, TBD | TBD |
| 2 | ASRA | TBD, TBD | TBD |
| 3 | PRISM | TBD, TBD | TBD |
| 4 | Repository Fixer | TBD, TBD | TBD |
| 5 | Hallucination Scorer | TBD, TBD | TBD |
| 6 | Code Evolver | TBD, TBD | TBD |
| 7A | DLD Screening | TBD, TBD | TBD |
| 7B | Software Investigator | TBD, TBD | TBD |

## GitHub teams and permissions

Access follows one rule: **you get what your role needs, on your own project only.**

```
Department Leads ............ admin on every repository
Project Leads ............... (all leads, for announcements and @mentions)

ONS ......................... write on ONS
 └─ ONS Leads ............... maintain on ONS          (inherits ONS membership)
ASRA ........................ write on ASRA
 └─ ASRA Leads .............. maintain on ASRA
... same pattern for every project ...
```

| GitHub team | Who is in it | Access |
|---|---|---|
| `department-leads` | Department Leads | **Admin** on all repositories |
| `project-leads` | All 16 Project Leads | **Read** on the handbook; used to notify all leads with `@MIC-AIML-Build-Cycle-2026-27/project-leads` |
| `<project>` (e.g. `ons`) | All members of that project, including its leads | **Write** on that project's repository only |
| `<project>-leads` (e.g. `ons-leads`), a child of the project team | That project's two leads | **Maintain** on that project's repository; requested as reviewers via CODEOWNERS |

Why it is set up this way:

- **Write** lets members push branches, open and merge PRs, and manage issues. Branch protection stops anyone pushing straight to `main`.
- **Maintain** adds managing settings that matter day to day (labels, milestones, releases, merging) without being able to delete the repository or change its visibility.
- **Admin** is limited to Department Leads.
- **Organisation owner** is limited to the Department Leads who administer the organisation. Everyone else is a regular member.
- Because each project team only has access to its own repository, members do not get write access to other projects. All repositories are public, so anyone can still *read* other teams' code and learn from it.

## Joining

1. Create a GitHub account if you do not have one, and **enable two-factor authentication**.
2. Send your GitHub username to your Project Leads.
3. Accept the organisation invitation (check your email or <https://github.com/orgs/MIC-AIML-Build-Cycle-2026-27/invitation>).
4. Read [Development Workflow](development-workflow.md) and your project's `CONTRIBUTING.md`.
