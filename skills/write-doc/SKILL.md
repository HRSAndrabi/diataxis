---
name: write-doc
description: Use when writing a single documentation document of a known Diataxis type — tutorial, how-to guide, reference, or explanation
---

# Diataxis: Write Doc

Write one document. Apply the rules for its type without deviation. Place it correctly. Commit it.

## Checklist

Create a todo for each item and complete them in order:

1. **Confirm inputs** — document type, title, one-line purpose, project context, target path. For how-to guides, confirm the title begins with "How to". If it does not, propose a corrected title and ask the user to confirm before proceeding.
2. **Confirm style** — use the English variant and style agreed earlier in the session. If no preference has been established, use UK English as the default. Only ask the user if you genuinely cannot determine what was agreed.
3. **Confirm documentation toolchain** — use the toolchain confirmed during plan approval. If it was not established, detect it from the project (see Toolchain Conventions below) and ask the user to confirm before proceeding. The toolchain determines file format, directory structure, docstring style, and cross-reference syntax.
4. **Apply the rules for the document type** — see below; do not deviate
5. **Write the document** to the confirmed target path using the confirmed toolchain's conventions
6. **Self-review** — check the document against the Anti-Patterns table before committing. Confirm no anti-pattern is present.
7. **Commit** — `git commit -m "docs: add [type] — [title]"`. If the directory is not inside a git repository, write the file, report the path, and stop — do not attempt to commit.

## Tutorials

A tutorial is a lesson for someone who is new to the topic. You are the instructor. The reader follows your instructions. Something real and visible happens at every step.

**Do:**

- Open with a single sentence naming what the learner will accomplish: "In this tutorial, we will build X from scratch."
- Use first-person plural throughout: "we", "let's", "our". You and the reader are doing this together.
- Make every step produce a visible, verifiable result. Show the exact expected output after each step.
- Make every decision for the reader. Choose the simplest path and follow it. No alternatives, no options, no "you could also try".
- Keep explanation to one sentence per step at most. If a concept needs more explanation, link to an explanation document — do not include it here.
- End with the completed outcome and a concrete pointer to what the reader can explore next.

**Do not:**

- Explain why something works the way it does. That belongs in an explanation document.
- Offer alternatives. Assume the reader does not know enough to judge which alternative is better.
- Skip steps because they seem obvious. If the reader has to do it, include it.
- Assume the reader has any context beyond what this tutorial has already given them.
- Use second-person commands alone ("run this", "open that"). Prefer "let's run this" — the instructor is present throughout.

## How-to Guides

A how-to guide gets a competent user from A to B. The reader has a specific goal and the competence to achieve it. They do not need motivation, background, or teaching. They need the steps.

**Do:**

- Start the title with "How to...". Always. The title names the goal, not the tool or the feature.
- Write steps, commands, and conditionals only.
- Fork where the task genuinely branches. Real workflows have decision points — capture them, label them clearly.
- Link to reference documentation for exhaustive option lists. Do not reproduce them inline.
- Assume the reader knows what they want, knows why they want it, and is capable of following instructions.
- Number every step. Use a header only when a step contains significant sub-steps.

**Do not:**

- Explain why any step is necessary unless the explanation is required to complete the step.
- Include background, history, or motivation. The reader chose this guide precisely because they already have that context.
- Begin with any preamble that delays the first actionable step. "First, make sure you understand..." is the wrong opening for a how-to guide.
- Pad with reassurances ("don't worry, this is straightforward"). The reader is competent. Treat them that way.
- Write the title from the tool's perspective ("Using the deploy command"). Write it from the user's goal ("How to deploy to production").

## Reference

Reference describes the machinery. It does not teach, instruct, or express opinions. It states facts completely and stops.

**Do:**

- Structure reference to mirror the product exactly. If the product has three modules, the reference has three sections — in the same order, using the same names.
- Cover every option, flag, field, method, and parameter. Incompleteness makes reference useless.
- Use a table for every set of structured data. The table must have exactly these four columns: option name, type, default, and description. Never omit a column.
- Format all option names, values, and inline code with backticks. When a parameter has no default, write `none`. When a parameter is required with no default, write `required`.
- Include at most one example per parameter, only where the effect cannot be stated unambiguously in prose.
- Provide complete examples at the end of the document that demonstrates the most common usage patterns. The example must be fully functional and produce the expected result when copied and run.

**Do not:**

- Instruct. "To enable X, set Y to Z" belongs in a how-to guide. Reference says: "Y accepts values [A, B, C]. Default: A."
- Explain why a design decision was made. That belongs in an explanation document.
- Express opinions or make recommendations.
- Omit options because they are rarely used. Completeness is not optional.

## Explanation

Explanation is for readers who want to understand, not act. They are not in the middle of a task. Give them the context and reasoning they need to make sense of the system.

**Do:**

- Explain design decisions and the trade-offs behind them with honesty and specificity.
- Express opinions. Recommend approaches. Explanation is the only documentation type where this is appropriate.
- Make connections to related concepts, even outside the immediate system, where they illuminate the subject.
- Write discursively. Explanation does not need to be a list. Paragraphs are fine.
- Stop when the concept is understood. Do not expand scope to cover every related concept.

**Do not:**

- Include steps or commands. Any instruction belongs in a how-to guide, not here.
- Use explanation as a dumping ground for content that did not fit elsewhere. Every document has a purpose; make this one's clear.
- Confuse explanation with reference. Reference states facts; explanation contextualises and argues.
- Write a history section that is really just a changelog. History in explanation illuminates why things are the way they are today — it does not list what changed and when.

## Anti-Patterns

| What you might do                            | Why it is wrong                                                                        |
| -------------------------------------------- | -------------------------------------------------------------------------------------- |
| Tutorial that walks through all the features | Tutorials serve learning, not feature demonstration. Pick one task; complete it fully. |
| How-to guide that opens with background      | How-to guides are for competent users. They came here to act, not to be taught.        |
| Reference that says "to use X, do Y"         | Reference describes; how-to guides instruct. Move the instruction.                     |
| Explanation that lists steps at the end      | Explanation has no steps. Move them to a how-to guide.                                 |
| Any document that covers two types           | It covers neither well. Split it into two documents.                                   |

## Toolchain Conventions

The toolchain confirmed in step 3 determines file format, directory structure, API reference approach, and cross-reference syntax. Do not guess — use what was confirmed.

**If a toolchain is already in use:**

- Read its configuration files to understand the expected directory structure and file format. Follow the existing conventions exactly.
- Place the new file where files of the same type already live. Match the format of the files that are already there.
- For API reference: check whether the toolchain auto-generates API docs from inline source comments. If it does, write or improve the inline comments rather than creating a separate reference file.
- For cross-references: use whatever syntax the existing documents use. Do not invent a new convention.
- Do not mix file formats within the same project (e.g. do not add `.md` files to a project that uses `.rst`).

**If no toolchain has been confirmed:**

Do not place any files. Ask the user what documentation tool they want to use and what file format they prefer. Once confirmed:

- Follow the tool's own conventions for directory structure and file format.
- If the tool has no strong convention, use this default structure:

```
docs/
  tutorials/
  how-to/
  reference/
  explanation/
```

Do not create empty directories. Place the file only.

## Commit Format

```bash
git add docs/path/to/new-doc.md
git commit -m "docs: add [type] — [title]"
```

Examples:

- `docs: add tutorial — getting started with the CLI`
- `docs: add how-to — deploy to production`
- `docs: add reference — configuration options`
- `docs: add explanation — why we use event sourcing`
