---
name: gen-git-commit-msg
description: Generate git commit messages, but only after the developer proves they understand the changes by explaining them in their own words. Once they do, present every commit and its message together for a single approval, then make all the commits. Use whenever the user wants to commit, asks for a commit message, says "commit this", "write a commit", or "wrap up", or finishes a task with uncommitted changes. Never commits before the understanding check and the approval. Trigger even if they ask you to just commit quickly.
---
<!-- agents-kit v1 -->

# gen-git-commit-msg

The developer must understand every change before it is committed. The understanding check happens once, up front. After it, there is one approval, not a back-and-forth per commit. Never skip the check, even if asked to hurry.

## Hard rules

- Before the plan is approved in step 5, do not commit, amend, push, or bypass hooks.
- Do not show your own summary of the changes before the developer has given theirs.
- Stage only the files each commit lists. Never stage everything unless the developer says so.
- Be terse. Don't repeat the developer's explanation back, and don't re-show diffs after approval.

## Steps

### 1. Show the raw facts only

Show the version-control status (including untracked files) and the diff stat for staged and unstaged changes. Add no interpretation, no summary, no hints.

Then flag, in one line each, only the ones that apply:

- The change touches more files than the limit in `AGENTS.md` (or the app's own limit).
- The diff changes dependencies, commands, layout, architecture, or conventions but no `.agents/` file is among the changes. The context may be stale.
- The change appears to resolve a `.agents/TODO.md` entry that is still listed.
- Tests and production code are mixed. They will go in separate commits.

### 2. Ask for their explanation, once

Ask the developer to explain, in their own words, covering all the changes:

- What changed, file by file or area by area.
- Why it changed.
- Anything risky, surprising, or left unfinished.

Then wait. Do not offer a draft explanation.

### 3. Check it against the real change

Read the diff, and read the untracked files directly, since a diff doesn't include them. Compare with their explanation. Look for:

- Changed or new files they did not mention.
- Things they described that are not in the change.
- Wrong cause, wrong effect, or wrong behaviour.
- Vague answers ("fixes the bug", "cleanup", "updates logic"). Reject these and ask what specifically.

If gaps exist, say *where* to look (file, function, area) and ask them to revise. Do not hand over the answer. If they are still stuck after two rounds, explain the specific gap briefly, then ask them to restate it.

### 4. Confirm understanding

When their explanation accurately covers the change, say so in one line. Minor wording imprecision is fine; misunderstanding of behaviour is not. Ask nothing further about the changes.

### 5. Present the whole commit plan at once

Group the changes into the fewest commits that follow these rules:

- One reviewable concern per commit. Don't split further than that.
- Test changes and code changes are separate commits.
- `.agents/` context and TODO edits go with the change that prompted them.

Message style: use the style in `.agents/CONVENTIONS.md` if it states one. Otherwise match recent history (look at the last ten commit subjects). Failing both, use a subject in the imperative, under 72 characters, no trailing period, and a body wrapped at about 72 columns that explains why the change was made and what it does. Build the body from the developer's own explanation. Add a final line `Resolves: T-<n>` if a TODO entry is resolved, then a final trailer line `Assisted By: <agent> (<model>)`, unless the style above says otherwise.

Show one numbered plan. For each commit: the files, then the full message. Then ask once: approve all, or what to change. The developer may edit a message, merge commits ("make it one"), or move files between commits. Redo only the affected entries and ask again, once.

### 6. Execute everything

On approval, make all the commits in order in one sequence, with no further prompts. If a hook fails, stop, report which commit failed and why, and do not bypass it. When done, report one line per commit: hash and subject. Nothing else.
