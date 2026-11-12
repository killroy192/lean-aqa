# Track T: Terminal-first and CS literacy (Weeks 1–9)

**Depth:** Literacy. **Time:** ~1 h/week alongside the main phases.
**Test for every topic:** does it help her direct agents, read logs or diagnose failures? If not, skip it.

## Overview

| Section | Weeks | Alongside |
|---|---|---|
| T1 Terminal and shell | 1–3 | Phases 0–1 |
| T2 How software runs | 3–5 | Phases 1–2 |
| T3 Environments, virtualization, cloud | 6–9 | Phases 2–3 |

---

## T1: Terminal and shell (Weeks 1–3)

### What to learn
- [ ] Navigation and files: `pwd`, `ls`, `cd`, `cat`, `less`, `cp`, `mv`, `mkdir`; absolute vs relative paths
- [ ] **Why `rm` is dangerous**; reading a command for risk (`rm -rf`, `sudo`, `curl ... | sh`, `--force`)
- [ ] Searching and filtering: `grep`, `find`, `head`, `tail -f`, `wc`, `sort`, `jq`
- [ ] Pipes (`|`) and redirects (`>`, `>>`, `2>`)
- [ ] Environment variables and `PATH`; `.env` files; what must never be committed
- [ ] Exit codes (0 = success) and why CI cares
- [ ] stdin / stdout / stderr
- [ ] Processes, background jobs, `Ctrl+C`, finding what uses a port
- [ ] File permissions at concept level
- [ ] What a shell script is and how to run one (the agent writes them)
- [ ] The CLIs she will meet: `claude`, `git`, `gh`, `curl`, `jq`, package manager, test runner, `docker`, cloud CLI

### Resources (pick one primary, one practice)
- **A.** 🎥 MIT Missing Semester, lectures "The shell" and "Shell tools and scripting" — https://missing.csail.mit.edu
- **B.** 📚 The Linux Command Line (free book, read Part 1 only) — https://linuxcommand.org/tlcl.php
- **C.** 🛠 Linux Journey (interactive lessons) — https://linuxjourney.com
- **Practice:** 🛠 OverTheWire "Bandit", levels 0–10 — https://overthewire.org/wargames/bandit/
- **Reference:** 📖 explainshell (paste a command, get an explanation) — https://explainshell.com
- **Cheat sheet:** 📖 tldr pages — https://tldr.sh

### Practice
- **Log haystack:** the mentor gives a 10,000-line log. Find the first error and its cause using only `grep`, `less`, `head`, `tail`.
- **Explain-before-run:** for 10 commands from the agent, say what each does and its risk, before approving.

### Done when
- [ ] She finds the failing line in a 10,000-line log from the terminal
- [ ] She explains a command the agent proposes, including its risk

---

## T2: How software runs (Weeks 3–5)

### What to learn
- [ ] Compiled vs interpreted vs JIT; what a **build step** is
- [ ] Runtimes (Python, Node, JVM) at concept level; "what version am I running?"
- [ ] Dependencies, package managers, lockfiles, version pinning
- [ ] **Virtual environments** and why "works on my machine" happens
- [ ] Paradigms (names and shapes): procedural, object-oriented, functional, event-driven, async
- [ ] Static vs dynamic types (what a type error looks like)
- [ ] Exceptions and stack traces: how to find the first relevant line
- [ ] State, side effects and why **determinism** matters for tests
- [ ] Data formats: JSON, YAML, env files, config layers
- [ ] Concurrency: processes vs threads, race conditions, timeouts
- [ ] HTTP basics: methods, status codes, headers, auth tokens, cookies
- [ ] DOM and locators: what the browser sees; CSS selectors vs accessibility roles
- [ ] Git concepts: commit, branch, diff, merge, conflict, revert (no memorized commands)

