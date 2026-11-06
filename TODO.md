<!-- agents-kit v1 -->
# TODO

Memory bank for deferred work: features postponed, gaps found, optimisations, known bugs, and decisions waiting on the developer. Read on demand; it is not loaded every session.

## How this file works

- One entry per line: `- T-<n> [app] <type>: <what and why>. Where: <path>. (<YYYY-MM-DD>)`
- `[app]` is used only in workspaces. Types: `feature`, `gap`, `optimise`, `bug`, `decision`.
- IDs only increase and are never reused. Say what is already known, so the entry is useful months later without re-investigating.
- Entries are added, edited, or dropped only with the developer's approval. Nothing is silently added or dropped.
- An entry is deleted in the task that resolves it. Version-control history is the record, and the commit may carry `Resolves: T-<n>`.
- Past about 150 lines, propose grooming: merge duplicates and drop stale items, each with the developer's approval.

## Open

_No entries yet._
