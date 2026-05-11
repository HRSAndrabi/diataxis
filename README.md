# diataxis

A Claude Code plugin that surveys a project, plans a Diátaxis documentation system, and rewrites the approved documents one at a time.

## What is Diataxis?

[Diataxis](https://diataxis.fr) is a framework for classifying documentation by purpose, and using that classification to identify gaps and plan improvements. This plugin implements the Diataxis framework as a structured process for improving your project's documentation.

This plugin is designed as an orchestrated documentation rewrite. It surveys your project, produces a plan, waits for approval, then rewrites your documentation one document at a time. Each document is validated and routed to the correct type-specific writer based on its Diataxis classification.

Features:

- Comprehensive survey of your project's documentation
- Structured gap analysis and improvement plan based on the Diataxis framework
- Document-by-document implementation through type-specific Diátaxis writers

## Installation

```bash
claude plugin install https://github.com/andrabis/diataxis
```

## Usage

Run from any project directory:

```
/diataxis:document
```

The plugin reads your codebase, classifies existing documentation, produces a structured plan, and waits for approval before writing. After approval, `diataxis:document` sends each planned document to `diataxis:write-doc`, which validates the document context and routes to the correct writer.

## Skills

| Skill                   | Purpose                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------ |
| `diataxis:document`     | Entry point. Survey, plan, request approval, then orchestrate document implementation.           |
| `diataxis:survey`       | Survey the codebase and write `docs/diataxis/plan.md`. Run standalone if you only want the plan. |
| `diataxis:write-doc`    | Validate one planned document context and route it to the right writer.                          |
| `diataxis:tutorial`     | Write beginner-focused tutorials.                                                                |
| `diataxis:how-to-guide` | Write task-focused how-to guides.                                                                |
| `diataxis:reference`    | Write neutral, structured reference documentation.                                               |
| `diataxis:explanation`  | Write conceptual explanation documentation.                                                      |
