# Sync Global Skills

Pull the latest changes from all skill repositories in your global ~/.claude/skills directory to keep your installed skills up to date.

## Installation

### Git Submodule

```bash
# From your project's .claude/skills directory
git submodule add https://github.com/k3nd477/sync-global-skills .claude/skills/sync-global-skills
```

### Manual Clone

```bash
# Clone directly to your global skills directory
cd ~/.claude/skills
git clone https://github.com/k3nd477/sync-global-skills sync-global-skills
```

## Usage

Use the `/sync-global-skills` slash command in Claude Code:

```bash
/sync-global-skills
```

This will:
1. Scan your `~/.claude/skills/` directory for all skill repositories
2. Pull the latest changes from each repository's `origin main` branch
3. Report which skills were updated and which are already current

## Example Output

```
## Updated Skills
- **faq-skill**: Added model version specifier
- **issue**: Updated documentation and added model version

## Already Up to Date
- seo-strategy
- seo-content-drafts
- transcript-seo

## Skipped
- generate-llms-txt (not a git repository)
- using-xcode-cli (not a git repository)
```

## Use Cases

- **Keep skills current**: After updating skill repositories, sync your global installation to get the latest features and bug fixes
- **Team collaboration**: Ensure all team members have the same skill versions
- **Maintenance routine**: Run periodically to catch updates to dependencies and improvements
- **Before important work**: Sync before starting content workflows to ensure you have the latest tools

## Notes

- Non-git directories are skipped (e.g., utility directories that aren't version-controlled)
- The skill continues processing even if individual repositories fail to pull
- All skills pull from the `main` branch of their remote `origin`
- No configuration required—works with your existing ~/.claude/skills setup

## Repository

https://github.com/k3nd477/sync-global-skills
