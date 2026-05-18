# Eval 2: Task - Build/Dependency Version Review (Old Skill)

## User Request

> "Write a task ticket to review and update outdated build and dependency versions in this repository, starting from `gradle/libs.versions.toml`. Capture scope, constraints, and outcome-focused acceptance criteria, but stop at the draft for my review."

## Preflight

- `gh --version` → 2.92.0 — installed and functional.
- `gh issue list --state all --repo AppOutlet/skills` → no existing issues. Duplicate check passed.

## Codebase Investigation

Explored the repository at `/Users/messias/Workspace/skills` (remote: `git@github.com:AppOutlet/skills.git`).

**Files read/directories inspected:**
- `README.md` — describes this as a skills repository for AppOutlet, containing skill definitions for OpenCode agents.
- `skills/delegate-to-jules/` — contains only `SKILL.md` and `evals/`.
- `skills/ticket-creator/` — contains `SKILL.md`, `assets/` (templates), and `evals/`.
- `AGENTS.md` — overview of available skills and tools.

**Search results (no matches):**
- `gradle/libs.versions.toml` — does not exist
- `**/*.gradle*` — no matches
- `**/*.toml` — no matches
- `**/package.json` — no matches
- `**/Makefile` — no matches
- `**/*.yaml` / `**/*.yml` — no matches
- `**/*.jsonc` — no matches
- `**/.tool-versions` — no matches

**Finding:** This repository contains no build configuration files, no dependency manifests, and no version catalog. The referenced `gradle/libs.versions.toml` path does not exist. The only files are skill definitions in Markdown, template assets, and eval metadata JSON files.

## Template Used

`assets/task.md` (task type inferred — operational/maintenance work: review and update dependency/version configuration).

## Ticket Type

`task` — the work is a maintenance/review activity, not a bug, feature, or spike.

## Draft

Presented to user as a fenced Markdown code block following the task template structure, with title, scope/constraints, acceptance criteria, and additional information reflecting codebase findings.

## Self-Review (pre-presentation)

- **Title:** Outcome-oriented ("Review and update tooling versions across skills repository")
- **Description:** Explains the "why" and scope boundaries clearly for someone with no context
- **Acceptance criteria:** Verifiable outcomes (inventory documented, gaps identified, updates applied or rationale recorded)
- **Weasel words:** None found — "outdated", "documented", "identified", "updated" are concrete with clear definition
- **Hidden scope:** None — explicitly scoped out introducing a new build system
- **All template sections used:** Description, Scope & Constraints, Scope, Acceptance Criteria, Additional Information

## Output

Draft was presented but NOT created (user asked to stop at draft for review). No `.md` file was written to disk during the process.
