# Final Review: Complete Project + Evaluation + Demo

**Dates:** Monday 25 January → Friday 29 January 2027
**Final completion deadline:** Saturday 30 January 2027
**Phases covered:** Integration & Evaluation, Finalisation

## Goal

Present a **complete, working, tested, evaluated and documented system**, and demonstrate it.

## Expected

- **Complete working system**: the planned scope works end to end, and anything descoped is explained
- **Testing**: an automated test suite running in CI, plus manual testing of the main scenarios
- **Evaluation**: results produced with a documented, reproducible method, including limitations and failure cases (see [Evaluation Guide](evaluation-guide.md))
- **Documentation**: README complete with no remaining `TBD`s in key sections; architecture, setup and usage docs accurate
- **Deployment where applicable**: a hosted demo, a packaged tool or clear instructions to run it
- **Final demonstration**: a rehearsed live demo, with a recorded backup

## Final checklist

- [ ] README: overview, architecture, setup, usage, testing, evaluation, results, team: all filled in
- [ ] A new person can install and run the project by following the README
- [ ] `docs/architecture.md` matches the final system
- [ ] Evaluation results and how to reproduce them are documented
- [ ] Known limitations and future work are written down
- [ ] CI passes on `main`
- [ ] No secrets, credentials or private data in the repository (check history too)
- [ ] License decided (see [Licensing](github-guide.md#licensing))
- [ ] Release tagged (`v1.0.0` or `final`)
- [ ] Demo rehearsed, with a recorded backup
- [ ] Review update saved as `docs/updates/final-review.md`

## Questions reviewers are likely to ask

- Demonstrate the full system. What happens with unexpected input?
- What do the evaluation results show, and how confident are you in them?
- What are the limitations? Where does it fail?
- What did each member contribute?
- What would you do next with more time?

## After the final review

Repositories stay in the organisation as a record of the cycle and a starting point for future teams. Make sure `main` is in a clean, working state on 30 January 2027.
