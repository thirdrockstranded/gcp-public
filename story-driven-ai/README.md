# story-driven-ai

> Building the missing management layer for professional AI-assisted development — one piece at a time.

---

## Status

🧪 **Active experiment.** This is not a finished methodology. It is being developed and validated in public. Everything here is subject to revision — including the premise.

🤖 **AI-assisted repo.** This repository — including its documentation, journal entries, and framework documents — has been developed collaboratively with AI assistance. That is intentional and consistent with the project's purpose. It also means readers should apply their own judgment: AI can introduce subtle errors, overconfident framing, or gaps that a human author might catch. If you spot something that doesn't look right, that's a feature of the experiment, not a bug in the repo. Issues and discussion welcome.

---

## The Real Target

There is a moment every professional developer hits when working with AI that feels something like this:

*I'm done having fun with this. I need to put it to work. I need to assign it something, get a result I can stand behind, explain what was built and why, and answer for it if something goes wrong. I need to run this like a professional operation — not keep everything in my head and hope the next prompt gets me closer.*

What that moment reveals is a missing layer. Not missing capability — the models are capable enough. Not missing access — the tooling is everywhere. What's missing is **the Principal Layer** — the structured infrastructure that puts a professional developer in the role of *principal*: the party who sets direction, owns outcomes, and holds the process accountable. The AI is the agent. The layer is what makes that relationship professionally functional.

The same command, visibility, and accountability that a competent engineering manager has over a human development team. Assign work. Get structured output. Measure progress. Explain results. Catch problems early. Know what is done, what isn't, and why. Hold the process accountable to something other than vibes.

But before any of that is possible, someone has to produce the architectural picture that direction depends on. That is the other half of the Principal Layer — and the half that is most often left entirely to informal, unsupported process.

The Principal Layer has two modes:

**Design Mode** — working *with* AI to move from idea or intent to a coherent structure. A client problem, a product concept, a new feature in an established codebase, a greenfield vertical stack — anything from fuzzy to defined. The principal's architectural judgment is most active here. AI is a thinking partner and stress-tester, not an implementer. The output is something concrete enough that Direction Mode can use it as an input.

**Direction Mode** — working *through* AI to move from defined structure to implemented, verified output. Assign work. Measure results. Hold the process accountable.

The transition between them — the moment where "we're still figuring out what this is" becomes "we know what this is and now we're building it" — is one of the most important and least-discussed boundaries in professional software development. The Principal Layer is designed to support both sides of it.

The bridge between them is the **Handoff Contract** — a lightweight definition of what Design Mode must produce before Direction Mode can begin. See `framework/handoff-contract.md`.

That layer does not exist today in any coherent, portable, professional form. This project is an attempt to build it — starting with the most foundational piece.

---

## A Foundational Observation

The software engineering industry has spent decades iterating and refining how humans break down, specify, and communicate software problems — through structured methodologies, design principles, and project management frameworks. Agile, SOLID, domain-driven design, user stories, acceptance criteria — all of these are, in effect, a discipline for decomposing complexity into units that are well-defined, independently addressable, and verifiable.

The observation at the heart of this project: **we have been training AI to program all along.** Every well-formed user story, every clearly scoped ticket, every acceptance criterion written by a developer over the last three decades has contributed to the corpus that LLMs learned from. The better the human specification practices that fed that training, the better the model's ability to generate correct, coherent code from structured input.

This is not a coincidence — it is a feedback loop. Good software engineering practice produces good specifications. Good specifications produce good training data. Good training data produces models that respond well to good specifications.

The implication: the language of professional software engineering — stories, acceptance criteria, done-ness, accountability — is not just familiar to these systems. It is the language they were trained on. We do not need to invent a new way to speak to AI. We need to use the language we already have, deliberately and precisely, with the expectation of measurable results.

---

## The Architectural Position

To be direct: this project does not assume that existing software engineering or project management frameworks are the right answer and simply need tuning. The working assumption is that they are probably not — at least not in their current forms — because they were designed to coordinate humans, not direct machines.

That is not a criticism of those frameworks. It is an acknowledgment that the context has changed enough that the honest starting point is a design question, not an adaptation question.

**What should the system actually be?**

