# codex-skills

Shared repository for reusable skills that can be adapted for multiple AI agents.

## Included Skills

- `repo-x-ray`: inspects a repository and generates evidence-backed Mermaid diagrams for fast codebase understanding.

## Layout

```text
skills/
  repo-x-ray/
    SKILL.md
    agents/
      openai.yaml
```

## Usage

Use this repository as a source of portable skill definitions for AI-agent runtimes. Each agent platform may have its own packaging or installation requirements, but the `skills/` directory is intended to stay reusable and agent-agnostic.
