# Cursor: High-Leverage, Low-Effort Ways To Go Faster

This repo tracks how to get the most leverage out of Cursor with minimal effort, plus some more ambitious ideas once the basics are tight. Everything here is aimed at shipping faster with fewer regressions and cleaner diffs.

## Principles
- Constrain scope. Small, precise tasks beat broad, vague asks.
- Provide context. Link files, commands, failing output, and constraints.
- Close the loop. Generate → review diff → run checks → iterate.
- Bias to tests. Use failing tests (or examples) to anchor changes.
- Prefer repeatable workflows. Encode habits in rules, templates, and scripts.

## Do Today (90 minutes, big ROI)
1) Create `.cursorrules` to teach Cursor the project
```text
# .cursorrules (root)
# Purpose: Give Cursor default context so prompts can be short.

# Project overview
- Stack: <language/framework/tools>
- Build: <commands>
- Test: <commands>
- Run: <commands>

# Style & constraints
- Code style: <formatter/lint rules>
- Architectural boundaries: <modules that shouldn’t be crossed>
- Safety: Prefer minimal diffs; don’t change unrelated files; keep naming.
- Tests first when fixing bugs; propose test changes explicitly.

# Working agreements with the AI
- Explain assumptions in one sentence max.
- If unsure, ask for one clarifying question before proceeding.
- When refactoring, preserve behavior; list risks.
- For multi-file edits, summarize each file’s change in one line.
```

2) Add a one-page `CONTEXT.md` for fast grounding
```markdown
# CONTEXT
- What this project does in one paragraph
- Key domains/modules and how they fit
- Where to run, test, lint
- Links to architecture diagrams or docs (if any)
- Known tricky areas and gotchas
```

3) Standardize commands so Cursor can use them
- Add a `Makefile` or `justfile` exposing: `setup`, `run`, `test`, `lint`, `fmt`, `typecheck`.
- Put these in `README.md` so the model sees them during context windows.

4) Create a `prompts/` folder with reusable patterns
- `prompts/surgical-fix.md`: small, single-file fixes with constraints.
- `prompts/spec-to-code.md`: spec-first flow for new features.
- `prompts/refactor-safe.md`: behavior-preserving refactors.
- `prompts/test-first.md`: write failing test then implement.
- `prompts/review-diff.md`: strict diff review rules before apply.

5) Add a lightweight “Working With Cursor” section to `README.md`
- How to start a session, what to paste (errors, file paths), what to expect.

## Reusable Prompt Patterns (copy/paste)

Surgical Fix (smallest viable change)
```text
Goal: <what must be true when done>
Scope: Only touch <file(s)>. Do not change public APIs.
Constraints: Minimal diff, preserve naming, keep style.
Given:
- Command to repro: <command>
- Failing output: <paste>
- Relevant code: <paths or snippets>
Deliver:
- Brief reasoning (1–2 lines), then the patch.
- If the fix spans files, list one-line summary per file.
```

Spec → Code (feature stub → implementation)
```text
Spec:
- User story / acceptance criteria
- Inputs/outputs with examples
- Non-goals and constraints
Request:
- Propose file changes (list), then implement in small steps.
- Add/extend tests to cover acceptance criteria.
- Ask 1 clarifying question if any ambiguity remains.
```

Behavior-Preserving Refactor
```text
Objective: Improve <readability/structure/perf> without changing behavior.
Guardrails: Keep public APIs stable; retain tests; small commits.
Checklist:
- Identify seams to isolate
- Propose rename/move plan
- Apply changes in atomic steps
- Note risks and quick rollbacks
```

Diff Review (before applying large changes)
```text
Before apply, provide:
- Files changed list
- One-line rationale per file
- Risky areas to double-check
- Any commands I should run to validate
```

Test-First Fix
```text
Write a failing test that reproduces the bug in <file>.
Then implement the minimal fix; keep the diff tight.
Explain the failure mechanism briefly (one sentence).
```

## Daily Usage Playbook
- Kickoff (2–3 min): Paste `CONTEXT.md` summary or remind Cursor where tests/run live.
- Frame tasks narrowly: “Edit only X and Y; do not touch Z.”
- Always paste failing output and the exact command to repro.
- Keep change sets < ~100 lines where possible; split otherwise.
- Close loops: after each patch, run `test`/`lint`/`typecheck` and feed output back.

## Guardrails That Save Time
- Always specify file paths and scope.
- Ask for “reasoning in 1–2 lines” max to reduce fluff.
- Require a “files changed summary” for multi-file edits.
- Use a standard commit message template to keep history readable.

Commit Template
```text
<type>(<scope>): <summary>

Rationale:
- Why this change
Validation:
- Commands run and outcomes
Notes:
- Breaking changes or follow-ups
```

## Tooling That Multiplies Cursor
- `Makefile`/`justfile` targets make actions discoverable to the model.
- Lint/format/typecheck configured and documented.
- Short `ARCHITECTURE.md` diagram or bullets improves global reasoning.
- Small example datasets or fixtures to demo features and tests.

## Metrics (prove ROI)
Track for 2 weeks:
- Time from “bug discovered” → “PR ready”.
- % of changes shipped with new/updated tests.
- Average diff size per task.
- Number of AI iterations per task (aim to reduce with better prompts/context).

## Ambitious (after basics stick)
- Knowledge Pack: curate `docs/` with mini overviews of domains; link from `.cursorrules`.
- Change Budgeting: enforce a max diff policy per patch to keep iterations snappy.
- Code Generation Pipelines: define module scaffolds (CLI to create files + tests) then let Cursor fill internals.
- Typed Everywhere: add type hints/TS to improve model and human correctness.
- Regression Nets: snapshot tests for key flows to unlock bolder refactors with AI help.
- Repo Bots: lightweight scripts to validate PRs locally (lint/test/typecheck) and summarize results for Cursor discussions.

## Next 3 Concrete Steps
1) Add `.cursorrules` and `CONTEXT.md` (start minimal; iterate).
2) Introduce `Makefile`/`justfile` with `run`, `test`, `lint`, `fmt` targets.
3) Create `prompts/` with the 4 templates above and start using them daily.

---
If you want, I can scaffold `.cursorrules`, `CONTEXT.md`, and a `Makefile` tailored to your stack—just tell me the language/framework and your usual commands.
