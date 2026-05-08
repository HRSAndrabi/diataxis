# diataxis

A Claude plugin that surveys your codebase, classifies your existing documentation using the [Diataxis framework](https://diataxis.fr), identifies every gap, produces a structured plan, and then writes documentation one document at a time — with your approval at every stage.

## What is Diataxis?

Diataxis is a framework for organising technical documentation into four distinct types, each serving a different reader in a different situation. Mixing types is the single most common documentation failure. This plugin prevents it.

**Tutorials** are lessons. The reader is a beginner. Every step produces a visible result. The writer is responsible for the learner's success.

**How-to guides** are directions. The reader is competent and has a specific goal. Skip the background. Get them there.

**Reference** is a map of the machinery. Every option, flag, and field. Neutral and complete. No instructions, no opinions.

**Explanation** is for understanding. Design decisions, trade-offs, history. The only type where expressing an opinion is appropriate.

## Why this matters

Most documentation fails because it tries to serve multiple readers in multiple situations in a single document. A README that is simultaneously a getting-started tutorial, an API reference, and a design manifesto serves none of those readers well.

Diataxis solves this by giving every document a clear, singular purpose. This plugin enforces that discipline.

## Installation

```bash
claude plugin install https://github.com/andrabis/diataxis
```

## Usage

To survey your project and start planning documentation improvements:

```
/diataxis:document
```

The plugin surveys your codebase, classifies what exists, identifies gaps, and presents a plan for your approval before writing a single word.

### Skills

| Skill                | Purpose                                                                                             |
| -------------------- | --------------------------------------------------------------------------------------------------- |
| `diataxis:document`  | Entry point. Survey → plan → confirm → write.                                                       |
| `diataxis:survey`    | Survey the codebase and return a structured gap analysis. Run standalone if you only want the plan. |
| `diataxis:write-doc` | Write a single document of a specified type. Run standalone if you know exactly what you need.      |

## Licence

MIT
