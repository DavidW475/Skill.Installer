---
name: create-installer-skill
description: "Create a new AI skill in skill-installer format. Use when: creating a new skill, adding a skill to a skill repository, scaffolding a Skill.md with frontmatter, generating skill folder structure with CHANGELOG.md."
argument-hint: "Skill name and purpose, e.g. 'go-senior-dev — Senior Go developer persona'"
metadata:
   version: "1.1.0"
---

# Create Skill (skill-installer format)

## What This Skill Does

Scaffolds a complete skill folder ready for use with [skill-installer](https://github.com/davidrenne/skill-installer).
A skill is a directory containing a `Skill.md` (with YAML frontmatter) and an optional `CHANGELOG.md`.

## Skill Folder Structure

```
<skill-name>/
├── Skill.md          ← Required: metadata frontmatter + instructions body
├── CHANGELOG.md      ← Required: referenced by Skill.md frontmatter
└── (optional extra files: scripts/, references/, assets/, ...)
```

## Skill.md Format

The file MUST begin with a YAML frontmatter block delimited by `---`.

```
---
name: "<kebab-case-name>"           # Required. Must match the folder name exactly.
version: "<semver>"                  # Required. Start at "1.0.0".
description: "<one-line summary>"    # Required.
author: "<name or team>"             # Recommended.
tags: ["<tag1>", "<tag2>"]           # Optional. Lowercase keywords.
min_installer_version: "1.0.0"       # Optional. Minimum skill-installer version required.
changelog: "CHANGELOG.md"            # Optional. Path relative to skill folder.
---

# (skill body follows — plain markdown)
```

**Rules:**
- `name` must be lowercase, alphanumeric, hyphens only (e.g. `go-senior-dev`)
- `version` must follow semver (`MAJOR.MINOR.PATCH`)
- The folder name must match `name` exactly

## CHANGELOG.md Format

```markdown
# Changelog

## [1.0.0] — YYYY-MM-DD
### Added
- Initial release
```

## Procedure

1. **Gather information** — if the user's request is incomplete, ask for:
   - `name` (kebab-case, folder name)
   - `description` (one sentence)
   - `author`
   - `tags` (optional)
   - The skill's purpose / body content

2. **Determine target directory** — create the skill folder inside the current workspace or path specified by the user. If unclear, use the workspace root.

3. **Create `<name>/Skill.md`** — use the template in [./assets/Skill.md.template](./assets/Skill.md.template). Fill in all frontmatter fields. Write a meaningful body describing the skill's purpose, persona, constraints, and examples.

4. **Create `<name>/CHANGELOG.md`** — use the template in [./assets/CHANGELOG.md.template](./assets/CHANGELOG.md.template). Set today's date and version `1.0.0`.

5. **Validate** — confirm the created `Skill.md` passes these checks:
   - Starts with `---`
   - `name` matches the folder name
   - `version` is present and valid semver
   - Frontmatter closes with `---` on its own line

6. **Report** — tell the user:
   - The folder path created
   - How to add the skill's parent repository as a source in skill-installer
   - Example: `skill-installer` → `s` → `n` → enter repo URL
