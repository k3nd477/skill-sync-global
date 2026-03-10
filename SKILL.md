---
name: sync-global-skills
description: Pull the latest changes from all global skill repositories in ~/.claude/skills/
model: claude-haiku-4-5-20251001
allowed-tools: Bash
---

# Sync Global Skills

Pull the latest changes from all skill repositories in your global ~/.claude/skills directory to ensure all installed skills are up to date with their remote repositories.

## Instructions

1. **List all skill directories**: Use Bash to list all directories in `~/.claude/skills/`

2. **Iterate through each directory and pull updates**:
   - For each directory that is a git repository, run: `git pull origin main`
   - Skip non-git directories (they're not repositories)
   - Catch and continue on pull errors

3. **Track results** as you go:
   - Record which skills had updates (Fast-forward, files changed)
   - Record which skills were already up to date
   - Record any errors encountered

4. **Report summary** with three sections:
   - **Updated**: List of skills with changes and brief description of what changed
   - **Already up to date**: List of skills with no changes
   - **Skipped**: Non-git directories that were skipped (optional)

## Output Format

Present results in a clear summary format:

```
## Updated Skills
- **[skill-name]**: [brief description of changes]

## Already Up to Date
- [skill-name]
- [skill-name]

## Skipped
- [non-git-directory] (not a git repository)
```

## Implementation Notes

- The global skills directory is `~/.claude/skills/` (expands to the user's home directory)
- Pull from `origin main` branch for all repositories
- Use `git status` or `git pull` output to determine if updates were made
- Continue processing all skills even if some fail
