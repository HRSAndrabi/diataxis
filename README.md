# diataxis

A Claude Code plugin that surveys your project's documentation, identifies every gap, and writes new documents one at a time — with your approval at every stage.

## What is Diataxis?

[Diataxis](https://diataxis.fr) is a framework for classifying documentation by purpose, and using that classification to identify gaps and plan improvements. This plugin implements the Diataxis framework as a structured process for improving your project's documentation.

This plugin is designed to be used iteratively. It surveys your project, produces a plan for what documentation is missing, and waits for your approval before writing anything. You can choose to have it write documents inline in this session, or dispatch subagents to write them one at a time while you review the output.

Features:

- Comprehensive survey of your project's documentation
- Structured gap analysis and improvement plan based on the Diataxis framework
- Writing new documents one at a time, with your approval at every stage

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
