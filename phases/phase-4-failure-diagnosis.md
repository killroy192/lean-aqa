# Phase 4: Failure and flake diagnosis (Weeks 10–12)

**Depth:** **Own** (failure and flake diagnosis). **Time:** ~3 weeks at 6–7 h. **Track T3 supports this phase.**

## Goal
When a test fails, she can find out why from evidence (logs, traces, timing, environment), classify the cause, and direct an agent to fix the real problem. She rejects "fixes" that only hide it.

## What to learn

### The four categories
- [ ] **Product bug:** the app is wrong
- [ ] **Test bug:** the test is wrong (bad locator, wrong expectation, hidden dependency)
- [ ] **Environment issue:** data, config, network, version, resources
- [ ] **Flake:** non-deterministic; passes and fails with no change

### Evidence reading (no code reading required)
- [ ] CI logs: finding the first real error, not the last
- [ ] Playwright traces, screenshots, videos, network logs
- [ ] Timing: slow steps, timeouts, races
- [ ] Comparing a passing run and a failing run (what differs?)
- [ ] Reproducing locally vs in CI; why they differ (Track T2/T3)

### Common flake causes (concept level)
- [ ] Race conditions and unsynchronized waits
- [ ] Shared state and test order dependence
- [ ] Time, dates, random data
- [ ] External services and rate limits
- [ ] Resource limits in CI (CPU, memory, parallelism)
- [ ] Animations, async loading, network jitter

### Fix quality
- [ ] **Bad fixes:** adding `sleep`, retries without cause, loosening assertions, skipping the test
- [ ] **Good fixes:** waiting on a condition, isolating state, fixing data, stabilizing the environment
- [ ] When retries are acceptable, and how to track them

### Directing the agent
- [ ] "Investigate with evidence" prompts: ask for hypotheses, tests of each hypothesis, and what was ruled out
- [ ] Asking the agent to show the evidence for its conclusion
- [ ] Stopping the agent from guessing and changing five things at once

## Resources

### Flaky tests (pick two)
- **A.** 📖 Google Testing Blog, "Flaky Tests at Google and How We Mitigate Them" — https://testing.googleblog.com/2016/05/flaky-tests-at-google-and-how-we.html
- **B.** 📖 Martin Fowler, "Eradicating Non-Determinism in Tests" — https://martinfowler.com/articles/nonDeterminism.html
- **C.** 📖 Playwright "Best practices" (auto-waiting, avoiding flakiness) — https://playwright.dev/docs/best-practices

### Evidence tools
- 📖 Playwright Trace Viewer — https://playwright.dev/python/docs/trace-viewer
- 📖 Playwright debugging — https://playwright.dev/python/docs/debug
- 📖 GitHub Actions: monitoring and troubleshooting workflows — https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows
- 📖 GitHub Actions: downloading artifacts — https://docs.github.com/en/actions/how-tos/manage-workflow-runs/download-workflow-artifacts

### Systematic debugging (mindset, pick one)
- **A.** 📖 "Debugging" chapter notes from MIT Missing Semester (lecture "Debugging and Profiling") — https://missing.csail.mit.edu/2020/debugging-profiling/
- **B.** 📖 Julia Evans, "Debugging" posts and zines (some free) — https://jvns.ca

### Log reading in the terminal
- See Track T1 ([track-t-terminal-and-cs-literacy.md](track-t-terminal-and-cs-literacy.md)): `grep`, `tail`, `less`, `jq`.

## Practical projects

### Project 1: Failure museum (mentor-built)
The mentor prepares a repo with **5 seeded failures**, one each:
1. A real product bug
2. A stale locator (test bug)
3. A wrong environment value (e.g. missing env var / wrong port)
4. A race condition flake
5. A test-order dependence

For each one she writes a short report: what category, the evidence, the real cause, and the right fix. An agent investigates under her direction; she must not accept a conclusion without evidence.

### Project 2: Catch the bad fix
For each failure, ask the agent for a quick fix. Identify which "fixes" are bad (sleep, retry, loosened assertion). Then re-prompt for the correct fix and compare.

### Project 3: Flake hunt
Run the suite 20 times in CI or locally. Identify the flaky tests with a script or report (the agent writes it). Quarantine them with a ticket and a reason, then diagnose one fully.

### Project 4: Triage template
Create a one-page triage template (symptom, evidence, hypothesis, classification, owner, next action). Use it for every failure in this phase.

## Agent exercises
- "Compare run #1 (pass) and run #2 (fail). List every difference in logs, timing and environment."
- "Give three hypotheses for this failure and a cheap experiment to test each."
- "What would you do to prove the flake is caused by X, rather than assume?"
- "Rewrite this fix without using sleep or retries."

## Mentor drills (weekly)
- **Week 10:** two failures that look identical but have different causes. She separates them.
- **Week 11:** an agent confidently claims a root cause with weak evidence. She challenges it with the right question.
- **Week 12:** works locally, fails in CI. She names the category (version, resources, data, timing) before the agent fixes it.

## Done when
- [ ] She correctly classified all 5 seeded failures with evidence
- [ ] She rejected at least 2 bad fixes and got correct ones
- [ ] She can explain, in plain words, why a retry or sleep may hide a bug
- [ ] She has a reusable triage template and has used it ≥ 5 times
- [ ] She can read a CI log and a trace to locate the first real error

## Pitfalls
- Fixing the first symptom in the log; the first *error* is usually the cause, the last is often noise.
- Accepting "it's a flake" as an answer. A flake has a cause; find it or record that you couldn't.
- Letting the agent change multiple things at once. One hypothesis, one experiment.
- Ignoring the environment. Many "test bugs" are config or data issues.
