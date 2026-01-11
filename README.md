# AI Skills

A curated collection of Agent Skills (SKILL.md standard) for working with AI agents. This repository follows the [Agent Skills specification](https://agentskills.io/specification) and is inspired by [Anthropic's skills repository](https://github.com/anthropics/skills).

## What are Skills?

Skills are folders of instructions, scripts, and resources that AI agents load dynamically to improve performance on specialized tasks. Skills teach agents how to complete specific tasks in a repeatable way, whether that's creating documents with brand guidelines, analyzing data using specific workflows, or automating personal tasks.

Each skill is self-contained in its own folder with a `SKILL.md` file containing the instructions and metadata that agents use.

## Repository Structure

```
ai-skills/
├── skills/          # Your custom skills (each skill in its own subfolder)
├── spec/            # Agent Skills specification reference
└── template/        # Template for creating new skills
```

## SKILL.md Format

A skill is a directory containing at minimum a `SKILL.md` file with YAML frontmatter followed by Markdown content.

### Required Frontmatter

```markdown
---
name: skill-name
description: A clear description of what this skill does and when to use it
---
```

### Optional Frontmatter Fields

```markdown
---
name: my-skill
description: Does something useful
license: Apache-2.0
compatibility: Requires git and docker
metadata:
  author: your-name
  version: "1.0"
allowed-tools: Bash(git:*) Read
---
```

- **`license`**: License name or reference to a bundled license file
- **`compatibility`**: Environment requirements (1-500 chars) - only include if your skill has specific requirements
- **`metadata`**: Arbitrary key-value mapping for additional metadata
- **`allowed-tools`**: Space-delimited list of pre-approved tools (experimental)

### Body Content

The Markdown body after the frontmatter contains the skill instructions. Recommended sections:

- Step-by-step instructions
- Examples of inputs and outputs
- Common edge cases
- Guidelines and best practices

**Best Practice:** Keep your main `SKILL.md` under 500 lines. Move detailed reference material to separate files.

## Optional Directories

You can include additional directories to support your skill:

- **`scripts/`**: Executable code that agents can run (Python, Bash, JavaScript, etc.)
- **`references/`**: Additional documentation loaded on demand (e.g., `REFERENCE.md`, `FORMS.md`)
- **`assets/`**: Static resources (templates, images, data files)

When referencing other files, use relative paths from the skill root:

```markdown
See [the reference guide](references/REFERENCE.md) for details.
Run the extraction script: `scripts/extract.py`
```

## Creating a Skill

1. Create a new directory in `skills/` with your skill name (lowercase, hyphens for spaces)
2. Copy `template/SKILL.md` as a starting point
3. Fill in the required frontmatter (`name` and `description`)
4. Write your instructions in the Markdown body
5. Optionally add `scripts/`, `references/`, or `assets/` directories

### Example Skill Structure

```
skills/
└── my-skill/
    ├── SKILL.md
    ├── scripts/
    │   └── process.py
    ├── references/
    │   └── REFERENCE.md
    └── assets/
        └── template.json
```

## Progressive Disclosure

Structure skills for efficient use of context:

1. **Metadata** (~100 tokens): `name` and `description` loaded at startup
2. **Instructions** (< 5000 tokens recommended): Full `SKILL.md` body loaded when skill is activated
3. **Resources** (as needed): Files in `scripts/`, `references/`, or `assets/` loaded only when required

## Validation

Use the skills-ref reference library to validate your skills:

```bash
skills-ref validate ./skills/my-skill
```

This checks that your `SKILL.md` frontmatter is valid and follows all naming conventions.

## Resources

- [Agent Skills Specification](https://agentskills.io/specification) - Complete format specification
- [Anthropic's Skills Repository](https://github.com/anthropics/skills) - Example skills and reference implementation
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills) - Overview of skills
- [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills) - Detailed guide

## License

Skills in this repository may have different licenses. Check individual skill directories for license information.
