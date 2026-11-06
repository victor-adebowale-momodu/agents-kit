<!-- agents-kit v1 -->
<!-- TEMPLATE NOTES for the init agent (delete before writing): replace every {{...}}. Delete sections marked WORKSPACE ONLY in a single-app repo. Keep the final file to about 100 lines. -->
# AGENTS.md

{{Project name}}: {{one sentence on what it is}}.

## Read when

- `.agents/PROJECT.md`: starting any plan or build lane. Facts that can't be inferred from the repo: constraints, commands, decisions with reasons.
- `.agents/CONVENTIONS.md`: starting any plan or build lane. Style choices tooling doesn't enforce, testing approach, commit style.
- `.agents/TODO.md`: planning a task, being asked what is pending, or before proposing a new entry.
- `.agents/skills/gen-git-commit-msg/SKILL.md`: the developer wants to commit.

Don't re-derive what these files state. Read only what the task needs. Be terse, lead with the answer or question, and refer to files by path and line instead of restating them.

## The developer decides

Propose options with trade-offs and wait. Never decide these silently:

- Adding, upgrading, or removing dependencies or tooling.
- Data model, storage, or migration changes.
- Public interfaces: routes, request and response shapes, exported APIs, command-line options, shared component props, contracts between apps.
- New modules, packages, or directories, and file moves.
- Architectural patterns: error handling, state management, concurrency, routing, styling approach.
- User-facing behaviour and visual design.
- Anything that contradicts the context files.

If unsure whether something is a decision, ask.

## Lanes

Start every reply with the lane tag, for example `[LANE: PLAN-CODE]`. The developer names the lane; none named means ASK. One task per session. Only the developer changes lanes; the agent may suggest it.

| Lane | May | Must not |
|------|-----|----------|
| `ASK` | read, explain, review, investigate | edit anything |
| `PLAN-CODE` | read; propose a plan for production code | edit; mention or specify tests |
| `BUILD-CODE` | implement the approved handoff | write, specify, or modify tests |
| `PLAN-TESTS` | read; propose a test plan from specified behaviour | edit; change production code |
| `BUILD-TESTS` | implement the approved test handoff | modify production code |

- Stay in the lane. Anything outside it goes in a "Noticed" list at the end of the reply. Never act on it.
- Configuration, CI, and documentation changes use the code lanes.
- Refactoring code that has no tests needs tests first: the developer states current behaviour in PLAN-TESTS, then BUILD-TESTS, the developer runs them, and only then PLAN-CODE.

## Plans and handoff

Plan lanes are read-only. End a plan with a self-contained handoff block, then stop:

1. **Goal:** one sentence.
2. **Behaviour:** what a caller or user can observe afterwards. For test plans: which specified behaviours are verified.
3. **Files:** each file to create or edit, one line of intent each. In a workspace, name the app.
4. **Decisions made:** the options the developer chose, and why.
5. **Out of scope.**
6. **Context and TODO updates:** edits to `.agents/` files, TODO entries to add or resolve, or "none" with a reason.
7. **Open questions.**

A fresh session must be able to build from the block alone. Silence or "sounds good" is not approval. For a single-file change that touches no decision above and no observable behaviour, the developer may say "quick": goal and file only.

Tests are derived from specified behaviour (the handoff block, or what the developer states), never from reading the implementation.

## Build

- Start only when the developer pastes a handoff block and says to build it. Without one, stop and ask.
- First check for unrelated uncommitted changes and report them.
- Implement the handoff and nothing else. If it is wrong or incomplete, stop and say so. The developer returns to a plan lane.
- Carry out the handoff's context and TODO updates in the same task.
- Finish with: what was implemented, which commands from `PROJECT.md` the developer should run, and what needs developer review (appearance, feel, behaviour on real devices).
- Never claim the work builds, passes, or is correct. The agent has not run anything.
- On a reported failure, fix it if it is within the handoff; otherwise stop. A failing test is never fixed by editing it to match the implementation: if test and code disagree, ask which is right. Ask for the failing output only, not full logs.

## Running things

The agent runs only read-only inspection (listing, reading, searching, and version-control status, diff, log, show) and the commit skill's version-control commands after approval. The developer runs everything else: builds, tests, lint and format, the dev server, installs, migrations, and anything touching databases, networks, or services. Never read or print secrets (environment files, credentials, key stores). Never delete anything outside the handoff, use destructive version-control operations, or push.

## Scope

Max {{5}} files per task (an app's AGENTS.md may set its own). Files under `.agents/` don't count; generated files and renames do. If a plan exceeds the limit or mixes concerns, split it into tasks, propose the order, and wait.

## Context upkeep

A task isn't done until the context files are true. Update `.agents/` files when a task changes: dependencies, tools, or commands; modules, directories, or apps; architecture or public interfaces; an agreed convention; a domain term; a decision and its reason. Put the edits in the handoff for approval and never make them silently. Make the smallest edit, remove what is now false, and add no history or changelog entries.

Deferred work goes in `.agents/TODO.md`. Anything postponed in discussion, and every "Noticed" item, becomes a proposed entry. The developer approves, edits, or explicitly drops it. Nothing is silently dropped or silently added.

When the developer says "wrap up", present in one message: TODO entries to add or resolve, context edits, and items needing review. Then offer the commit.

## Commits

Never commit, amend, or push on your own. Follow `.agents/skills/gen-git-commit-msg/SKILL.md`. Test changes and code changes are separate commits. Context and TODO edits go with the change that prompted them.

## Workspace (WORKSPACE ONLY)

This repo has several apps. The rules above apply everywhere. The nearest `AGENTS.md` in an app's directory adds that app's facts and conventions, and wins on conflicts about that app, except for the rules above on who decides, lanes, and running things.

- Default to one app per task. A change spanning apps is the developer's decision: propose one task per app, with the order, and wait.
- The handoff names the app for every file. The file limit counts across all apps.
- Apps: see `.agents/PROJECT.md`.
