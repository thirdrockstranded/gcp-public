# User Story Template — v0.1

> This is the initial template. It will be revised as iterations produce scoring data.

---

## File Naming Convention
```
US-[NNN]-[short-slug].md
```
Example: `US-003-color-quantization.md`

---

## Template

```markdown
# US-[NNN] — [Feature Name]

## Epic
[One sentence describing the overall goal this story contributes to.]

## Story
**As a** [type of user],  
**I want to** [action or capability],  
**So that** [outcome or value].

## Inputs
[List of inputs this feature receives — from the user or from upstream stories.]

## Acceptance Criteria
- [ ] [Specific, testable condition]
- [ ] [Specific, testable condition]
- [ ] [...]

## Notes
[Domain knowledge, constraints, deferred items, open questions, stakeholder guidance.]

## Test Coverage
- Unit: [what logic assertions cover this story]
- E2E (Playwright): [what UI flows cover this story]
```

---

## Principles for Writing Stories in This Framework

**Acceptance criteria must be testable.** Every criterion should map to either a unit test assertion or a Playwright step. If you can't write a test for it, rewrite the criterion until you can.

**Inputs are explicit.** Don't assume the LLM knows what data is available. List it.

**Notes carry domain knowledge.** This is where stakeholder expertise lives in the repo. Magic numbers (like 42" fabric width or 1/8 yard rounding) get explained here, not buried in code.

**Test coverage is declared, not implied.** The story says what kind of tests should exist. The test files implement them. The two stay in sync.

**One story per feature area.** Stories should be cohesive but not monolithic. If a story has more than ~8 acceptance criteria, consider splitting it.

---

## Open Questions (v0.1)
- Should stories reference each other explicitly (e.g., "from US-003") or stay decoupled?
- How granular should acceptance criteria be — implementation-level or behavior-level?
- Should edge cases live in the story or only in the test file?
- Does the story format need a "Definition of Done" section separate from acceptance criteria?
