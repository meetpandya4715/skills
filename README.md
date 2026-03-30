# agent-skills

Shared repository for reusable skills that can be adapted across AI-agent runtimes.

## Included Skills

- `repo-x-ray`: inspects a repository and generates evidence-backed Mermaid diagrams for fast codebase understanding.

## Target Runtimes

This repository is intended to hold skills that can be adapted for tools such as:

- Codex
- OpenCode
- Claude Code
- Cursor
- Gemini CLI
- other terminal-native AI agents

The goal is to keep the core skill behavior portable and keep runtime-specific glue isolated.

## Layout

```text
skills/
  repo-x-ray/
    SKILL.md
    agents/
      openai.yaml
```

- `SKILL.md`: agent-agnostic skill instructions and workflow.
- `agents/`: optional runtime-specific adapter files, prompts, or metadata.

## Usage

Use this repository as a source of portable skill definitions for AI-agent runtimes. Each platform may have its own packaging, prompt wiring, or metadata requirements, but the `skills/` directory should remain as runtime-neutral as practical.
