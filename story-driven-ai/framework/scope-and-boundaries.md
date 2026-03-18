# Scope and Boundaries

## The Core Tension

story-driven-ai is a methodology for working with AI — but it is being built *using* AI, and developed initially on top of a specific AI toolchain (Claude / Claude Code). This creates contamination risks that must be actively managed:

1. **Tool bleed** — behaviors or patterns that are specific to Claude get written as if they are universal principles
2. **Implementation assumptions** — artifacts like CLAUDE.md, session management conventions, and multi-project setups are Claude Code implementation details, not methodology
3. **Confirmation bias** — an AI helping build a methodology for working with AI has a structural incentive (even if unintentional) to validate the approach rather than challenge it

This document defines where the methodology ends, where the reference implementation begins, and where the two could not be cleanly separated.

---

## What Is the Methodology (AI-Agnostic)

These concepts are intended to be tool-independent. They should apply whether you are working with Claude, GPT, Gemini, a local model, or an AI toolchain that doesn't exist yet.

- **Structured user stories as the primary driver of code generation** — the story is the specification; acceptance criteria are the verification contract
- **The Principal Layer** — the idea that a developer must maintain command and accountability over AI output, analogous to an engineering manager over a human team. The AI executes; the developer governs.
- **The three-level information hierarchy** — Story level (what this feature does), Project level (how this project operates), Session level (what the AI knows before touching a story)
- **Acceptance criteria standards** — behavioral, testable, unambiguous. The AC is a contract, not a description.
- **Definition of Done as a separate concern** — implementation quality standards that exist below the behavioral layer
- **Environment / Testing Prerequisites as a required story section** — any story referencing automated tests must state what environment those tests assume
- **Developer constitution** — project-level technical preferences (e.g. containerization, unit conventions) that cross-cut all stories and belong at the project level, not inside individual stories
- **Iteration scoring** — measuring AI output quality against stories as a feedback loop for methodology improvement
- **The separation of sycophancy from validation** — methodology documents and AI outputs must be challenged, not just confirmed. Seek disconfirmation actively.

---

## What Is the Reference Implementation (Claude-Specific)

These are implementation artifacts for the Claude / Claude Code toolchain. They are *examples* of how the methodology can be realized, not the methodology itself.

- **CLAUDE.md** — Claude Code's mechanism for persistent project context. The *concept* (give the AI a briefing document it reads every session) is methodology. The specific file name, format, and Claude Code behavior are implementation.
- **The two-Claude-Project setup** — using separate Claude.ai projects for PM work and implementation work to manage context contamination. This pattern may not translate to other tools.
- **`/clear` and session management conventions** — Claude Code-specific
- **Story files as the context payload** — feeding story markdown directly to Claude Code is a Claude-specific workflow. Other tools may require different context injection mechanisms.
- **MCP server integration** — Claude-specific protocol

When documenting methodology, avoid using Claude-specific terminology as if it were generic. For example: "give the AI a project briefing document" is methodology. "Create a CLAUDE.md" is implementation.

---

## Where They Could Not Be Separated

This section is an honest log of places where the implementation bled into the methodology, and why.

| Area | Contamination | Reason |
|------|--------------|--------|
| Story format | Markdown files with specific section headers were designed with Claude's context window behavior in mind | Claude's tendency to anchor on structured headers influenced what "a good story" looks like |
| Iteration scoring | The scoring approach assumes test output Claude Code can read and reason about | Designed around Claude Code's ability to run and interpret test results |
| Journal / [META] tagging | The tagging convention emerged from working in Claude.ai chat and wanting to flag methodology-level observations | May not translate meaningfully outside a chat-based workflow |

*This table should be updated as new contamination is identified. Identifying contamination is a feature, not a failure.*

---

## Guiding Principle for All Contributors (Including AI)

> When adding to this methodology, ask: "Is this true because it's a good idea, or is it true because Claude works this way?"

If the answer is the latter, it belongs in the reference implementation section, not the methodology. If you cannot tell, document the uncertainty explicitly rather than papering over it.

This applies to human contributors and to AI assistants helping develop this repository. AI-generated contributions to this methodology should be treated with the same skepticism as any other source — the AI has no special authority here, and its tendency toward agreement is a known liability.