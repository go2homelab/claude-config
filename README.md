# Claude Code Configuration

This directory contains the Claude Code configuration for the homelab environment, synced across devices via Syncthing.

## Overview

This configuration directory is symlinked from `~/.claude` and tracked in the [go2homelab](../projects_c/go2homelab) git repository for version control.

## Key Configuration

### Network Drive Access

The `settings.json` file includes permissions for automatic access to the network drive without prompts:

```json
"permissions": {
  "additionalDirectories": [
    "/Volumes/studioB"
  ]
}
```

### Network Drive Details

- **Mount Point**: `/Volumes/studioB`
- **Type**: SMB/CIFS network share
- **Purpose**: Shared storage accessible across the homelab network
- **Syncthing**: Configuration is synced via Syncthing in the `~/studiobsync/2.homelab` directory

## Setup

### Initial Setup

1. **Mount the network drive** (macOS):
   ```bash
   # Finder → Go → Connect to Server (⌘K)
   # Enter: smb://server-name-or-ip/studioB
   ```

2. **Symlink configuration**:
   ```bash
   # The ~/.claude directory should be symlinked to this location
   ln -s ~/studiobsync/2.homelab/claude_config ~/.claude
   ```

3. **Git tracking**:
   ```bash
   # Configuration is tracked via symlink in go2homelab repository
   cd ~/studiobsync/2.homelab/projects_c/go2homelab
   ln -s ../../claude_config claude_config
   git add claude_config
   ```

### Syncing to Other Devices

When setting up on a new device that syncs this Syncthing folder:

1. Wait for Syncthing to sync the `claude_config` directory
2. Create the symlink: `ln -s ~/studiobsync/2.homelab/claude_config ~/.claude`
3. Mount the studioB network drive
4. Claude Code will automatically have access to the network drive

## Structure

- `settings.json` - Main Claude Code configuration
- `history.jsonl` - Conversation history (not committed to git)
- `plugins/` - Installed plugins
- `skills/` - Custom skills
- `projects/` - Project-specific configurations
- `todos/` - Task lists and todo items

## Enabled Plugins

- `document-skills@anthropic-agent-skills` - Document handling (XLSX, DOCX, PDF, PPTX)
- `superpowers@superpowers-dev` - Enhanced development workflows
- `internal-comms@awesome-claude-skills` - Internal communications templates
- `mcp-builder@awesome-claude-skills` - MCP server development
- `skill-creator@awesome-claude-skills` - Skill creation tools
- `file-organizer@awesome-claude-skills` - File organization utilities

## Maintenance

### Backup

This configuration is backed up in three ways:
1. **Syncthing** - Real-time sync across devices
2. **Git** - Version control in go2homelab repository
3. **GitHub** - Remote backup at go2homelab/go2homelab

### Updates

When modifying `settings.json`:
1. Edit the file directly in this directory
2. Changes sync automatically via Syncthing
3. Commit changes to git repository for version control
4. Push to GitHub for team access

## Troubleshooting

### Network Drive Not Accessible

If Claude Code can't access `/Volumes/studioB`:
1. Verify the drive is mounted: `ls /Volumes/`
2. Check the mount point matches: `readlink /Volumes/studioB`
3. Reconnect via Finder if needed
4. Verify settings.json has the correct path in `additionalDirectories`

### Configuration Not Loading

If Claude Code isn't using this configuration:
1. Verify symlink: `readlink ~/.claude` should show this directory
2. Check file permissions: `ls -la ~/studiobsync/2.homelab/claude_config/`
3. Restart Claude Code

## Related Documentation

- [go2homelab Repository](../projects_c/go2homelab/README.md) - Main homelab documentation
- [Claude Code Docs](https://docs.claude.com/en/docs/claude-code) - Official documentation
