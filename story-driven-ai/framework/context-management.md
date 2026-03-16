# Context Management — v0.1 (Open Problem)

> How the Principal Layer handles the fundamental constraint that AI implementers have no memory between sessions.

---

## Status

⚠️ **Open problem.** This is one of the most actively discussed unsolved problems in practical AI-assisted development. This document captures the current thinking, the hypothesis being tested, and the open questions. It will be updated as Quiltix implementation generates evidence.

---

## The Constraint

An LLM has no persistent memory between sessions. Every session starts from zero. The principal accumulates context over the life of a project — decisions made, constraints discovered, judgment calls during implementation, what changed from the original spec and why. The AI implementer has none of that unless it is explicitly provided every single time.

This is not a limitation that will be fully solved by better models. It is a structural property of how sessions work that the Principal Layer must account for.

---

## The Central Hypothesis

The story-driven approach may partially solve the context problem as a side effect of good specification discipline.

If each user story is written to be self-contained — explicit inputs, domain knowledge in Notes, upstream story references, testable acceptance criteria — then **VISION.md + the relevant story may be sufficient as the complete context payload for an implementation session.**

The unit of work becomes the unit of context. That is an elegant property if it holds.

This is directly testable in the Quiltix case study. Iteration 01 will reveal whether stories as written are self-contained enough, or whether additional context is needed to produce correct output.

---

## What The Documentation Structure Probably Handles

- Stable project facts — constraints, non-goals, guiding decisions (VISION.md)
- Feature-specific domain knowledge — conventions, calculations, edge cases (story Notes)
- Scope boundaries — what's in, what's out, what's deferred (VISION.md non-goals + future phases)
- Cross-story dependencies — when explicitly referenced in story Inputs

---

## What The Documentation Structure Probably Doesn't Handle (Yet)

**Accumulated implementation state** — the gap between what the story specified and what was actually built, including:
- Judgment calls made during implementation that affect downstream stories
- Constraints discovered during implementation that weren't anticipated at story-writing time
- Structural decisions that emerged from the code rather than the spec
- What changed, what was simplified, what was deferred mid-implementation

This is the category where context gets lost in practice. The story says "implement X." During implementation, you discover Y and Z, make three decisions, and simplify one acceptance criterion. The next session — and the next story — starts without any of that knowledge unless it is explicitly captured somewhere.

---

## Approaches Under Consideration

### Option A — DECISIONS.md
A running log in the project repo capturing implementation decisions as they are made. Each entry: what was decided, why, and what it affects downstream. The principal maintains this between sessions and includes it as context when relevant.

**Tradeoff:** Adds maintenance overhead. Value depends on discipline of capture. May duplicate information that lives in git commit history.

### Option B — Story Completion Notes
When a story is implemented, the principal annotates it with what actually happened — what changed from the spec, what decisions were made, what downstream stories are affected. The story becomes both specification and implementation record.

**Tradeoff:** Keeps context co-located with the spec. Adds a post-implementation step to the workflow. May clutter the story format.

### Option C — Session Handoff Notes
A lightweight note written at the end of each session summarizing what was done, what was decided, and what the next session needs to know. Included as context at the start of the following session.

**Tradeoff:** Low overhead. Ephemeral — not part of the permanent project record. Breaks down if sessions are far apart.

### Option D — The Codebase As Context
Feed relevant code files as context alongside the story and VISION.md. The implementation state is in the code — reference it directly.

**Tradeoff:** Works well for small codebases. Context window limits make this impractical as the codebase grows. Requires the principal to know which files are relevant.

---

## Open Questions

- Does Quiltix Iteration 01 confirm or refute the central hypothesis? Does VISION.md + story prove sufficient?
- Is accumulated implementation state actually a problem at the story level, or does it only become a problem at the epic/project level?
- Should the story template include a post-implementation annotation section?
- Is there a lightweight standard for what gets captured in a DECISIONS.md that makes it worth maintaining?
- Does the right answer differ for solo principals versus teams?

---

## Relationship To Other Framework Documents

- **handoff-contract.md** — includes a context sufficiency test as a readiness check
- **story-template.md** — Notes and Inputs sections are the primary context carriers at the story level
- **scoring.md** — test failures that suggest missing context (vs. wrong implementation) are a signal worth tracking separately
