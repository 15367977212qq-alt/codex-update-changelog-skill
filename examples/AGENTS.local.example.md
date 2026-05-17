# Project Instructions

## Required skill: update-changelog

Whenever source code, configuration, tests, scripts, migrations, schemas, frontend components, backend services, deployment files, Docker / CI files, dependency files, or documentation related to code behavior are modified, Codex must update `CHANGELOG.md` before finishing the task.

Use this skill file:

`.codex/skills/update-changelog-local/SKILL.md`

If the skill is installed globally, use:

`C:\Users\你的用户名\.codex\skills\update-changelog-local\SKILL.md`

## Required behavior

Before finishing any code-changing task, Codex must:

1. Inspect the final diff with:
   - `git diff --name-only`
   - `git diff`
2. Update the repository root `CHANGELOG.md` according to the `update-changelog` skill.
3. Record actual changed files.
4. Record verification result.
5. Use the daily archive rule from the skill.
6. Archive the previous day's changelog to the configured local archive directory.
7. Reset repository root `CHANGELOG.md` to the initial template after archiving.
8. Do not use the old 7-day archive rule.
9. Do not finish a code-changing task without updating `CHANGELOG.md`.

## Notes

- The detailed changelog format, category rules, verification format, and archive behavior are defined in the skill file.
- Do not duplicate the full skill content here.