# Case Study 1 — Quiltix

## What Is Quiltix?

Quiltix is a web-based tool that converts any photograph into a pixel-style quilt pattern, outputting a visual grid preview and fabric yardage calculations.

Full project: [github.com/thirdrockstranded/quiltix](https://github.com/thirdrockstranded/quiltix)

---

## Why Quiltix As Case Study 1?

- **Bounded scope.** The MVP is well-defined with a small number of discrete features.
- **Measurable correctness.** Yardage calculations are deterministic — there is a right answer. This makes the logic test harness straightforward and unambiguous.
- **Real stakeholder.** A domain expert (experienced quilter) is available to validate output quality and pattern usability. This grounds the experiment in real-world requirements rather than synthetic ones.
- **Meaningful complexity.** The project involves image processing, math, UI, and PDF export — enough surface area to stress-test the story format across different kinds of features.

---

## Project Snapshot

| Attribute | Value |
|---|---|
| Platform | Web (React + FastAPI) |
| MVP features | 6 user stories |
| Primary domain risk | Color quantization quality |
| Primary output risk | PDF pattern usability (validated by stakeholder) |
| Deferred | Half-square triangles, metric units, palette editing |

---

## Iterations

| # | Composite Score | Notes |
|---|---|---|
| [01](./iterations/iteration-01/) | TBD | Initial story format, first generation |

---

## Key Domain Constraints (carried from Quiltix VISION.md)

- Seam allowance defaults to **1/4"**; cut size = finished size + 1/2"
- Standard fabric width: **42" usable** (quilting cotton convention)
- Yardage always rounds **up** to nearest 1/8 yard — never down
- Units: **imperial at launch**; data model is unit-aware for future metric toggle
- Block shapes: **squares only** at MVP
