<!-- agents-kit v1 -->
# Initialise agent context for this repository

You are setting up a minimal context system so future sessions don't re-explore this repo. I (the developer) make every decision. You ask, draft, and wait. Treat this repository as if it has never had an agent system. Do not edit or delete anything before step 7.

## Master files (outside the repo)

- `~/.agents/templates/`: `AGENTS.md`, `APP_AGENTS.md`, `PROJECT.md`, `CONVENTIONS.md`, `TODO.md`.
- `~/.agents/skills/gen-git-commit-msg/SKILL.md`: the commit skill.

If you cannot read these, tell me and stop. Do not recreate them from memory.

## Steps

1. **Preflight.** Check the version-control status. If there are uncommitted changes, stop and tell me to commit or stash them first. If the repo is not under version control, warn me that the discard in step 2 cannot be undone and continue only with my explicit confirmation.

2. **Find and discard the old setup.** List, without opening them, every instruction or context file written for an agent: root or nested files such as `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, local or override variants, rule files and rule folders for any editor or agent, copilot instruction files, and the context files inside any `.agents/` folder. Show me the list. Do not touch tool settings, permissions, hooks, connector configuration, or any skills other than the commit skill, including those inside `.agents/skills/`. Ask once: "Discard these? They stay in version-control history." Anything I tell you to keep is skipped; everything else is removed in step 7. Do not read their content and do not carry anything over. If I want something remembered, I will tell you in my own words.

3. **Work out the shape.** Decide from the repo contents:
   - **Empty or no source** (greenfield): go to the interview in step 4b.
   - **Existing code, one app**: one set at the root.
   - **Existing code, several apps**: look for workspace or monorepo configuration files, or several independent project manifests in subdirectories. Ask me to confirm the list of apps, each app's path, and its type (backend, frontend, mobile, command-line, library, other).

4. **Gather.**
   - **4a. Existing repo.** Read only manifests, task-runner and CI files, tool configuration files, and the opening of the README. Do not read source files. Do not read secrets or environment files; their names are enough.
   - **4b. Greenfield.** Interview me on purpose, language and runtime, frameworks, package manager, test tooling, formatter and linter, and app structure. For each choice give two or three options with trade-offs, and let me decide. Pick nothing yourself. Do not scaffold the project; this step only sets up context files.

5. **Interview for what the repo can't tell you.** Ask in at most two grouped rounds, skipping anything already answered:
   - Purpose, and domain terms an agent would misread.
   - Non-obvious commands and their prerequisites; local services and configuration variable names.
   - Decisions and their reasons that must not be undone.
   - Generated, vendored, or tool-managed paths not to edit.
   - Style choices that tooling doesn't enforce; how tests are laid out and what is real or faked in them.
   - Commit message style, and the max number of files per task (default 5; per app if they differ).
   - Known deferred work, bugs, or gaps, which become `TODO.md` entries.

6. **Draft from the templates.** Produce, in this order:
   - `AGENTS.md` at the root. In a single-app repo, delete the WORKSPACE ONLY section.
   - `.agents/PROJECT.md`, `.agents/CONVENTIONS.md`, `.agents/TODO.md`.
   - In a workspace: one nested `AGENTS.md` per app from `APP_AGENTS.md`.

   Rules:
   - **Traceability.** Every line must come from a file you read or an answer I gave. Otherwise omit it. Never invent commands, versions, or conventions, and never propose conventions I didn't state; ask instead.
   - **Lean.** Leave out anything a manifest, config, or the README already says, dependency lists, directory trees, and rules a formatter or linter enforces. Link instead of copying.
   - **Strip** the template notes and unused placeholders. Keep the `agents-kit` version stamp at the top of each file.
   - `TODO.md` keeps its "How this file works" section. Replace the placeholder under "Open" with the entries I approved, or leave it as it is if there are none.
   - **Budget.** About 100 lines for `AGENTS.md` and about 80 for each other file, with root and nested files together under 32 KiB. Each first version is minimal; lines are added later when an agent repeatedly gets something wrong.
   - Show me the drafts and any unresolved questions, then wait for my answers and approval.

7. **Ask three more things, then write.**
   - Should `.agents/` and `AGENTS.md` be committed, or kept out of version control locally using the repository's local exclude list rather than the shared ignore file?
   - Which agent tools do I use?
   - Confirm the max-files-per-task number.

   After I answer, remove the old files from step 2, write the files from step 6, and copy the commit skill verbatim to `.agents/skills/gen-git-commit-msg/SKILL.md`. Create no other files, apart from the pointer files in step 8.

8. **Tool compatibility.** For each tool I named:
   - **Claude Code:** create a `CLAUDE.md` containing only the single line `@AGENTS.md`, which imports it. Never add other content, because an existing `CLAUDE.md` takes the place of `AGENTS.md` unless it imports it. Claude Code finds the commit skill through the user-level link made when `~/.agents` was installed; if I haven't made that link, tell me to.
   - **Gemini CLI:** tell me to add `AGENTS.md` to its context file list in its settings. I make that change; you don't edit user-level settings.
   - **Anything else:** nothing is needed if it reads `AGENTS.md`. If I name a tool and you don't know how it loads instructions, say so instead of guessing.

9. **Finish.** List the files created or removed with their line counts. Do not commit. Tell me the commit skill is ready, and suggest a pilot: run three to five real tasks with these files and, if practical, the same tasks without them, noting tokens used, time, and whether I had to rework the result. Cut lines that don't earn their place.

## Constraints

- Don't run builds, tests, installs, or anything that changes state beyond steps 7 and 8.
- Don't read or print secrets.
- Don't create override or local variants of instruction files.
- If unsure whether something is mine to decide, ask.
