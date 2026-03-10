# Sync Global Skills Developer Documentation

## Skill Architecture

**Skill Type**: Maintenance utility (instruction-based)
**Purpose**: Automate syncing all globally installed skills with their remote repositories
**No Configuration Required**: Works with standard ~/.claude/skills directory structure

## Technical Design

### Execution Flow

1. **Discovery Phase**:
   - List all directories in `~/.claude/skills/` (non-hidden)
   - For each directory, check if it contains a `.git` subdirectory
   - Separate git repositories from non-git directories

2. **Pull Phase**:
   - For each git repository, execute: `git -C <dir> pull origin main`
   - Capture stdout and stderr to determine outcome
   - Continue on failure rather than stopping

3. **Reporting Phase**:
   - Parse pull output to categorize results:
     - "Already up to date" → No changes
     - "Fast-forward" or "files changed" → Updated with changes
     - Error messages → Failed to pull
   - Format and present results to user

### Implementation Notes

- Uses `git pull origin main` rather than separate `fetch` and `merge` for simplicity
- Assumes all repositories use `main` as default branch
- Does not attempt to resolve merge conflicts (user should investigate manually)
- Non-git directories are gracefully skipped without error

## Integration with K3ND477 Skills Ecosystem

**Part of**: K3ND477 Skills collection
**Related Skills**: None (standalone maintenance utility)
**Depends on**: User having git and ~/.claude/skills directory structure

## Future Enhancements

Potential improvements to consider:

- **Dry run option**: Show what would be pulled without actually pulling
- **Selective sync**: Allow specifying which skills to update
- **Branch flexibility**: Option to pull from branches other than `main`
- **Merge conflict handling**: Detect and report merge conflicts
- **Activity logging**: Store sync history with timestamps
- **Auto-sync scheduling**: Use CronCreate to run on a schedule

## Testing

When modifying this skill:

1. **Basic test**: Run skill in a directory with mixed git and non-git subdirectories
2. **Edge cases**:
   - Empty ~/.claude/skills directory
   - Repositories with unstaged changes
   - Repositories missing remote origin
   - Network failures when pulling
3. **Integration**: Verify skill works alongside other global skills

## Configuration

No configuration file needed. The skill automatically:
- Discovers all directories in ~/.claude/skills/
- Uses `origin` as the remote name
- Targets `main` branch for pulls
- Continues on errors

## Maintenance Notes

- This skill itself can be included in sync operations (if installed globally)
- Keep SKILL.md instructions explicit and step-by-step
- Update README.md if workflow changes significantly