Not "how do we adapt Scrum" or "how do we bolt user stories onto a prompt workflow." The architectural instinct here is a clean sheet: given that your implementer is an AI, given what AI is good at and bad at, given what professional developers and teams actually need — design the process from those requirements up.

The requirements of that system:
- A clear, repeatable way to direct AI toward specific, agreed-upon outcomes
- Structured, verifiable output — not plausible-looking approximations
- Metrics and evidence of progress at a granular level
- Transferability to other developers and team members without requiring them to reinvent it
- Professional accountability — to clients, employers, and the craft itself
- Honest about what it doesn't know yet, and open to the answer being surprising

---

## The Open Questions This Project Is Trying To Answer

This is as much an inquiry as a methodology. The questions below are the actual targets. Case studies generate evidence. Evidence sharpens or refutes the answers.

**1. What is the right unit of work for AI-assisted development?**
A human developer can ask clarifying questions, hold context across weeks, recover from ambiguity. An LLM gets one shot per context window. That changes what "well-specified" means — but how, exactly? Is the user story the right unit? Too big? Too small? This project intends to find out empirically.

**2. What parts of existing frameworks are actually useful, and what is baggage?**
Some ceremony in Agile exists to solve problems that simply do not exist when the implementer is an AI. Starting from first principles: what does a specification process actually need? What can be discarded? What needs to be invented?

**3. Is "break it into digestible, testable pieces and iterate" even the right model?**
This project begins with that assumption and holds it loosely. A negative result — the decomposition model is wrong, or only partially right — would be as valuable as a positive one.

**4. Should we dispense with inherited frameworks entirely?**
There is a reasonable argument that carrying forward the vocabulary of frameworks designed for human teams introduces friction that a clean-sheet approach would avoid. This project doesn't start there, but takes the question seriously and will revisit it as evidence accumulates.

---

## This Project In Context — A Series

`story-driven-ai` is Project 1 in what is really a larger series of work, each piece addressing a different slice of the missing Principal Layer:

| Project | Slice | Question |
|---|---|---|
| **1. story-driven-ai** (this repo) | Specification & verification | Can you direct AI precisely enough to get structured, measurable results? |
| 2. *(future)* | Visibility & progress | How do you know where things stand across a real engagement, in a form you can show someone? |
| 3. *(future)* | Accountability & handoff | How does this transfer to a team, survive a client conversation, hold up under professional scrutiny? |

Everything else that belongs in the management layer depends on the answer to Project 1's question. You cannot manage output you cannot specify or verify. So this is the right place to start.

---

## The Hypothesis (Current)

Structured, well-formed user stories — stored alongside the code they describe — can serve as a reliable, repeatable specification layer for AI code generation. The quality of the generated code is directly measurable against those stories through automated testing. Iterating the story format improves the score.

"Structured and well-formed" is doing significant work in that sentence. An open and important qualifier: *structured and well-formed relative to what context?* A story that is perfectly self-contained in isolation may be insufficient if the AI has no way to understand where it sits in the larger architectural picture. The degree to which a story needs to carry its own context — versus relying on ambient project knowledge — is itself one of the things this experiment is designed to reveal.

A working hypothesis within the hypothesis: stories may exist on a **context sufficiency gradient**. At one end, a story paired with a good VISION.md may be enough. At the other, there may be cases where a middle layer is needed — something between the whole-project vision and the individual story, covering a cluster of related features and the shared domain knowledge they depend on. Whether that layer needs to be a defined artifact, and what form it should take, is an open question this project intends to answer empirically.

If proven, this becomes a developer-native methodology for AI-augmented development that is:
- **Self-documenting** — the repo is the spec
- **Measurable** — test scores quantify how well output matched intent
- **Repeatable** — the story format is a portable template, not project-specific
- **Iterable** — the framework improves with each case study

The hypothesis is stated with confidence but held loosely. The experiment may refute it. That outcome is documented here too.

---

## The Approach

1. **Write user stories** in a structured format before any code is written
2. **Generate code** using an LLM, providing the stories as the specification
3. **Run automated tests** against the generated code — two layers:
   - Logic/math test harness (deterministic assertions)
   - UI/functional tests (Playwright)
