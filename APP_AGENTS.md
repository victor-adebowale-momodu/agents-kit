<!-- agents-kit v1 -->
<!-- TEMPLATE NOTES for the init agent (delete before writing): nested AGENTS.md for ONE app in a workspace. Only facts the agent can't infer from that app's repo contents. Every line must come from a file you read or an answer the developer gave. Delete empty sections. Keep to about 80 lines. If it overflows, move the overflow into a `.agents/` folder inside the app and point to it with a "Read when" line. -->
# {{App name}} (app-level AGENTS.md)

Adds to the root `AGENTS.md` and applies only inside this directory. Type: {{backend | frontend | mobile | command-line | library | other}}. Purpose: {{one sentence}}.

## Facts

- {{Constraint, decision, or non-obvious fact, with the reason.}}
- Boundaries: {{contracts this app provides or consumes, and with which apps}}.
- Do not edit: {{generated or tool-managed paths, and why}}.

## Commands

The developer runs these. List only commands that are non-obvious or have prerequisites.

| Task | How it's run | Notes / prerequisites |
|------|--------------|-----------------------|

## Conventions

Only choices that tooling doesn't enforce. Name the formatter and linter and stop.

- {{Language-specific and app-type choices the developer stated.}}
- Testing: {{where tests live, how they are named, what is real vs. faked in tests}}.

## Task size (optional)

Max files per task: {{N}}. Overrides the root default.
