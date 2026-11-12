# Phase 0: Setup and orientation (Week 1)

**Depth:** Literacy. **Time:** ~6–7 hours. **Track T1 (terminal) starts here.**

## Goal
Get a working workspace and have a first supervised session with a coding agent. She should finish the week unafraid of the terminal, project folders and logs.

## What to learn
- [ ] What a **repo**, **branch**, **commit** and **remote** are (concept only)
- [ ] What a **terminal**, **shell** and **command** are, and how to open one
- [ ] Vocabulary: dependency, environment variable, process, port, log, config file
- [ ] How to open a project folder in the IDE and look around without fear
- [ ] How to start Claude Code in a project folder and ask it questions
- [ ] How to read a command the agent proposes *before* approving it
- [ ] What the permission prompts mean (read, edit, run command) and when to say no

## Setup checklist (the agent does the installing; she asks it to explain each step)
- [ ] GitHub account, with two-factor authentication enabled
- [ ] Open-source IDE (VS Code or approved fork)
- [ ] Git and `gh` (GitHub CLI), signed in
- [ ] Claude Code installed and signed in
- [ ] Node.js and Python installed (the agent checks versions and installs them)
- [ ] Approved MCPs configured (ask the mentor for the allowlist)
- [ ] A practice folder, e.g. `~/dev/learn-qa`

## Resources

### Terminal and project orientation (pick one)
- **A.** 🎥 MIT Missing Semester, lecture 1 "Course overview + the shell" — https://missing.csail.mit.edu/2020/course-shell/ (and the tools site at https://missing.csail.mit.edu)
- **B.** 🛠 Linux Journey, "Command Line" section — https://linuxjourney.com
- **C.** 🛠 Terminal games: OverTheWire "Bandit", levels 0–5 only — https://overthewire.org/wargames/bandit/

### Git and GitHub concepts (pick one)
- **A.** 🛠 GitHub Skills, "Introduction to GitHub" — https://skills.github.com
- **B.** 📖 GitHub Docs, "Hello World" — https://docs.github.com/en/get-started/start-your-journey/hello-world
- **C.** 🛠 Learn Git Branching, first two levels only — https://learngitbranching.js.org

### Claude Code first steps (do the official one, add one more if wanted)
- **Required:** 📖 Claude Code overview and quickstart — https://docs.claude.com/en/docs/claude-code/overview
- **Option A:** 📚 Anthropic Academy course "Claude Code in Action" (free, sign-up) — https://anthropic.skilljar.com
- **Option B:** 🎥 DeepLearning.AI short course on agentic coding with Claude Code — https://www.deeplearning.ai/short-courses/

### IDE basics (only if unfamiliar)
- 📖 VS Code "Getting Started" — https://code.visualstudio.com/docs/getstarted/getting-started

## Practical project: "Hello, agent"
1. Create a folder and run `git init` (ask the agent to explain what that did).
2. Start Claude Code in it. Ask it to create a simple `README.md` and a tiny script that prints today's date.
3. Ask it to explain each file and each command it ran.
4. Commit the files and push them to a new GitHub repo using `gh`. Read every command before approving.
5. Open the project in the IDE. Find the files, the terminal panel and the git panel.

## Agent exercises
- "What is this project and how do I run it?" in a folder with a small existing project. Verify the answer by running it.
- Ask the agent to run a command that fails (e.g. a wrong path). Ask it to explain the error in plain words.
- Deliberately ask for something risky ("delete these files") and observe the permission prompt.

## Mentor drills
- **Explain-before-run:** the mentor shows three commands, one of which is risky (`rm -rf`, `sudo`, `curl ... | sh`). She identifies which and why.
- **Orientation:** open an unfamiliar repo. In 10 minutes, find the README, the tests folder and the config file, and say what the project does.

## Done when
- [ ] She has a pushed GitHub repo created through the terminal
- [ ] She can explain what each command in the session did, in her own words
- [ ] She can answer "what is this project and how do I run it?" for a new repo, with the agent's help, and sanity-check the answer
- [ ] She says no to at least one agent action and can explain why

## Pitfalls
- Approving everything without reading. Slow down; this habit is the foundation of every later phase.
- Trying to memorize commands. She does not need to. She needs to understand what a command *does*.
- Perfecting the setup. Good enough is fine; ask the mentor if something is blocked more than 30 minutes.
