# skills

Reusable skills for AI agents and coding assistants.

This repository is designed to work well with the `skills` CLI and to stay portable across agents such as Codex, OpenCode, Claude Code, Cursor, Gemini CLI, and similar runtimes.

Discover installed and community skills at [skills.sh](https://skills.sh).

## Install

```bash
npx skills@latest add meetpandya4715/skills
```

### Common Commands

```bash
# Preview the skills in this repository
npx skills@latest add meetpandya4715/skills --list

# Install one skill
npx skills@latest add meetpandya4715/skills --skill repo-x-ray

# Install to specific agents
npx skills@latest add meetpandya4715/skills --skill repo-x-ray -a codex -a claude-code

# Install globally without prompts
npx skills@latest add meetpandya4715/skills --skill repo-x-ray -g -y
```

## Available Skills

### Codebase Understanding

- **repo-x-ray**  
  Inspect a repository and generate evidence-backed Mermaid diagrams for fast orientation, onboarding, and architecture review.

  ```bash
  npx skills@latest add meetpandya4715/skills --skill repo-x-ray
  ```

## Repository Layout

```text
skills/
  repo-x-ray/
    SKILL.md
    agents/
      openai.yaml
```

- `SKILL.md` holds the core skill instructions.
- `agents/` holds optional runtime-specific adapters, prompts, or metadata.

## Compatibility

The goal of this repository is to keep the core skill logic runtime-neutral and isolate agent-specific behavior where needed. That makes the same skill easier to adapt across tools like Codex, OpenCode, Claude Code, Cursor, and Gemini CLI.

## Contributing

Future skills in this repository should follow the same pattern:

1. Put the reusable instructions in `skills/<skill-name>/SKILL.md`.
2. Keep the frontmatter clear and discoverable with `name` and `description`.
3. Add runtime-specific adapter files only when they are actually needed.
