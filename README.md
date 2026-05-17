# Codex Update Changelog Skill

A Codex skill for automatically updating `CHANGELOG.md` after code changes.

This skill helps Codex inspect the final `git diff`, identify changed files, categorize changes, record verification results, and maintain a daily changelog workflow.

It provides two variants:

1. `update-changelog-obsidian`
   - Records daily changes in repository root `CHANGELOG.md`
   - Archives previous daily changelogs into an Obsidian Vault directory
   - Adds Obsidian-compatible YAML frontmatter to archived files
   - Supports Dataview-based changelog indexing

2. `update-changelog-local`
   - Records daily changes in repository root `CHANGELOG.md`
   - Archives previous daily changelogs into a normal local directory
   - Keeps archived files as plain Markdown
   - Does not require Obsidian

---

## Features

- Automatically updates `CHANGELOG.md` after code modifications
- Groups changes by date
- Categorizes changes into:
  - Added
  - Changed
  - Fixed
  - Removed
  - Verification
  - Notes
- Records changed file paths
- Records test or verification results
- Supports daily archive workflow
- Supports Obsidian Vault archive integration
- Supports a non-Obsidian local archive mode
- Avoids the old 7-day archive rule
- Keeps configuration centralized

---

## Repository Structure

```text
codex-update-changelog-skill/
├── README.md
├── LICENSE
├── .gitignore
├── skills/
│   ├── update-changelog-obsidian/
│   │   └── SKILL.md
│   └── update-changelog-local/
│       └── SKILL.md
├── examples/
│   ├── AGENTS.obsidian.example.md
│   ├── AGENTS.local.example.md
│   ├── CHANGELOG.example.md
│   └── dataview-query.md
└── docs/
    ├── deployment.md
    ├── obsidian-integration.md
    └── git-commit-guide.md
Installation
Option 1: Install globally

Copy the skill into your Codex global skills directory:

C:\Users\<your-username>\.codex\skills\

Example:

C:\Users\<your-username>\.codex\skills\update-changelog-obsidian\SKILL.md
C:\Users\<your-username>\.codex\skills\update-changelog-local\SKILL.md
Option 2: Install inside a project

Copy the skill into your project repository:

your-project/
└── .codex/
    └── skills/
        ├── update-changelog-obsidian/
        │   └── SKILL.md
        └── update-changelog-local/
            └── SKILL.md
Basic CHANGELOG.md Template

Create a CHANGELOG.md file in the repository root:

# CHANGELOG

## Unreleased

暂无变更。
AGENTS.md Configuration

Add an AGENTS.md file to your project root.

For the Obsidian version:

# Project Instructions

## Required skill: update-changelog

Whenever source code, configuration, tests, scripts, migrations, schemas, frontend components, backend services, deployment files, Docker / CI files, dependency files, or documentation related to code behavior are modified, Codex must update `CHANGELOG.md` before finishing the task.

Use this skill file:

`.codex/skills/update-changelog-obsidian/SKILL.md`

Before finishing any code-changing task, Codex must:

1. Inspect the final diff with:
   - `git diff --name-only`
   - `git diff`
2. Update the repository root `CHANGELOG.md` according to the `update-changelog` skill.
3. Record actual changed files.
4. Record verification result.
5. Use the daily archive rule from the skill.
6. Archive the previous day's changelog to the configured Obsidian archive directory.
7. Reset repository root `CHANGELOG.md` to the initial template after archiving.
8. Do not use the old 7-day archive rule.
9. Do not finish a code-changing task without updating `CHANGELOG.md`.

For the local version, replace the skill path with:

.codex/skills/update-changelog-local/SKILL.md
Configuration

Each SKILL.md contains a Configuration section.

For the Obsidian version, update:

Project name
Archive directory
Archive directory for Git Bash
Obsidian Dataview source path
Obsidian frontmatter template

For the local version, update:

Project name
Archive directory
Archive directory for Git Bash
Obsidian Dataview Example

If you use the Obsidian version, add this query to your Obsidian project homepage:

TABLE date AS 日期, file.link AS 日志, source AS 来源
FROM "bi_project/CHANGELOG"
WHERE type = "changelog" AND project = "bi_project"
SORT date DESC
LIMIT 10
Recommended Git Commit Format
docs: add codex update changelog skill

or:

feat: add daily changelog archive workflow# codex-update-changelog-skill
