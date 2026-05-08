---
name: survey
description: Use when surveying a codebase and existing documentation to produce a Diataxis-classified gap analysis and documentation plan
---

# Diataxis: Survey

Explore the project, catalogue every existing document, classify each using the Diataxis framework, identify every gap, and produce a structured documentation plan. Return the plan to the caller — do not present it to the user and do not wait for approval.

## Checklist

Create a todo for each item and complete them in order:

1. **Explore the codebase** — README, docs/, any .md files, code entry points, tech stack, intended audience, and documentation toolchain (see Toolchain Detection below)
2. **Write a one-paragraph project summary** — what the project does, who it is for, what the main concepts are
3. **Catalogue every doc found** — classify each with the Diataxis framework; flag every misclassification
4. **Run the gap analysis** — check all four types; note what is missing or inadequate in each
5. **Draft the documentation plan** — specific title and one-line purpose for every gap

## The Four Types

Every piece of documentation belongs to exactly one of the four types below. Classify by asking two questions: Is this about _doing_ or _understanding_? Is the reader _learning_ or _working_? These two questions resolve every ambiguous case.

|                   | Learning    | Working      |
| ----------------- | ----------- | ------------ |
| **Doing**         | Tutorial    | How-to guide |
| **Understanding** | Explanation | Reference    |

### Tutorials

A tutorial is a lesson. The reader is a beginner who cannot yet judge whether their own work is correct. That is your responsibility as the writer. You guide; they follow. Something real and visible happens at every step.

**Identify a tutorial by these characteristics:**

- It walks the reader through completing something specific from scratch
- Every step produces a visible, verifiable result — the reader can confirm they are on track
- Nothing is assumed; nothing is skipped
- The reader learns by doing, not by reading about doing

**Common misclassifications:**

- A "Getting Started" page that explains concepts instead of guiding action is not a tutorial — it is explanation dressed up as a tutorial
- A feature walkthrough that demonstrates capability instead of teaching the reader how to accomplish something is not a tutorial — it is a product demo
- A tutorial that offers three ways to do the same thing is not a tutorial — it is an indecisive how-to guide

### How-to Guides

A how-to guide serves a competent user who has a specific goal and needs to achieve it. The reader already knows what they want and why. Your job is to get them there.

**Identify a how-to guide by these characteristics:**

- The title names a goal: "How to deploy to production", "How to add a custom provider"
- It assumes the reader is competent and purposeful — no background, no motivation, no preamble
- It contains steps, commands, and conditionals only
- It may fork: real tasks have decision points and the guide captures them

**Common misclassifications:**

- A "Configuration" page that explains every option in narrative form is not a how-to guide — it is reference with instructions mixed in
- An "Advanced Usage" page that teaches concepts rather than directing action is not a how-to guide — it is explanation
- A tutorial that says "if you're an advanced user, skip to step 4" is not a how-to guide — it is a tutorial that does not trust its audience

### Reference

Reference is a map of the machinery. The reader is working and needs a fact. Give it to them — then stop.

**Identify reference by these characteristics:**

- It describes what exists: every API endpoint, every configuration key, every CLI flag, every method signature and return type
- Its structure mirrors the structure of the product itself — same order, same names, same groupings
- It contains facts, not instructions or explanations
- It is complete — incompleteness defeats the purpose of reference entirely

**Common misclassifications:**

- A "README" that mixes a configuration table with usage examples and a philosophy section is not reference — it is three things failing to be any of them
- An "API reference" that says "to call this method, first do X" is giving instructions — reference says what the method accepts and returns, nothing more
- A "Concepts" page that lists terms and their definitions but then explains why those concepts exist is mixing reference with explanation

### Explanation

Explanation is for readers who want to understand, not act. They are not in the middle of a task. They want to know why the system works the way it does.

**Identify explanation by these characteristics:**

- It covers design decisions, trade-offs, history, and context
- The reader can benefit from it without having the product open in front of them
- It expresses opinions and recommends approaches — this is the only type where that is appropriate
- It makes connections to related concepts, even outside the immediate system

**Common misclassifications:**

- Architecture comments scattered across inline code are not explanation — they are explanation without a home, which is the same as no explanation at all
- A "Philosophy" section buried inside a README is explanation that has been misplaced — extract it
- A document titled "How it works" that contains both conceptual background and step-by-step instructions is not explanation — the instructions need to move to a how-to guide

## Toolchain Detection

Identify the documentation toolchain before doing anything else. It determines file format, directory structure, inline comment conventions, and cross-reference syntax. The toolchain you detect becomes a field in your output — the orchestrator will confirm it with the user before writing begins.

**To detect the toolchain, look for:**

- Documentation build configuration files anywhere in the project (root, `docs/`, or config directories)
- Build scripts in package manager files (`package.json`, `Makefile`, `pyproject.toml`, `tox.ini`) that reference documentation generation
- CI pipeline steps that build or deploy documentation
- The file format of existing documentation files (`.rst`, `.md`, `.adoc`, etc.)
- Patterns in existing doc files that suggest auto-generation from source comments

**If a toolchain is detected:** note it and include it in the output. Do not recommend switching to a different tool.

