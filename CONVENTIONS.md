<!-- agents-kit v1 -->
<!-- TEMPLATE NOTES for the init agent (delete before writing): record only choices tooling does not enforce. If a formatter, linter, or compiler decides it, name the tool and stop. Every line must come from the developer's answers; never import conventions from other languages or projects. Include only the app-type bullets that apply. Delete empty sections. In a workspace, this root file holds cross-cutting rules only; per-app specifics live in each app's AGENTS.md. Keep to about 80 lines. -->
# CONVENTIONS

## General

- {{Principles the developer stated, for example on naming or structure.}}

## Language-specific

One subsection per language used.

### {{Language}}

- Formatter and linter: {{names}}. Their configuration is the source of truth.
- {{Choices they don't enforce: naming, structure, error handling, async, typing.}}

## By app type

- Backend: {{interface conventions (validation, error shape, pagination); data access and migration rules; background work and retries}}.
- Frontend: {{component structure; where state lives; data fetching; styling system and tokens; accessibility; supported browsers and devices; copy and localisation}}.
- Command-line or library: {{public surface; compatibility promises; documentation of exported items}}.

## Testing

- Tests verify behaviour a caller or user can observe: return values, responses, rendered output and interactions, output text, emitted events. They don't assert internals such as private state, call order, or implementation details.
- Name each test for the behaviour it checks. Cover the main path, boundaries, invalid input, and the failure modes the behaviour implies.
- User interfaces: query the way a user would (role, label, visible text) and exercise interactions. Visual appearance is flagged for developer review, never asserted.
- Layout and naming: {{where tests live and how they are named}}.
- External dependencies in tests (database, network, browser): {{real or faked}}.
- {{Other test rules the developer states.}}

## Commits

Message style: {{the developer's convention, or "match recent history"}}. The commit skill's defaults apply otherwise.

## Task size (optional)

Max files per task: {{N}}. Overrides the default in `AGENTS.md`.
