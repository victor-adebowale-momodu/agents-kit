<!-- agents-kit v1 -->
<!-- TEMPLATE NOTES for the init agent (delete before writing): only facts an agent cannot infer from the repository. Every line must come from a file you read or an answer the developer gave; otherwise omit it. Skip anything a manifest, config, or README already states, and link to it instead. No dependency lists, no directory trees, no style rules a tool enforces. Delete empty sections and sections marked WORKSPACE ONLY in a single-app repo. Keep to about 80 lines. -->
# PROJECT

## Purpose

{{What this does and for whom, in two sentences. See the README for the rest.}}

## Apps (WORKSPACE ONLY)

| App | Path | Type | Purpose |
|-----|------|------|---------|

Each app's own `AGENTS.md` holds its facts and conventions.

How apps relate: {{contracts, shared packages, which app calls which, where shared definitions live}}.

## Decisions

One line each: what is used or done, and why, so it isn't second-guessed.

- {{Uses X because Y.}}

## Commands

The developer runs these. List only commands that are non-obvious or have prerequisites.

| Task | How it's run | Notes / prerequisites |
|------|--------------|-----------------------|

## Environment

What must exist locally (services, tools, accounts) and which configuration variables are needed. Names only, never values.

## Architecture

Only what the code doesn't make obvious: components and their boundaries, data flow, external services, contracts with other systems.

## Do not edit

Generated files, vendored code, lock files, anything managed by a tool: {{paths and why}}.

## Glossary

Domain terms an agent would otherwise misread. One line each.
