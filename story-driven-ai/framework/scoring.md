# Scoring Generated Output — v0.1

> How to measure whether the AI-generated code matched the intent of the user stories.

---

## The Two Test Layers

### Layer 1: Logic Test Harness (pytest)
Deterministic assertions against the core business logic. These tests have known inputs and known expected outputs. Pass/fail is unambiguous.

Examples for Quiltix:
- Given a 60"×80" quilt with 2" blocks → assert grid is 30×40
- Given a 2" finished block with 1/4" seam allowance → assert cut size is 2.5"
- Given 450 squares of Fabric 1 at 2.5" cut size → assert yardage rounds up to correct value
- Given a known image resized to 10×10 with N=3 colors → assert output contains exactly 3 colors

### Layer 2: UI / Functional Tests (Playwright)
End-to-end tests that verify a user can complete the workflow. Pass/fail per step.

Examples for Quiltix:
- User can upload a photo and see a preview
- User can complete all input fields and proceed
- Grid preview renders with correct number of cells
- Fabric requirements list shows correct number of entries
- Export button triggers a PDF download

---

## Scoring Formula

### Per-Layer Score
```
layer_score = passing_tests ÷ total_tests × 100
```

### Composite Score
```
composite_score = (logic_score × 0.6) + (ui_score × 0.4)
```

The 60/40 weighting reflects MVP priority on correctness over UI completeness. This weighting is itself subject to revision.

---

## Iteration Record Format

Each iteration in a case study captures:

| Field | Description |
|---|---|
| Iteration | Number (01, 02, ...) |
| Story format version | Which template version was used |
| Changes from previous | What was different about the stories this iteration |
| Logic score | % of unit tests passing |
| UI score | % of Playwright tests passing |
| Composite score | Weighted total |
| Notes | What the score revealed; what to try next |

---

## What We're Looking For

A story format iteration is considered an improvement if:
- Composite score increases, OR
- A previously failing test category starts passing, OR
- The generated code requires significantly less manual correction

A story format iteration is considered neutral or worse if:
- Score stays flat despite changes, OR
- Score improves in one layer but regresses in another without a clear reason

---

## Open Questions (v0.1)
- Should LLM-as-judge scoring be added as a third layer? (Does the generated code *feel* like it matched intent, beyond binary pass/fail?)
- How do we account for tests that were never generated (missing coverage vs. failing coverage)?
- Should manual correction effort be tracked as a separate metric?
