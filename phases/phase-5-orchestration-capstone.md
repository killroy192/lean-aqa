# Phase 5: Orchestration and capstone (Weeks 12–17)

**Depth:** **Own** (agent workflows at scale). **Literacy** for LLM evals and governance. **Time:** ~5 weeks.

## Goal
She runs several agents in parallel without losing control, automates triage with her sign-off, understands how AI features are evaluated and what governance requires, and pulls everything together in a capstone portfolio project.

## What to learn

### Orchestration
- [ ] When to parallelize and when not to (independent tasks, merge conflicts, review load)
- [ ] Subagents: specialized agents (test writer, reviewer, triager) with their own context
- [ ] Git worktrees or equivalent isolation so parallel agents don't collide (concept; agent runs commands)
- [ ] Handoffs: passing context between agents via files (specs, plans, summaries), not memory
- [ ] The approved orchestrator tooling at work (ask mentor); how to see what each agent is doing
- [ ] Cost and time: when more agents are not better

### MCP and tool access (literacy)
- [ ] What MCP is; how an agent gets browser, mobile or issue-tracker tools
- [ ] Allowlisting, permissions and why least privilege matters
- [ ] Risks: prompt injection from page content, over-broad access, data leaving the company

### AI-assisted triage
- [ ] Pipeline: failure → evidence collection → hypothesis → classification → draft bug report → human sign-off
- [ ] What the human must verify before filing (reproduction, severity, duplicates)
- [ ] Avoiding noisy auto-filed tickets

### LLM evals (literacy)
- [ ] Why testing AI features differs: non-determinism, no single right answer
- [ ] Eval datasets, rubrics, assertions that tolerate variation
- [ ] LLM-as-judge and its biases
- [ ] Regression tracking over model/prompt changes
- [ ] Red-teaming and prompt-injection basics

### Governance (literacy)
- [ ] Data handling: no customer data or secrets in prompts
- [ ] Secrets management and `.env` hygiene
- [ ] Cost control: budgets, model choice, caching
- [ ] Audit trail: what an agent did and why (logs, commit history, session summaries)
- [ ] Approved-tools-only policy

## Resources

### Orchestration and multi-agent
- **A.** 📖 Claude Code subagents — https://docs.claude.com/en/docs/claude-code/sub-agents
- **B.** 📖 Anthropic, "How we built our multi-agent research system" — https://www.anthropic.com/engineering/multi-agent-research-system
- **C.** 📖 Git worktrees (concept) — https://git-scm.com/docs/git-worktree
- **D.** 🛠 Open-source orchestrators (only if approved): Claude Squad — https://github.com/smtg-ai/claude-squad

### MCP
- 📖 Model Context Protocol intro — https://modelcontextprotocol.io/introduction
- 📖 Claude Code MCP docs — https://docs.claude.com/en/docs/claude-code/mcp
- 📖 Playwright MCP — https://github.com/microsoft/playwright-mcp

### Evals (pick one tool and one reading)
- **Reading:** 📖 Anthropic, "Define success criteria and build evaluations" — https://docs.claude.com/en/docs/test-and-evaluate/develop-tests
- **Tool A:** 🛠 Promptfoo — https://www.promptfoo.dev/docs/intro
- **Tool B:** 🛠 DeepEval — https://deepeval.com/docs/getting-started
- 📖 OWASP Top 10 for LLM applications — https://genai.owasp.org/llm-top-10/

### Governance
- 📖 Claude Code security and permissions — https://docs.claude.com/en/docs/claude-code/security
- 📖 Claude Code IAM / permissions — https://docs.claude.com/en/docs/claude-code/iam
- 📖 GitHub secret scanning (concept) — https://docs.github.com/en/code-security/secret-scanning/introduction/about-secret-scanning
- Company policy on AI tool usage (ask mentor; required reading)

## Practical projects

### Project 1: Parallel agents
Pick a backlog of 3–4 independent test tasks (e.g. different features of the demo app). Run agents in parallel, each with its own spec, branch/worktree and self-check. She reviews results through the verification layer, merges, and records what went well and badly (conflicts, cost, quality).

### Project 2: Reviewer subagent
Create a reviewer subagent with a prompt that checks work *against the spec* and flags weakened assertions, new dependencies and scope drift. Run it on Project 1's outputs and compare with her judgment.

### Project 3: Triage automation
Build a flow where failed CI runs trigger an agent that collects logs/traces, proposes a classification, and drafts a bug report. She signs off before anything is filed. Measure: how often is the draft right? What does she correct most?

### Project 4: Eval suite (literacy-level)
Pick a small LLM feature (e.g. a summarizer or a chat answer). Write 15–20 eval cases with rubrics, run them with Promptfoo or DeepEval, change the prompt, and compare results. Document one case where the judge was wrong.

### Project 5 (CAPSTONE)
An end-to-end workflow, documented in a public repo:
1. **Input:** a vague requirement from the mentor.
2. **Spec:** questions, assumptions, acceptance criteria.
3. **Strategy:** risk-based plan with automation decisions.
4. **Build:** agent-built tests (web + a small mobile smoke suite from Track M).
5. **Verification layer:** self-checks, mutation or planted bugs, gates, independent reviewer.
6. **CI:** runs on every pull request with artifacts.
7. **Failure:** a seeded failure triaged using evidence, with a report.
8. **Governance notes:** secrets handling, cost estimate, tool allowlist, audit trail.
9. **Decision log:** what she decided and why, including what she rejected from the agent.

## Agent exercises
- "Split this backlog into independent tasks and say which can run in parallel."
- "Write a handoff note for another agent to continue this work."
- "What could be injected through page content that would change your behavior?"
- "Draft an eval rubric for this feature and list the ways the judge could be wrong."

## Mentor drills
- **Week 13:** two parallel agents produced conflicting changes. She resolves it and changes the workflow to avoid the problem.
- **Week 14:** an auto-drafted bug report that looks plausible but is wrong. She finds the error.
- **Week 15:** a page with hidden text trying to steer the agent (prompt injection). She spots it in the transcript and states the control.
- **Week 16–17:** capstone review. She walks through her workflow and decisions, not code.

## Done when
- [ ] She ran ≥ 3 agents in parallel and documented outcomes and costs
- [ ] A reviewer subagent exists, tested on real output
- [ ] Triage automation works with human sign-off and measured accuracy
- [ ] She ran a small eval suite and can explain LLM-as-judge limits
- [ ] The capstone repo is public (or mentor-accessible), complete and reproducible
- [ ] She can state the governance rules she followed and why

## Pitfalls
- More agents ≠ more quality. Review capacity is the bottleneck.
- Auto-filing bugs. Always keep a human sign-off.
- Giving broad tool access "to make it work". Start with least privilege.
- Treating eval scores as truth. Examine failures and judge disagreements.
- Skipping the decision log. It is what shows judgment to employers.