4. **Score the output** — % of tests passing across both layers
5. **Iterate the story format** — did changing the structure improve the score?
6. **Repeat**

The story format is the variable. The test score is the signal.

---

## Repo Structure

```
story-driven-ai/
├── README.md                       # This file — start here
├── framework/                      # The methodology itself (evolves over time)
│   ├── story-template.md           # The current user story template (Direction Mode)
│   ├── scoring.md                  # How to measure and score generated output (Direction Mode)
│   ├── handoff-contract.md         # The boundary between Design and Direction Mode
│   ├── context-management.md       # Open problem — session memory and context continuity
│   └── observations.md             # Distilled findings — graduates from journal
├── case-studies/
│   └── quiltix/                    # Case Study 1
│       ├── overview.md             # Project context and links
│       └── iterations/             # Scored iterations of the story format
│           └── iteration-01/
│               ├── score.md        # Test results and scoring
│               └── notes.md        # What changed and why
└── journal/                        # Raw dev log — dated markdown entries
    └── YYYY-MM-DD.md               # [META] tag for publication-relevant thinking
```

---

## Case Studies

| # | Project | Description | Status |
|---|---|---|---|
| 1 | [Quiltix](./case-studies/quiltix/overview.md) | Photo-to-quilt-pattern web app | 🔄 In progress |

---

## Following Along

Journal entries in `/journal` are raw and honest — work in progress, dead ends included. Entries tagged `[META]` contain observations that transcend the immediate methodology and may inform eventual publication. `framework/observations.md` is the editorial distillation of those entries as patterns emerge.

If you find this useful, fork it, apply it to your own project, and share what you find. Attribution appreciated — git history is permanent.

---

## A Note On Writing Journal Entries

Journal entries serve two purposes simultaneously, and it's worth being conscious of both when writing them.

**Purpose 1: Raw capture.** Get the thought down while it's alive. Don't polish, don't self-edit, don't wait until the idea is fully formed. The journal is the place where half-formed observations, dead ends, revised positions, and "I wonder if..." thinking belongs. Completeness matters more than elegance here.

**Purpose 2: Source material.** The journal is the first draft of whatever this project eventually produces — a guide, a talk, a series of posts, a short book. Entries tagged `[META]` in particular are raw manuscript. Writing with that in mind doesn't mean over-formalizing — it means including enough context that the thought is recoverable later by someone (including future you) who wasn't in the room when it occurred.

A useful heuristic: **write as if you're leaving a voice memo for a smart colleague who missed the conversation.** Enough context to reconstruct the thinking. Honest about uncertainty. Specific about what prompted the observation. That's both good capture and good source material at the same time.

---

## Background

This work began as a search for a developer-native way to work with AI that felt rigorous rather than ad hoc — and grew into a recognition that the missing piece is not a better prompt, but a better process. One designed for the actual problem rather than inherited from a different era.

Developed together by the founders of Green Checkered Pants, a company currently in formation, bringing 30 years of software engineering and architecture experience to the problem of professional AI-assisted development.

---

## Meta-Analysis & Publication Notes

As this experiment progresses, observations that transcend the immediate methodology — insights about the industry, the nature of AI-assisted development, parallels to prior art, potential conclusions — are captured in the journal with a `[META]` tag in the entry title. These are the raw materials for any eventual write-up, talk, or guide that comes out of this work.

The journal is intentionally unsanitized. Capturing the thinking as it happens, including dead ends and revised positions, is part of the record. A polished summary of meta-analytical findings will eventually live in `framework/observations.md` as patterns emerge.

Emerging themes for eventual publication:
- The accidental training ground — software engineering as inadvertent AI curriculum
- The methodology gap — why AI coding capability has outpaced AI development process
- The shoehorn problem — why experienced developers struggle most with AI-assisted development
- The team scaling problem — why undocumented AI workflows don't survive the first hire
- The professionalism & accountability argument — the business case for structured process
- The unit of work problem — what changes when the implementer never asks a question
- The design-direction boundary — the most important transition nobody talks about
- The handoff contract — the lightweight artifact that bridges design and direction
- The context problem — whether the Principal Layer's documentation discipline is accidentally the solution
- The clean sheet question — what would this look like designed for the actual problem
