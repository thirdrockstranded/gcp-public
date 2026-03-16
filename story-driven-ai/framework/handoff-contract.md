# The Handoff Contract — v0.1

> The boundary between Design Mode and Direction Mode. Defines what Design Mode must produce before Direction Mode can begin.

---

## The Problem This Solves

Design Mode can produce many things — conversations, diagrams, vision docs, rough feature lists. Some of those are consumable by Direction Mode. Some aren't. Without a defined contract at the handoff, the gap gets filled with assumptions and the AI implementer fills ambiguity silently — it won't ask clarifying questions, it will just implement something plausible-looking.

The handoff contract is the answer to: *how do we know when Design Mode is done and Direction Mode can begin?*

---

## The Handoff Is Ready When You Can Answer Yes To All Of These

- [ ] Is the problem statement specific enough to be *wrong*? If it can't be wrong, it isn't specific enough.
- [ ] Are the boundaries defined — what's in scope, what is explicitly out of scope?
- [ ] Are the major components or feature areas identified at a high level?
- [ ] Are the guiding constraints captured — defaults, conventions, known risks, deferred decisions?
- [ ] **Can you write the first user story?** If yes, Design Mode has produced something Direction Mode can consume. If you're still unsure what the first story should be, it hasn't.

---

## The Handoff Artifact

The primary handoff artifact is **VISION.md** — the output of Design Mode in a form Direction Mode can reference throughout implementation.

### VISION.md Must Contain

| Section | Purpose |
|---|---|
| Problem statement | What is being solved and for whom |
| Core capabilities | What the system does — at feature area level, not implementation level |
| Explicit non-goals | What is out of scope — as important as what's in |
| Guiding constraints | Defaults, conventions, standards that affect implementation (e.g. "1/4 inch seam allowance", "imperial units first") |
| Future phases | Deferred decisions — captured so they don't leak into MVP scope |

### Direction Mode Input Requirement

Direction Mode requires:
1. A VISION.md that satisfies the above
2. At least one user story that references the vision and has testable acceptance criteria

If both exist, Direction Mode can begin. If either is missing or incomplete, return to Design Mode.

---

## The Re-Entry Problem

The boundary between Design Mode and Direction Mode is not a one-way door. Real projects surface design questions during implementation — a story reveals an unresolved structural decision, a constraint turns out to be wrong, scope needs to change.

When this happens, the flow is:
1. **Pause Direction Mode** — don't implement around the ambiguity
2. **Re-enter Design Mode** — resolve the structural question with the principal's judgment, with AI as thinking partner if useful
3. **Update VISION.md** — capture the resolution as a constraint or scope change
4. **Resume Direction Mode** — with the updated vision as the reference

The key discipline: never let Direction Mode resolve design questions silently. If a story can't be implemented without making a structural decision, that decision belongs in Design Mode first.

---

## Open Questions (v0.1)

- Does Design Mode need additional artifacts beyond VISION.md for larger or more complex systems? (Component diagrams, ADRs, risk registers?)
- Is the contract meaningfully different for additions to an existing codebase versus greenfield work?
- How granular should "major components or feature areas" be in the VISION.md to satisfy the contract?
- Should the first user story be written as part of Design Mode output, or is "can you write it?" sufficient as a readiness test?

---

## Relationship To Other Framework Documents

- **story-template.md** — defines the structure of Direction Mode's primary input artifact
- **scoring.md** — defines how Direction Mode output is measured
- **VISION.md** (in project repos) — the primary handoff artifact this contract governs

---

## Context Sufficiency — An Additional Readiness Test

Beyond the structural readiness checks above, the handoff is ready when the documentation passes a **context sufficiency test**:

> Could a capable but completely stateless AI implementer — with no memory of any prior session — be handed VISION.md plus a single user story and produce correct, coherent output?

If yes for at least the first story, Direction Mode can begin. If no — if correct implementation requires knowledge that lives outside those two documents — that missing knowledge needs to be captured before proceeding.

This is both a readiness test and a design discipline. Every piece of domain knowledge, every constraint, every upstream dependency that implementation requires should live explicitly in either VISION.md or the relevant story's Notes and Inputs sections. Not in your head. Not in a prior conversation. In the documents.

### What This Means For Story Writing

A story that passes the context sufficiency test:
- Does not require the AI to infer unstated constraints
- Does not assume knowledge from prior sessions
- Contains all domain knowledge needed in the Notes section
- References upstream stories explicitly rather than assuming shared context
- Has acceptance criteria specific enough that correct vs. incorrect output is unambiguous

### What Remains Open

How to handle **accumulated implementation state** — decisions made during implementation that affect downstream stories but weren't anticipated at story-writing time — is an unsolved problem not fully addressed by this contract. See `framework/context-management.md` for the current thinking on this open problem.
