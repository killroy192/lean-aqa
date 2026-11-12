# Phase 1: Directing a coding agent (Weeks 2–4)

**Depth:** **Own** (agent management and workflow design). **Time:** ~3 weeks at 6–7 h. **Track T1 completes, T2 begins.**

## Goal
She can turn a vague request into a clear spec, get an agent to build it in small verified steps, and keep the solution simple. This is the core professional skill of the program.

## What to learn

### How agents work (concepts)
- [ ] Context window: what the agent "remembers", why long sessions degrade, when to restart
- [ ] Tools and permissions: read, edit, run commands, MCP tools
- [ ] Common failure modes: looping, scope drift, hallucinated APIs/files, over-engineering, claiming success without proof
- [ ] Models differ in speed, cost and capability; when to use which

### Task design
- [ ] Decomposing a task into small, checkable steps
- [ ] Writing a spec: goal, constraints, non-goals, acceptance criteria
- [ ] A **done-definition the agent can check itself** (a command that passes/fails)
- [ ] Asking the agent to plan first and reviewing the plan before it edits

### Context engineering
- [ ] `CLAUDE.md`: project conventions, commands, rules ("prefer the smallest change", "no new dependencies without asking")
- [ ] Skills and reusable prompts / slash commands
- [ ] Subagents (concept; used heavily in Phase 5)
- [ ] When to reset the session, summarize, or start fresh

### Interaction habits
- [ ] Plan mode before editing
- [ ] Small steps, frequent commits
- [ ] Asking "why did you choose this?" and "what is the simplest alternative?"
- [ ] Recognizing a stuck agent (repeated attempts, growing diff) and redirecting

## Resources

### Core reading (do these)
- 📖 Claude Code best practices — https://www.anthropic.com/engineering/claude-code-best-practices
- 📖 Claude Code docs: memory / `CLAUDE.md` — https://docs.claude.com/en/docs/claude-code/memory
- 📖 Anthropic: Building effective agents — https://www.anthropic.com/engineering/building-effective-agents

### Prompting and specs (pick one or two)
- **A.** 📖 Anthropic prompt engineering overview — https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview
- **B.** 📖 Anthropic: Effective context engineering for AI agents — https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- **C.** 🛠 GitHub Spec Kit (spec-driven development, read the README and try the flow) — https://github.com/github/spec-kit

### Courses (pick one)
- **A.** 📚 Anthropic Academy: "Claude Code in Action" and "AI Fluency" — https://anthropic.skilljar.com
- **B.** 📚 DeepLearning.AI short courses on agents / Claude Code — https://www.deeplearning.ai/short-courses/

### Terminal and runtime literacy for this phase (Track T)
- See [track-t-terminal-and-cs-literacy.md](track-t-terminal-and-cs-literacy.md), sections T1 and T2.

## Practical projects

### Project 1: The vague ticket (mentor-supplied)
The mentor gives one vague sentence, e.g. *"Users should be able to filter orders."* She must:
1. List the questions she needs answered (and note assumptions if no one is available).
2. Write a one-page spec with acceptance criteria and non-goals.
3. Ask the agent to produce a plan and review it.
4. Have the agent implement it in small steps, with commits, in a tiny sample app (the mentor provides one, or use a simple todo app the agent generates).
5. Check it with a command (tests, a script) that the agent can run on its own.

### Project 2: Her own `CLAUDE.md`
Write a `CLAUDE.md` for the practice repo with: how to run, how to test, coding style, "smallest change" rule, "ask before adding dependencies", "never claim done without running the check". Test it by asking for a task with and without the file; compare the results.

### Project 3: Break the agent on purpose
Give the agent an ambiguous or contradictory request and observe how it behaves (assumes? asks? invents?). Write down three failure modes you saw and a rule that would prevent each.

## Agent exercises
- Ask for a plan only; edit the plan yourself; then ask for the implementation.
- Ask the agent "what could go wrong with this change?" before running it.
- Restart a long session with a short summary of state and compare quality.
- Ask the agent for the simplest possible solution, then for an "enterprise" one, and compare the diff size.

## Mentor drills (weekly)
- **Week 2:** vague ticket → spec. Mentor critiques what is missing or untestable.
- **Week 3:** the agent has drifted (extra files, new dependency). She spots it from the diff summary and redirects.
- **Week 4:** over-engineered solution. She asks for a simplification with a measurable target (e.g. fewer files, no new dependency).

## Done when
- [ ] She turned a vague ask into a spec, a plan and a working feature with **no more than two redirections**
- [ ] The feature has a self-check command the agent runs on its own
- [ ] Her `CLAUDE.md` demonstrably changes agent behavior
- [ ] She can explain, in plain words, why a long session degrades and what she does about it
- [ ] Track T1 "done when" is met (find a failing line in a large log from the terminal)

## Pitfalls
- Writing prompts like conversation instead of specs. Ask: "Could another person build this from my text?"
- Treating the agent's confidence as evidence. Evidence is a passing check, not a statement.
- Huge tasks in one go. If the diff is too big to understand, the task was too big.
- Learning to code "properly" to review output. Not needed; build verification mechanisms instead (Phase 2).