### Resources (pick one primary, others optional)
- **A.** 🎥 Crash Course Computer Science (watch ~10 episodes: software, programming languages, OS) — https://www.youtube.com/playlist?list=PL8dPuuaLjXtNlUrzyH5r6jN9ulIgZBpdo
- **B.** 📚 Harvard CS50x, Weeks 0–1 lectures only (concepts, how programs run) — https://cs50.harvard.edu/x/
- **C.** 📖 Crafting Interpreters, chapter 2 "A Map of the Territory" (compile vs interpret, no coding) — https://craftinginterpreters.com/a-map-of-the-territory.html
- **Python environments:** 📖 Python docs, "Virtual Environments and Packages" — https://docs.python.org/3/tutorial/venv.html
- **HTTP:** 📖 MDN "An overview of HTTP" — https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview
- **HTTP codes:** 📖 MDN HTTP status codes — https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
- **DOM and locators:** 📖 MDN "Introduction to the DOM" — https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction
- **DevTools:** 📖 Chrome DevTools overview — https://developer.chrome.com/docs/devtools
- **Git concepts:** 📖 Pro Git, chapters 1–3 (concepts) — https://git-scm.com/book/en/v2 ; 🛠 Learn Git Branching — https://learngitbranching.js.org
- **Paradigms:** 📖 Wikipedia "Programming paradigm" (skim the overview) — https://en.wikipedia.org/wiki/Programming_paradigm
- **Async:** 📖 MDN "Asynchronous JavaScript" (concepts only) — https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS

### Practice
- Ask an agent to explain a failing stack trace and point to the first relevant line. She verifies by finding it herself.
- Create and activate a virtual environment with the agent; break it (wrong version); fix it.
- Open DevTools → Network on a demo site; find a request, its status and its JSON response.
- Call an API with `curl` (the agent writes the command) and explain the response.

### Done when
- [ ] She explains in plain words why a test passes locally and fails in CI
- [ ] She can say whether a project needs a build step and what runtime it uses
- [ ] She reads a stack trace and a network request without help

---

## T3: Environments, virtualization and cloud (Weeks 6–9)

### What to learn
- [ ] VMs vs containers; image vs container
- [ ] Docker basics: `build`, `run`, `ps`, `logs`, `exec`, `stop`
- [ ] Docker Compose: running an app + database + test runner together
- [ ] Environment parity: why CI runs in containers; why local and CI differ
- [ ] Networking for testers: localhost, ports, DNS, HTTPS, proxies; "why is the service unreachable?"
- [ ] CI runners: hosted vs self-hosted, caching, artifacts, parallel jobs
- [ ] Cloud basics (AQA only): regions, compute, storage, managed services, ephemeral test environments
- [ ] Secrets managers, IAM and least privilege (concept)
- [ ] Cost drivers: what makes test infrastructure expensive

### Resources
**Containers (pick one)**
- **A.** 📖 Docker "Get started" — https://docs.docker.com/get-started/
- **B.** 🛠 Play with Docker (browser, no install) — https://labs.play-with-docker.com
- **C.** 📖 Docker Curriculum — https://docker-curriculum.com

**Docker Compose**
- 📖 Compose overview — https://docs.docker.com/compose/

**Networking (pick one)**
- **A.** 📖 How DNS works (comic) — https://howdns.works
- **B.** 📖 MDN "How the web works" — https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/How_does_the_Internet_work

**Cloud (pick one provider; concepts transfer)**
- **A.** 📚 AWS Cloud Practitioner Essentials (free digital course) — https://aws.amazon.com/training/digital/aws-cloud-practitioner-essentials/
- **B.** 📚 Microsoft Learn, "Azure Fundamentals" (AZ-900) — https://learn.microsoft.com/en-us/training/courses/az-900t00
- **C.** 📚 Google Cloud Skills Boost, "Cloud Digital Leader" learning path — https://www.cloudskillsboost.google

**CI runners and environments**
- 📖 GitHub Actions: runners — https://docs.github.com/en/actions/concepts/runners
- 📖 GitHub Actions: caching and artifacts — https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/caching-dependencies-to-speed-up-workflows

### Practice
- **Containerize the demo app** with an agent. Run the app and the test suite in containers.
- **Broken environment drill:** wrong Python version, missing env var, port in use. She names the category before the agent fixes it.
- **Works locally, fails in CI:** the mentor sets up a case with a version or resource difference. She finds the difference by comparing logs.
- **Cost estimate:** estimate monthly cost of running the suite on every PR for a team of 10 (agent drafts; she reviews assumptions).

### Done when
- [ ] She spins up the demo app and its dependencies in containers with an agent
- [ ] She reasons about why a CI job is slow or red (runner, cache, resources, parallelism)
- [ ] She explains containers vs VMs and local vs CI parity to a colleague in two minutes

---

## Explicitly out of scope
Software design patterns, system architecture, algorithms and data structures, Kubernetes and infrastructure-as-code authoring, writing application code.
