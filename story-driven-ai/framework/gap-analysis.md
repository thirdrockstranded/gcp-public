# [META] Gap Analysis — story-driven-ai Framework

*Generated: 2026-03-19*  
*Source: Critical review session, pre-first-implementation*  
*Purpose: Active disconfirmation. These are the hardest pushbacks on the current approach. They are not blockers — they are the work.*

---

## Gap 1: The Scoring Mechanism Doesn't Exist

**The claim:** The methodology produces measurable outcomes. Iteration scoring is named as a core concept.

**The reality:** There is no validated scoring rubric. No baseline has been established. There is currently no way to determine whether iteration 2 is objectively better than iteration 1. What exists is a well-organized way to write stories and observe what happens. That is valuable — but it is a *practice with documented observations*, not a *methodology with measurable outcomes*. The gap between those two things matters enormously if the goal is to generalize or publish.

**What needs to exist:** A concrete scoring rubric that can be applied consistently across iterations and — critically — across different projects, developers, and AI tools. The rubric must be defined before the first scored iteration, not derived from it.

**Risk if unresolved:** Every "this worked" claim is unfalsifiable. The methodology becomes a collection of anecdotes organized in markdown.

---

## Gap 2: One Case Study Proves Nothing, and It Isn't Independent

**The claim:** Quiltix is Case Study 1 and will validate the methodology.

**The reality:** Quiltix is being built by the person developing the methodology, using the tool the methodology is designed around. There is no separation between researcher and subject. Every observation is made by someone who wants the methodology to work, using a tool that has a structural interest in the methodology working. Confirmation bias is not just a risk here — it is the default state.

**What needs to exist:** A second case study, run by a different developer, on a different project, preferably with a different AI tool. Until then, every conclusion drawn from Quiltix is provisional and should be labeled as such.

**Risk if unresolved:** The methodology looks validated when it is only self-confirmed. External credibility requires external replication.

---

## Gap 3: The Principal Layer Is a Metaphor, Not a System

**The claim:** The Principal Layer gives developers command and accountability over AI, analogous to an engineering manager over a human team.

**The reality:** This is a compelling framing, but it is a framing — not an operationalized framework. Key questions that remain unanswered:
- What does the Principal Layer *do* concretely beyond writing good stories and reviewing output?
- How does it handle disagreement between developer intent and AI output?
- What are the failure modes of the Principal Layer itself? (Developer abdicates, over-specifies, or cannot evaluate AI choices in an unfamiliar domain — all of which occurred in the current session.)
- How does the Principal Layer scale when multiple AI agents are operating simultaneously?

**What needs to exist:** A concrete description of Principal Layer *behaviors*, not just the concept. What does a developer in the Principal Layer role actually do at each phase of the workflow? What decisions belong to them that cannot be delegated?

**Risk if unresolved:** The Principal Layer becomes a metaphor that makes the methodology sound more complete than it is. Metaphors are not systems.

---

## Gap 4: The Methodology May Be Solving the Wrong Problem

**The claim:** Better-structured stories produce better AI output.

**The reality:** This may be true, but the more significant variable may simply be *model quality*. A better model produces better output regardless of story structure. A weaker model fails regardless of how good the story is. If that is true, the methodology is valuable but secondary — and its apparent effectiveness will fluctuate with model releases in ways that have nothing to do with the methodology itself.

**The deeper problem:** There is currently no mechanism for separating "the stories helped" from "the model improved" in iteration scoring. Without that separation, the methodology cannot make causal claims about its own effectiveness.

**What needs to exist:** A controlled comparison — same stories, different models — or at minimum an explicit acknowledgment in the methodology that model quality is a confounding variable that cannot currently be isolated.

**Risk if unresolved:** The methodology takes credit (or blame) for outcomes that are actually model-dependent. Conclusions drawn today may not hold as models improve, degrade, or change behavior.

---

## Gap 5: Naming the Contamination Problem Doesn't Resolve It

**The claim:** `scope-and-boundaries.md` addresses the risk of Claude-specific implementation bleeding into AI-agnostic methodology.

**The reality:** Naming a risk is not the same as managing it. The contamination table in `scope-and-boundaries.md` has three entries and an instruction to update it — but no mechanism for *catching* contamination as it occurs. The current process for identifying contamination is: the same person, using the same tool, noticing when they've let implementation details slip into methodology claims. That is not a robust process.

**What needs to exist:** An active disconfirmation practice built into the methodology's cadence. Concretely: a recurring "red team" step where the methodology is explicitly challenged rather than confirmed. This could be a scheduled session, a checklist applied to each journal entry, or a review by someone outside the project. A document that acknowledges the risk without providing a mechanism to catch it is a liability that looks like an asset.

**Risk if unresolved:** `scope-and-boundaries.md` provides the appearance of rigor without the substance of it. The methodology looks self-aware while remaining self-confirming.

---

## Summary Table

| Gap | Core Risk | Status |
|-----|-----------|--------|
| Scoring mechanism absent | Claims are unfalsifiable | Open |
| Single non-independent case study | Self-confirmation, no external validity | Open — requires second case study |
| Principal Layer underspecified | Metaphor without operational definition | Open |
| Model quality as confound | Cannot isolate methodology effectiveness | Open — requires controlled comparison |
| Contamination detection has no mechanism | Scope boundaries named but not enforced | Open — requires recurring practice |

---

## A Note on This Document

This gap analysis was produced by the same AI (Claude) being used to build the methodology it is critiquing. That is itself an instance of Gap 5. Treat this document as a starting point for critical review, not a conclusion. The value of this document is proportional to how seriously these gaps are pursued — not how thoroughly they are acknowledged.
