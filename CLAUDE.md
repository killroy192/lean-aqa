# learn-ana

Learning program for a manual QA engineer (near-zero dev-tooling background) becoming an **AI-native automation QA (AQA) engineer**. This repo is documentation only: no application code, no build, no tests.

## Layout
- `ai-native-aqa-learning-plan.md`: the master plan. Source of truth for principles, skill map, timeline, tooling constraints and open items.
- `phases/README.md`: index of student guides.
- `phases/phase-0` … `phase-5-*.md`: one guide per phase (goal, what to learn, resources, projects, agent exercises, mentor drills, done-when, pitfalls).
- `phases/track-t-terminal-and-cs-literacy.md`: terminal, how software runs, containers, cloud (Weeks 1–9).
- `phases/track-m-mobile-aqa.md`: mobile AQA toolsets (Weeks 9–13).

## Core principles (do not contradict these when editing)
- She does **not** write or review application/test code line by line; agents generate code. Verification relies on mechanisms (mutation/planted bugs, gates, hooks, independent reviewer agents, CI), not code reading.
- Don't teach what an agent already does well enough, unless the user explicitly asks for deep expertise.
- **Deep expertise:** agent management and workflows, verification layers, test strategy under ambiguity, failure/flake diagnosis. Everything else is **literacy** (understand and direct).
- Terminal-first. Mobile and CS topics are scoped to AQA relevance only; no system architecture, design patterns, algorithms, native app development, or Kubernetes/IaC authoring.
- Tool constraints: Claude, open-source IDEs and orchestrators, allowlisted MCPs, CLIs. Don't recommend unapproved tools as required.

## Conventions
- Resources must be **free**, with A/B/C options per topic so the user picks. Labels: 📖 reading, 🎥 video, 🛠 hands-on, 📚 book/course.
- Keep every phase guide in the same section structure.
- Timeline is ~17 weeks; if a phase's weeks change, update the table in the master plan, `phases/README.md`, and the guide header.
- After adding or changing URLs, check them (e.g. `curl -s -o /dev/null -L -w '%{http_code}'`). Some sites return 403 to bots (Ministry of Testing, Google Cloud Skills Boost, LabEx); that doesn't mean the link is dead.
- Use the user's phrasing and decisions; don't re-open settled choices (listed above) without being asked.

## Open items (see master plan, section 11)
Playwright MCP allowlisting, approved orchestrator, mobile platform priority (Android/iOS, Mac availability), mobile MCP/device cloud approval, product app type, whether LLM evals should become deep expertise.
