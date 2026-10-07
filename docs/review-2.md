# Review 2: MVP

**Dates:** Sunday 20 December → Thursday 24 December 2026
**Milestone due:** 24 December 2026
**Phases covered:** Core Build, MVP

## Goal

Show a **Minimum Viable Product**: the main components are built and connected, and **the core workflow runs end to end**, with first evidence of how well it works.

## Expected

- **Main components connected**: not separate scripts, but one system where the output of one part feeds the next
- **Core workflow working end-to-end**: a user or reviewer can follow the main scenario from input to result
- **Initial testing / evaluation / results**
  - Automated tests for the important parts, running in CI
  - An evaluation method decided and written down (see [Evaluation Guide](evaluation-guide.md))
  - First results, even if preliminary, with a note on their limitations

## Evidence to bring

| Item | Where |
|---|---|
| End-to-end demo | Review session |
| Updated architecture (reflecting what was actually built) | `docs/architecture.md` |
| Test suite passing in CI | Repository → Actions |
| Evaluation plan and initial results | `docs/` or `evaluation/` |
| Review update | `docs/updates/review-2.md` |

## Questions reviewers are likely to ask

- Walk through the full workflow. Where does it break or need manual steps?
- How do you know it works? What are the tests and results?
- What changed since Review 1, and why?
- What is left for the Final Review, and is it realistic in about 4.5 weeks including the holidays?

## Team-specific requirements

Project Leads may add requirements. List them in the README under *Build Cycle Milestones → Review 2*.

## After the review

- Turn feedback into issues on the *Final Review* milestone.
- Freeze scope: from here on, prioritise completing, testing, evaluating and documenting over adding new features.
- Optional: tag `v0.5.0`.
