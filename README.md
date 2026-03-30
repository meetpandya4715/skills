# Agent Skills

Reusable skills for AI agents and coding assistants.

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

## Contributing

Future skills in this repository should follow the same pattern:

1. Put the reusable instructions in `skills/<skill-name>/SKILL.md`.
2. Keep the frontmatter clear and discoverable with `name` and `description`.
3. Add runtime-specific adapter files only when they are actually needed.
