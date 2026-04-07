# User Story Template — v0.3

> Changes from v0.2: Added `## Environment / Testing Prerequisites` guidance on exact version pinning for browser automation dependencies and Vite `allowedHosts` behavior in Docker networks. These were identified as load-bearing infrastructure concerns during US-001 (Quiltix case study). See META-2, META-3 in the US-001 session document.
>
> Changes from v0.1: Added `## Definition of Done`, `## Environment / Testing Prerequisites`, and AC-to-test mapping convention in `## Test Coverage`. These sections were identified as necessary during the Quiltix design phase (see journal 2026-03-17, 2026-03-19).

---

## Template

Copy everything below the horizontal rule into a new story file.

---

# US-XXX — [Short Title]

## Epic
[One sentence describing the larger feature area this story belongs to.]

## Story
**As a** [user type],  
**I want to** [action],  
**So that** [outcome/value].

## Inputs
- [List the inputs this story operates on — data, files, user-provided values]

## Acceptance Criteria
- [ ] AC-01: [Behavioral, testable, unambiguous. Written from the user's perspective.]
- [ ] AC-02: [Each criterion must be machine-verifiable or explicitly marked [MANUAL].]
- [ ] AC-03: [Qualitative criteria ("a clear error message") must be made specific ("error message containing the text 'Accepted formats: JPEG, PNG, WEBP'").]

> **AC authoring rules:**
> - Every AC must have a corresponding named test in the Test Coverage section
> - If an AC cannot be automated, mark it `[MANUAL]` — it will be reviewed manually and excluded from automated scoring
> - Avoid "TBD" — an unresolved AC is a blocker that must be resolved before implementation begins
> - Prefer concrete thresholds over qualitative descriptors ("files over 10MB" not "large files")

## Definition of Done
- [Where is validation enforced? Client-side, server-side, or both?]
- [Error message quality standard — no raw exception text, specific user-friendly copy]
- [Rendering/layout expectations if UI is involved]
- [Any non-functional requirements — performance, accessibility, browser support]

## Environment / Testing Prerequisites
> Required for any story with E2E or integration tests. Omit only for pure unit test stories.

- [What must be running for tests to execute? e.g. "Full stack via `docker compose up`"]
- [Which containers are involved?]
- [Any seed data, fixtures, or preconditions required?]
- [Single command to bring up the test environment]

> **Bootstrap and dependency pinning notes (apply to all projects using Playwright in Docker):**
>
> - Browser automation dependencies (`@playwright/test`, `playwright`) must be pinned to **exact versions** (e.g. `1.46.0`), not semver ranges (e.g. `^1.46.0`). A range resolves to the latest at install time, which will mismatch the browser binaries in a versioned base image and cause crashes or SIGSEGVs.
> - Vite 5.4+ enforces `allowedHosts` by default. Any Playwright container connecting to a Vite dev server over a Docker network (e.g. `http://frontend:5173`) will be rejected with a host header error unless `server.allowedHosts: true` is set in `vite.config.ts`. This is not a story-level concern — it belongs in the bootstrap story's acceptance criteria or in `CLAUDE.md`.
>
> *Source: US-001 session document, Quiltix case study (META-2, META-3).*

## Test Coverage

Map every AC to at least one named test. No unmapped ACs.

| AC | Test Name | Type |
|----|-----------|------|
| AC-01 | test_[descriptive_name] | unit / e2e |
| AC-02 | test_[descriptive_name] | unit / e2e |
| AC-03 | [MANUAL] | manual |

**Test types:**
- `unit` — pytest, no running services required
- `e2e` — Playwright, full stack required
- `integration` — pytest with running services
- `manual` — cannot be automated; requires human review before story is marked done

## Notes
- [Domain context, stakeholder input, rationale for specific decisions]
- [Known limitations or accepted tradeoffs]
- [Tunable constants or thresholds — name them, don't hard-code them]
- [Dependencies on other stories]

---

## Authoring Checklist

Before handing a story to implementation, verify:

- [ ] Every AC is specific and unambiguous
- [ ] No AC contains "TBD"
- [ ] Every AC has a named test in the Test Coverage table
- [ ] Any qualitative AC is either made specific or marked `[MANUAL]`
- [ ] Definition of Done is filled in
- [ ] Environment / Testing Prerequisites is filled in (if E2E or integration tests present)
- [ ] If E2E tests use Playwright in Docker: browser automation deps are pinned to exact versions
- [ ] If E2E tests run against a Vite dev server in Docker: `server.allowedHosts: true` is confirmed in `vite.config.ts`
- [ ] Story can be implemented without requiring changes to VISION.md or other stories

If any item is unchecked, the story is not ready for implementation.
