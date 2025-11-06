# Claude Code Session Context

This file provides context for Claude Code sessions to quickly understand the homelab environment setup.

## Environment Overview

This is a **homelab environment** with enterprise-grade networking, storage, and development tools. The setup includes Proxmox virtualization, TrueNAS storage, UniFi networking, and extensive automation.

## Key Directories

- **Home**: `/Users/gru/`
- **Syncthing Root**: `~/studiobsync/2.homelab/`
- **Main Homelab Repo**: `~/studiobsync/2.homelab/projects_c/go2homelab/`
- **Claude Config**: `~/.claude/` (symlinked to `~/studiobsync/2.homelab/claude_config/`)
- **Obsidian Vault (_career_obs)**: `/Users/gru/Library/Mobile Documents/com~apple~CloudDocs/_career_obs/` (iCloud synced)
- **Obsidian Vault (medfam_obs)**: `/Users/gru/medfam_obs/` (Medical family tracking)
- **Network Drive**: `/Volumes/studioB/` (SMB/CIFS share - always accessible)

## Network Storage

### studioB Network Drive

- **Path**: `/Volumes/studioB/`
- **Type**: SMB/CIFS network share
- **Server**: 192.168.3.50 (gnas._smb._tcp.local)
- **Status**: Pre-configured in permissions - no prompts needed
- **Purpose**: Shared homelab storage accessible across all devices
- **Configuration**: See `settings.json` → `permissions.additionalDirectories`
- **Reconnect Script**: `~/studiobsync/2.homelab/scripts/reconnect-smb-drives.sh`

### allgfamdocs Network Drive

- **Path**: `/Volumes/allgfamdocs/`
- **Type**: SMB/CIFS network share
- **Server**: 192.168.3.50 (gnas._smb._tcp.local)
- **Status**: Pre-configured in permissions - no prompts needed
- **Purpose**: Shared homelab storage accessible across all devices
- **Configuration**: See `settings.json` → `permissions.additionalDirectories`
- **Reconnect Script**: `~/studiobsync/2.homelab/scripts/reconnect-smb-drives.sh`

## Syncthing Setup

Configuration and important files are synced across devices via Syncthing:

- **Sync Folder**: `~/studiobsync/2.homelab/`
- **Claude Config**: Synced at `~/studiobsync/2.homelab/claude_config/`
- **Symlink**: `~/.claude` → `~/studiobsync/2.homelab/claude_config/`

This means any changes to Claude Code configuration sync automatically across devices.

## Git Repositories

### go2homelab

- **Location**: `~/studiobsync/2.homelab/projects_c/go2homelab/`
- **Remote**: `github.com:go2homelab/go2homelab.git`
- **Purpose**: Homelab infrastructure documentation and configuration
- **Tracked Items**:
  - Infrastructure documentation
  - Network configuration details
  - Claude Code configuration (via symlink)
  - Homelab setup guides

## Infrastructure Stack

- **Hypervisor**: Proxmox
- **NAS**: TrueNAS, ZimoOS
- **Networking**: UniFi (UCG Fiber, multiple switches, WiFi 7 APs)
- **Orchestration**: Docker Compose
- **Automation**: n8n
- **AI Assistant**: Claude Code (that's you!)

## Network Hardware

Extensive UniFi deployment:
- **Gateway**: UCG Fiber
- **Switches**: Pro XG 8 PoE, US 48 PoE, US 16 PoE, multiple Flex switches with 10GbE and multi-gig
- **Access Points**: 3x U7 Pro (WiFi 7), U7 In-Wall, U6 IW

## Important Notes for Claude Sessions

1. **Network Drive**: `/Volumes/studioB` is always accessible - no permission prompts needed
2. **Configuration Persistence**: All Claude Code config changes are synced via Syncthing and tracked in git
3. **Working Directory**: Current session started in `~/studiobsync/2.homelab/projects_c/go2homelab/`
4. **Commit Style**: This user likes descriptive commits with the Claude Code attribution footer
5. **Documentation**: User values thorough documentation - don't hesitate to be detailed

## Common Tasks

### Committing Changes

When committing, follow these patterns seen in the repository:
- Clear, descriptive commit messages
- Include what changed and why
- Add Claude Code attribution footer
- Push to GitHub after committing

### Accessing Network Storage

Simply use `/Volumes/studioB/path/to/file` - it's pre-configured in permissions.

### Reconnecting SMB Drives

If the network drives become disconnected, use the reconnect script:
```bash
~/studiobsync/2.homelab/scripts/reconnect-smb-drives.sh
```

This script automatically reconnects:
- `/Volumes/studioB` from 192.168.3.50
- `/Volumes/allgfamdocs` from 192.168.3.50

The drives are hosted on `gnas._smb._tcp.local` and mount as SMB shares.

### Accessing Obsidian Vaults

**_career_obs vault:** `/Users/gru/Library/Mobile Documents/com~apple~CloudDocs/_career_obs/` (iCloud synced)

**medfam_obs vault:** `/Users/gru/medfam_obs/` (Medical family tracking - used by gmed agent)

### Documentation

Documentation is highly valued here. When making changes:
1. Update relevant README files
2. Keep this CLAUDE.md file current
3. Commit documentation changes to git
4. Ensure Syncthing syncs across devices

## Quick Reference

```bash
# Main homelab repository
cd ~/studiobsync/2.homelab/projects_c/go2homelab/

# Claude configuration
#cd ~/.claude/  # or ~/studiobsync/2.homelab/claude_config/
cd ~/studiobsync/2.homelab/claude_config/

# Obsidian vault (_career_obs)
cd "/Users/gru/Library/Mobile Documents/com~apple~CloudDocs/_career_obs/"

# Obsidian vault (medfam_obs) - Medical family tracking
cd /Users/gru/medfam_obs/

# Network drive
cd /Volumes/studioB/

# Reconnect SMB drives
~/studiobsync/2.homelab/scripts/reconnect-smb-drives.sh

# Check Syncthing sync status
ls -la ~/studiobsync/2.homelab/
```

## Resources

- [go2homelab README](studiobsync/2.homelab/projects_c/go2homelab/README.md)
- [Claude Config README](studiobsync/2.homelab/claude_config/README.md)
- [Claude Code Docs](https://docs.claude.com/en/docs/claude-code)
