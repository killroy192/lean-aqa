# Phase 2: Building the verification layer (Weeks 5–8)

**Depth:** **Own** (verification layers). **Time:** ~4 weeks at 6–7 h. **Track T2 completes, T3 begins.**

## Goal
She can set up tooling so that agents find their own mistakes, so she does not have to read the code. She builds an agent-written test suite and proves, with mechanisms, that it actually catches bugs.

## What to learn

### The idea
- [ ] **Output is not evidence.** Evidence is a check that fails when the thing is wrong.
- [ ] Layers: fast checks (lint, types) → tests → mutation/planted-bug checks → independent review → CI gates
- [ ] Why agents write tests that pass but assert nothing useful (tautologies, element-exists only, mocks that mirror the code)

### Self-checking loops
- [ ] Linters and formatters (what they catch, how an agent runs them)
- [ ] Type checking (concept; the agent runs it)
- [ ] Hooks and project rules so the agent must run checks before it says "done"
- [ ] Reading a check result: pass/fail, what the failing output means

### Test-the-tests
- [ ] **Mutation testing:** change the code on purpose; if tests still pass, the tests are weak
- [ ] **Planted bugs:** she (or the mentor) introduces a defect by hand or via the agent and checks the suite catches it
- [ ] Coverage: what it tells you and what it hides (coverage ≠ quality)
- [ ] **Diff-based gates:** detect deleted or weakened assertions, skipped tests, added `sleep`/retries

### Independent verification
- [ ] A second agent / subagent reviews the first one's work **against the spec**, not the code
- [ ] Why the reviewer should not share the author's context

### CI gates
- [ ] What CI is; required checks on pull requests
- [ ] Artifacts the agent can read: traces, screenshots, logs, reports
- [ ] Flake detection (run N times; compare)

### Simplicity guardrails
- [ ] Limits on diff size and number of files
- [ ] "No new dependencies without approval"
- [ ] Complexity or duplication checks

### Test tooling (agent writes it; she knows the landscape)
- [ ] pytest and Playwright at the level of "what is a test, a fixture, a locator, a trace"
- [ ] API vs UI tests, and why API tests are cheaper and more stable
- [ ] Language choice: Python (pytest + Playwright) is the default in this plan; TypeScript is equally fine if the team uses it. Pick one and stay with it.

## Resources

### Test frameworks (skim, don't memorize)
- **A.** 📖 Playwright for Python — intro and trace viewer — https://playwright.dev/python/docs/intro and https://playwright.dev/python/docs/trace-viewer
- **B.** 📖 Playwright (TypeScript) docs — https://playwright.dev/docs/intro
- **C.** 📖 pytest "Get started" — https://docs.pytest.org/en/stable/getting-started.html
- 📚 Test Automation University (free courses; pick Playwright or API testing basics) — https://testautomationu.applitools.com

### Mutation testing (pick the one matching your language)
- **Python:** `mutmut` — https://github.com/boxed/mutmut
- **JS/TS:** Stryker Mutator — https://stryker-mutator.io/docs/
- 📖 Concept overview: Google Testing Blog, "Does your code pass the mutation test?" — https://testing.googleblog.com/2021/04/mutation-testing.html

### Linters, hooks, gates
- 📖 Ruff (Python linter/formatter) — https://docs.astral.sh/ruff/
- 📖 Claude Code hooks guide — https://docs.claude.com/en/docs/claude-code/hooks-guide
- 📖 pre-commit framework — https://pre-commit.com
- 📖 coverage.py — https://coverage.readthedocs.io

### CI
- **A.** 🛠 GitHub Skills, "Hello GitHub Actions" — https://skills.github.com
- **B.** 📖 GitHub Actions docs, "Understanding GitHub Actions" — https://docs.github.com/en/actions/get-started/understanding-github-actions
- 📖 Playwright CI guide — https://playwright.dev/python/docs/ci-intro

### Concepts of good tests (short reads)
- 📖 Martin Fowler, "Test Pyramid" — https://martinfowler.com/bliki/TestPyramid.html
- 📖 Martin Fowler, "Eradicating Non-Determinism in Tests" — https://martinfowler.com/articles/nonDeterminism.html

### Practice targets (pick one UI + one API)
- **UI:** SauceDemo — https://www.saucedemo.com
- **UI + API:** Restful-booker / Automation in Testing — https://automationintesting.online
- **UI:** ParaBank — https://parabank.parasoft.com
- **API:** JSONPlaceholder (simple) — https://jsonplaceholder.typicode.com

## Practical projects

### Project 1: Agent-built suite
With the spec-first workflow from Phase 1:
1. She writes the test specs (what to verify, and why) for the demo app: ~10–15 UI cases and ~8–10 API cases.
2. The agent builds the suite. She does not edit code by hand.
3. The suite runs from a clean clone with one command (documented in `README.md`).

### Project 2: Self-checking agent
Configure the project so the agent **cannot report done without** running: linter, tests, and a short summary of what was checked. Use hooks or `CLAUDE.md` rules. Prove it by giving a task where the checks fail and watching the agent react.

### Project 3: Prove the suite works
1. Run mutation testing against the app code or a small sample under test; list surviving mutants.
2. Plant 5 bugs by asking an agent (or the mentor) to inject realistic defects. Record which the suite caught or missed.
3. Ask a second agent to review the suite against the spec; compare its findings.
4. Improve the verification layer based on what was missed. Document how.

### Project 4: Weakening gate
Ask an agent to "make the failing test pass" in a way that cheats (delete an assertion, add a sleep). Build a gate (diff check, rule, hook) that catches it. Prove the gate fires.

### Project 5: CI
Run the suite on every pull request in GitHub Actions with the report and traces as artifacts. Make it a required check.

## Agent exercises
- "Write a test that would fail if feature X broke." Then break X and verify.
- "Review these tests against this spec. What is missing? What is asserted that doesn't matter?"
- "List every assertion in this file in plain English." She reads the English, not the code.
- Ask for the smallest change that fixes a failure, then check the diff size.

## Mentor drills (weekly)
- **Week 5:** a suite where half the tests are tautologies. She finds them using mutation results and the plain-English assertion list.
- **Week 6:** an agent "fixed" a failing test by weakening it. She identifies it from the diff summary and the gate.
- **Week 7:** a green CI that hides a skipped test. She finds it from the report.
- **Week 8:** over-engineered test framework (extra layers, new dependency). She asks for the simplest version and measures the reduction.

## Done when
- [ ] The suite runs from a clean clone in CI and locally
- [ ] She shows **one planted defect the suite caught, one weakened test the gates caught, and one the layer missed**, plus how she improved the layer
- [ ] The agent cannot say "done" without running the checks (demonstrated)
- [ ] She can explain, in plain words, why coverage alone doesn't prove quality
- [ ] A second-agent review exists and its findings are documented

## Pitfalls
- Trusting a green build. Always ask: what bug would turn this red?
- Chasing 100% coverage or 100% mutation score. Aim to know what's *not* covered, and decide.
- Building a large framework. Prefer the simplest suite that catches the planted bugs.
- Verifying with the same agent and context that wrote the code. Use an independent check.
- Reading code line by line to feel safe. Use mechanisms instead.
