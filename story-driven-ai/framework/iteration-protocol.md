# Iteration Protocol

> How a user story moves from specification to verified implementation through scored iteration.

---

## The Loop

A story is not "done" when code is generated. It is done when all acceptance criteria are verified by automated tests. The iteration protocol defines how that verification works and what happens when it fails.

```
Smoke test gate → Read story → Ask clarifying questions → Plan → Implement on branch
     → Generate tests → Run tests → Score → Pass? Done. Fail? Iterate.
```

---

## Smoke Test Gate

Before beginning implementation on any story, run the existing test suite against the current state of `develop`:

```
docker compose --profile test run test
```

**If smoke tests pass:** proceed to story implementation.

**If smoke tests fail:** stop. Report the failures to the developer before touching the story. Infrastructure issues must be resolved at the infrastructure level, not papered over during story implementation.

**Rationale:** Latent infrastructure failures discovered mid-story (broken container builds, version mismatches, host header rejections) block all AC verification and contaminate the session document with out-of-scope debugging. Catching them before implementation begins keeps the story session clean and the session document focused on methodology-relevant observations.

*Added after US-001 (Quiltix case study): two pre-existing infrastructure failures — a Playwright version mismatch and a Vite 5.4 `allowedHosts` enforcement change — blocked all e2e AC verification and required diagnosis before story testing could proceed. See META-1, META-2, META-3 in the US-001 session document.*

---

## Iteration Limit

Each story is attempted a maximum of **5 iterations** before escalating to the developer.

| Outcome | Definition |
|---------|------------|
| **Pass** | 100% of AC-mapped tests passing |
| **Escalate** | 5 iterations completed without 100% pass rate |

On escalation, Code reports back with the full iteration log, the highest score achieved, and the specific ACs that could not be satisfied. The developer reviews and decides: refine the story, adjust the acceptance criteria, or accept partial completion with documented gaps.

---

## What Resets Between Iterations

Each iteration attempt within a story run gets:
- The original story file (unchanged — stories are read-only)
- The session notes from all previous attempts for this story (cumulative context)
- The test results from the previous attempt (what failed and why)

Each iteration does **not** get:
- A clean branch — iterations build on the same feature branch
- Permission to modify the story file to make tests easier to pass

The goal of each iteration is to improve the implementation, not to lower the bar.

---

## Scoring Per Iteration

Each iteration is scored against the AC-to-test map defined in the story.

```
iteration_score = passing_ac_tests ÷ total_ac_tests × 100
```

A story passes when `iteration_score = 100`.

### Composite Project Score (across all stories)

```
logic_score = passing pytest tests ÷ total pytest tests × 100
ui_score    = passing Playwright tests ÷ total Playwright tests × 100
composite   = (logic_score × 0.6) + (ui_score × 0.4)
```

The 60/40 weighting reflects MVP priority on correctness over UI completeness. This weighting is subject to revision as the methodology matures.

---

## AC-to-Test Mapping Convention

Every acceptance criterion in a story must have at least one corresponding named test. The mapping is declared in the story's `## Test Coverage` section using this format:

```
- AC-03 → test_file_type_rejection
- AC-04 → test_file_size_limit
- AC-05 → test_image_preview_render
- AC-06 → test_low_res_warning_display
- AC-07 → test_continue_button_appears
```

**Rules:**
- Every AC gets at least one test. No unmapped ACs.
- Test names are specific and descriptive — no `test_1`, `test_upload`, etc.
- Qualitative ACs ("a clearly labeled button") must be made machine-verifiable before mapping (e.g. assert button exists with specific text, assert it is visible in the viewport)
- If an AC cannot be made machine-verifiable, it must be flagged `[MANUAL]` and excluded from automated scoring — but it must still be reviewed manually before the story is marked done

---

## The Session Document

At the end of each story run (pass or escalate), Code produces a session document at:

```
docs/stories/US-XXX-name-session.md
```

The session document includes:

- **Final score** and iteration count
- **Per-iteration scores** (table)
- **All assumptions made** — bolded
- **Test results** — which passed, which failed, final state
- **ACs marked [MANUAL]** and their manual verification status
- **Deviations from the story spec** — what was built differently than specified and why
- **Blocked ACs** — ACs that could not be satisfied, with explanation
- **`[META]` flags** — any methodology-level observations (missing spec, ambiguous ACs, story format gaps, model behavior surprises)

---

## Out-of-Scope Fixes During Implementation

When an implementation session surfaces a pre-existing infrastructure failure that blocks AC verification, the AI may fix it autonomously **only if all three conditions are met:**

1. The fix is unambiguously correct and low-risk (not a design decision)
2. The fix is the minimum change necessary to unblock testing
3. The fix is documented in the session document under a clearly labeled "Infrastructure Fixes" section, separate from story work

If the fix requires a design decision, or affects more than one file beyond the immediate blocker, stop and report to the developer before proceeding.

**Rationale:** The CLAUDE.md rule "modify files outside story scope — ask first" is correct in the general case. But a broken test container that prevents any AC from being verified is a special case: asking first is impractical when the infrastructure failure itself is what makes reporting difficult. This exception is narrow and must not become a license for scope creep. Every out-of-scope fix must be visible in the session document.

*Added after US-001 (Quiltix case study): CC fixed two infrastructure issues autonomously without asking first — correctly in both cases — but in doing so bent its own rules. The exception above codifies when that behavior is acceptable. See META-4 in the US-001 session document.*

---

## Methodology Findings Protocol

If a story cannot reach 100% because the spec is insufficient — missing information, ambiguous ACs, untestable criteria — that is a **methodology finding**, not just an implementation failure.

These findings are the primary research output of story-driven-ai. They must be:

1. Flagged `[META]` in the session document
2. Captured in the story-driven-ai journal in the next session
3. Used to update the story template if they reveal a structural gap

A story that escalates after 5 iterations because the spec was insufficient is more valuable to the methodology than a story that passes on the first try.

---

## What Is Not In Scope for This Protocol

- **Model selection** — which model runs the iterations is a project-level decision, not protocol
- **Branch merging** — the developer reviews and merges the PR; Code does not merge
- **Story revision** — if an iteration reveals the story needs revision, that is a design phase activity, not an implementation phase activity. Stop, revise the story, restart the iteration counter.