**If no toolchain is detected:** record "None detected" in the output. The orchestrator will ask the user to choose one before writing begins.

**Also detect the inline comment style** used in the source code, if any. Scan a sample of source files and note the convention (e.g. docstring format for Python, JSDoc-style comments for JavaScript, XML doc comments for C#). Include this in the toolchain output — it determines how API reference content is written.

## Cataloguing Existing Docs

For every documentation file found, record all three of these:

```
File: README.md
Content: Installation steps + configuration table + design rationale
Classification: Mixed (tutorial + reference + explanation) — needs splitting
```

Flag every misclassification. Do not mark a mixed document as acceptable. A document that serves two purposes serves neither well.

If no documentation files are found at all, write "No documentation found" under Existing Documentation in the output and proceed directly to the gap analysis. Treat every checklist item as unmet.

## Gap Analysis

Work through each type systematically. For each type, record what exists, what is missing, and what is misclassified:

**Tutorials**

- [ ] Is there at least one end-to-end getting-started tutorial?
- [ ] Does it guide the learner to a meaningful first success without requiring they understand everything first?
- [ ] Does every step produce a visible, verifiable result?
- [ ] Is it free of explanation (beyond a single clarifying sentence per step)?
- [ ] Does it make every decision for the reader — no options, no alternatives?
      For every unchecked item, add a corresponding `[ ]` entry to the Documentation Plan with a specific title and a one-line purpose statement.

**How-to guides**

- [ ] Are the most common user tasks covered as focused, goal-titled guides?
- [ ] Are they written from the user's goal — not from the tool's perspective?
- [ ] Do they assume a competent user who knows what they want?
- [ ] Are they free of teaching, background, and motivation?
      For every unchecked item, add a corresponding `[ ]` entry to the Documentation Plan with a specific title and a one-line purpose statement.

**Reference**

- [ ] Is the API / CLI / configuration fully described in a neutral, factual way?
- [ ] Does the structure of the reference mirror the structure of the product itself?
- [ ] Is it complete — every option, flag, field?
- [ ] Is it free of instruction and explanation?
      For every unchecked item, add a corresponding `[ ]` entry to the Documentation Plan with a specific title and a one-line purpose statement.

**Explanation**

- [ ] Are there documents explaining _why_ the system works the way it does?
- [ ] Are design decisions, architecture choices, and trade-offs documented?
- [ ] Is there context for non-obvious concepts that users need to understand the domain?
      For every unchecked item, add a corresponding `[ ]` entry to the Documentation Plan with a specific title and a one-line purpose statement.

## Output Format

Return your findings in the following format. Do not present this to the user — return it to the orchestrator (`diataxis:document`), which will present it and handle user interaction.

Use exactly these markers throughout the plan: `[x]` = exists and is well-formed, `[~]` = exists but needs improvement, `[ ]` = missing entirely. No other values are permitted.

```markdown
## Project Summary

[One paragraph: what the project does, who it is for, what the main concepts are, what the tech stack is.]

## Documentation Toolchain

Detected: [tool name, or "None detected"]
Config: [path to build config file, or "none found"]
Inline comment style: [e.g. "Google-style docstrings" / "JSDoc comments" / "none detected"]
Recommendation: [if already in use: "Continue with [tool]." / if not detected: "None detected — the orchestrator will ask the user to choose before writing begins."]

## Existing Documentation

- `README.md` — Mixed (tutorial + reference): installation guide + API table. Needs splitting.
- `docs/api.md` — Reference (good shape)
- `docs/CONTRIBUTING.md` — How-to guide (good shape)

## Misclassifications

- `README.md`: Mixes tutorial content (installation steps) with reference (API table) and explanation (design rationale). Split into three separate documents.

## Documentation Plan

### Tutorials (1 existing → 2 proposed)

- [~] "Getting started" _(exists in README — needs extracting and expanding into a proper lesson)_
- [ ] "Build your first X in 10 minutes" — A hands-on lesson walking a new user through a minimal working example from scratch.

### How-to guides (1 existing → 3 proposed)

- [x] "How to contribute" _(exists, good shape)_
- [ ] "How to deploy to production" — Steps covering env vars, healthchecks, and rollback.
- [ ] "How to run the test suite locally" — Steps to get tests running in a local dev environment, including prerequisites.

### Reference (1 existing — needs improvement)

- [~] "API reference" _(exists in README — needs extracting into its own file and completing)_
- [ ] "Configuration reference" — Complete description of every configuration key, type, default, and effect.

### Explanation (0 existing → 2 proposed)

- [ ] "Why we built it this way" — Architecture decisions and the trade-offs behind them.
- [ ] "Understanding the data model" — Conceptual overview of the core entities and how they relate.
```

## What Not to Do

- Do not present results to the user. Do not ask the user for approval. The orchestrator does that.
- Do not create empty folder structures. The plan lists documents to write; do not create `docs/tutorials/` with nothing in it.
- Do not skip the gap analysis because the gaps seem obvious. Run it explicitly and record the results.
- Do not classify a mixed document as one type because it is "mostly" that type. Flag the misclassification and propose splitting.
