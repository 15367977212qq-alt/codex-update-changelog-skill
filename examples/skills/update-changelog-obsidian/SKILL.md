记得在使用前修改如下部分内容
将下述内容复制黏贴到C：/用户/你的用户名/.codex/skills/update-changelog/SKILL.md
# update-changelog

## Purpose

每次代码修改完成后，更新项目根目录 `CHANGELOG.md`，按当天日期记录本次修改内容。

该 skill 使用按日归档机制：

- 项目根目录 `CHANGELOG.md` 只保存当天修改日志。
- 当进入新的一天时，先将上一天的 `CHANGELOG.md` 归档到配置的本地目录。
- 归档完成后，将项目根目录 `CHANGELOG.md` 重置为初始模板。
- 然后再创建当天日志并记录新的修改内容。

---

## Configuration

修改不同项目时，优先修改本节配置，不要在正文中分散修改路径或项目名。

### Project name

```text
改为你的项目名称
Archive directory
归档上一天 changelog 的目标目录：
<改为你想把每日日志归档到的目标地址>
Archive directory for Git Bash
如果在 Git Bash 中执行命令，使用下面路径：
<改为你想把每日日志归档到的目标地址>
Archive filename format
CHANGELOG_YYYY-MM-DD.md

When to use
Use this skill whenever any of the following files are modified:
● Source code

● Configuration files

● Tests

● Scripts

● Database migrations

● API schemas

● Frontend components

● Backend services

● Documentation related to code behavior

● Deployment files

● Docker files

● CI / workflow files

● Project dependency files

This skill must be used before finishing any task that changes files.
If there are no actual file changes, do not update CHANGELOG.md.

Core requirements
Before finishing any task that changes files, Codex must:
1. Inspect the final diff of the current task.

2. Identify all changed files.

3. Determine today’s local date.

4. Check whether repository root CHANGELOG.md exists.

5. If CHANGELOG.md belongs to a previous date, archive it before writing today’s changelog.

6. Reset repository root CHANGELOG.md after archiving a previous day.

7. Find or create today’s changelog section in repository root CHANGELOG.md.

8. Categorize changes into:

    ○ Added

    ○ Changed

    ○ Fixed

    ○ Removed

    ○ Verification

    ○ Notes

9. Update only today’s ## Unreleased section.

10. Do not invent changes that are not visible in the final diff.

11. Keep entries concise and specific.

12. Use Chinese for changelog content unless the repository already uses English.

13. Mention file paths only in Notes; do not repeat file paths in every change bullet.

14. Do not overwrite historical archive files.

15. Do not use the old 7-day archive rule.

16. Do not finish a code-changing task without updating CHANGELOG.md.


Date format
Always use this date format:
YYYY-MM-DD
Correct:
## 2026-05-17
Incorrect:
## 2026-5-17

Repository root CHANGELOG.md behavior
The repository root CHANGELOG.md is the active daily changelog.
It should only contain the current day’s changelog.
If no changelog has been written yet, or after a previous day has been archived, use this initial template:
# CHANGELOG

## Unreleased

暂无变更。
When the first code modification of the day is recorded, replace the placeholder with today’s date section.

Initial CHANGELOG.md template
If repository root CHANGELOG.md does not exist, create it with:
# CHANGELOG

## Unreleased

暂无变更。

Daily changelog structure
Use this structure in repository root CHANGELOG.md:
# CHANGELOG

## YYYY-MM-DD

## Unreleased

### Added
- 新增了 xxx。

### Changed
- 修改了 xxx。

### Fixed
- 修复了 xxx。

### Removed
- 删除了 xxx。

### Verification
- 运行：无
- 结果：未运行测试

### Notes
- 修改文件：
  - `path/to/file1`
  - `path/to/file2`
- 遗留问题：无

Daily writing rules
If today’s date section does not exist
Create today’s date section in CHANGELOG.md.
Example:
# CHANGELOG

## 2026-05-17

## Unreleased

### Added

### Changed

### Fixed

### Removed

### Verification

### Notes
Then write the current task’s changelog entries under the proper categories.

If today’s date section already exists
Append new entries under the existing category.
Example:
### Changed
- 修改了用户登录接口的参数校验。
- 调整了订单列表的分页逻辑。
Do not duplicate the same entry if it already exists.

If a category does not exist
Create the missing category under today’s ## Unreleased.
Required category order:
### Added

### Changed

### Fixed

### Removed

### Verification

### Notes

Category rules
Added
Use this section for newly added files, features, APIs, components, scripts, migrations, tests, or documentation.
Example:
### Added
- 新增了清洗任务重试接口。

Changed
Use this section for modified behavior, refactoring, configuration changes, documentation updates, API contract changes, dependency updates, or UI adjustments.
Example:
### Changed
- 调整了清洗任务状态流转逻辑。
If the task only changes documentation, record it under Changed.
Example:
### Changed
- 更新了接口部署说明。

Fixed
Use this section for bug fixes, error handling fixes, compatibility fixes, incorrect logic fixes, broken test fixes, or runtime error fixes.
Example:
### Fixed
- 修复了任务失败后重试次数未正确增加的问题。

Removed
Use this section for removed files, deleted APIs, removed fields, removed dependencies, or deprecated logic deletion.
Example:
### Removed
- 删除了旧版批量任务状态字段。

Verification
Always include verification information.
If tests were run successfully:
### Verification
- 运行：`pytest`
- 结果：通过
If tests failed:
### Verification
- 运行：`pytest`
- 结果：失败，失败原因：xxx
If no tests were run:
### Verification
- 运行：无
- 结果：未运行测试
If only syntax or build verification was run:
### Verification
- 运行：`python -m compileall app`
- 结果：通过

Notes
Always include changed files and remaining issues.
Example:
### Notes
- 修改文件：
  - `app/api/v1/clean_jobs.py`
  - `app/services/clean_job_service.py`
  - `CHANGELOG.md`
- 遗留问题：无
If there are known unresolved issues:
### Notes
- 修改文件：
  - `app/tasks/clean_worker.py`
  - `CHANGELOG.md`
- 遗留问题：清洗任务并发执行逻辑仍未接入队列。

Daily archive rule
This skill uses daily changelog archiving.
The old 7-day archive rule is no longer used.
Archive trigger
Before writing today’s changelog, Codex must check whether repository root CHANGELOG.md contains a date section from a previous day.
A date section looks like:
## YYYY-MM-DD
Archive is triggered when all of the following are true:
1. CHANGELOG.md exists.

2. CHANGELOG.md contains an actual date section.

3. The date section is earlier than today.

4. CHANGELOG.md contains actual changelog content, not only the initial template.

5. No archive file already exists for the same date.

Do not archive if:
● CHANGELOG.md only contains the initial template.

● CHANGELOG.md already belongs to today.

● There are no actual changelog entries.

● The only change is a changelog-only update without source/config/doc behavior changes.


Archive directory
Archive previous daily changelogs to the configured archive directory.
The archive directory is defined in:
Configuration → Archive directory
If the directory does not exist, create it.
Archive filename format is defined in:
Configuration → Archive filename format
Example archive filename:
CHANGELOG_2026-05-17.md
Use the date from the archived CHANGELOG.md date section as the archive filename date.

Archive file structure
Archived files are plain Markdown files.
Do not add Obsidian frontmatter, metadata, tags, or Dataview-specific fields.
Archive file content should preserve the previous day’s CHANGELOG.md content exactly.
Example archived file:
# CHANGELOG

## 2026-05-17

## Unreleased

### Added
- 新增了 Facebook 工作台 token 可用性检查逻辑。

### Changed
- 调整了 Facebook 初始化失败时的错误提示。

### Fixed
- 修复了代理端口解析错误导致 token 全部不可用的问题。

### Removed

### Verification
- 运行：无
- 结果：未运行测试

### Notes
- 修改文件：
  - `app/services/facebook_service.py`
  - `app/core/config.py`
  - `CHANGELOG.md`
- 遗留问题：无

Archive behavior
When archiving a previous day’s changelog, Codex must:
1. Read the date from the previous day’s date section in repository root CHANGELOG.md.

2. Create the configured archive directory if it does not exist.

3. Create an archive file using this filename format:

CHANGELOG_YYYY-MM-DD.md
4. Preserve the previous day’s changelog content exactly.

5. Do not overwrite an existing archive file.

6. If an archive file already exists for the same date, append a timestamp suffix or report the conflict clearly.

7. After successful archive, reset repository root CHANGELOG.md to the initial template.

8. Do not archive today’s active changelog.

9. Do not archive empty or placeholder changelog content.


Root CHANGELOG.md reset format after archive
After archiving a previous day’s changelog, reset repository root CHANGELOG.md to:
# CHANGELOG

## Unreleased

暂无变更。
Then create today’s date section when writing the current task’s changelog.

Released version preservation
If repository root CHANGELOG.md contains released historical versions, do not overwrite them.
However, this project uses daily active changelog files. Released historical versions should normally be kept in archived changelog files or separate release notes, not mixed into the active daily CHANGELOG.md.
If released version sections exist in root CHANGELOG.md:
● Do not delete them without explicit user instruction.

● Do not merge daily sections into released versions unless explicitly requested by the user.

● Prefer archiving only the daily active section.

● Preserve released version sections exactly as written.


Required workflow
Before finishing a task that changes files, Codex must run or inspect equivalent output:
git diff --name-only
git diff
Then:
1. Identify changed files.

2. Check whether root CHANGELOG.md belongs to a previous date.

3. If yes, archive the previous day’s changelog to the configured archive directory.

4. Reset root CHANGELOG.md to the initial template.

5. Create today’s date section if it does not exist.

6. Update today’s ## Unreleased section.

7. Record changed files under Notes.

8. Record verification result under Verification.


Recommended command sequence
Inspect changed files:
git diff --name-only
git diff
Create archive directory on Windows PowerShell if needed:
New-Item -ItemType Directory -Force "<Archive directory>"
Example:
New-Item -ItemType Directory -Force "D:\zhr\doucument\codex_project\bi_project\CHANGELOG"
Create archive directory in Git Bash if needed:
mkdir -p "<Archive directory for Git Bash>"
Example:
mkdir -p "D:/zhr/doucument/codex_project/bi_project/CHANGELOG"

Important rules
● Do not use the old 7-day archive rule.

● Do not archive to ./changelog_archive unless it is configured as the archive directory.

● Archive previous daily changelogs only to the configured archive directory.

● Do not overwrite historical archive files.

● Do not archive today’s active changelog.

● Do not add Obsidian frontmatter.

● Do not add YAML metadata unless the user explicitly requests it.

● Do not invent changes.

● Do not include implementation guesses.

● Do not write vague entries such as “优化代码” without specifying what changed.

● Do not list file paths in every category bullet.

● Do not omit Verification.

● Do not omit Notes.

● Do not finish code-changing tasks without updating CHANGELOG.md.

● Use YYYY-MM-DD date format.

● Use Chinese for changelog content unless the repository already uses English.

● If a task changes only documentation, still record it under Changed.

● If a task changes only CHANGELOG.md, do not create another changelog entry for the changelog-only update unless it is part of a broader task.

● If there are no actual file changes, do not update CHANGELOG.md.


Example root CHANGELOG.md for active day
# CHANGELOG

## 2026-05-17

## Unreleased

### Added
- 新增了 Facebook 工作台 token 可用性检查逻辑。

### Changed
- 调整了 Facebook 初始化失败时的错误提示。

### Fixed
- 修复了代理端口解析错误导致 token 全部不可用的问题。

### Removed

### Verification
- 运行：无
- 结果：未运行测试

### Notes
- 修改文件：
  - `app/services/facebook_service.py`
  - `app/core/config.py`
  - `CHANGELOG.md`
- 遗留问题：无

Example archived changelog file
Archive path is generated from:
Configuration → Archive directory
Archive filename:
CHANGELOG_2026-05-17.md
Archive content:
# CHANGELOG

## 2026-05-17

## Unreleased

### Added
- 新增了 Facebook 工作台 token 可用性检查逻辑。

### Changed
- 调整了 Facebook 初始化失败时的错误提示。

### Fixed
- 修复了代理端口解析错误导致 token 全部不可用的问题。

### Removed

### Verification
- 运行：无
- 结果：未运行测试

### Notes
- 修改文件：
  - `app/services/facebook_service.py`
  - `app/core/config.py`
  - `CHANGELOG.md`
- 遗留问题：无

Final behavior summary
This skill ensures that:
1. Codex records every code-changing task in CHANGELOG.md.

2. The active CHANGELOG.md only contains the current day’s changes.

3. Previous daily changelogs are archived to the configured local archive directory.

4. Archived changelogs are plain Markdown files.

5. The old 7-day archive rule is not used.

6. Changing archive location only requires editing the Configuration section.