# diataxis

A Claude Code plugin that surveys your project's documentation, identifies every gap, and writes new documents one at a time — with your approval at every stage.

## Installation

```bash
claude plugin install https://github.com/andrabis/diataxis
```

## Usage

Run from any project directory:

```
/diataxis:document
```

The plugin reads your codebase, classifies what documentation already exists, produces a structured plan for what is missing, and waits for your approval before writing a single word.

## Skills

| Skill                | Purpose                                                                                             |
| -------------------- | --------------------------------------------------------------------------------------------------- |
| `diataxis:document`  | Entry point. Survey → plan → confirm → write.                                                       |
| `diataxis:survey`    | Survey the codebase and return a structured gap analysis. Run standalone if you only want the plan. |
| `diataxis:write-doc` | Write a single document of a specified type. Run standalone if you know exactly what you need.      |
