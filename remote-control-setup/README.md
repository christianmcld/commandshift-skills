# Remote Control Setup

A Claude Code skill/guide for setting up remote access to Claude Code from your phone. Control Claude Code from anywhere with SSH tunneling, a task queue system, and status monitoring.

## What It Does

- Configures SSH server with key-based authentication
- Sets up secure remote access via Tailscale, Cloudflare Tunnel, or ngrok
- Creates a task queue system that watches for new tasks and runs them through Claude Code
- Installs a background service (launchd/systemd) to keep the task runner alive
- Provides a lightweight HTTP status endpoint for phone monitoring
- Includes security hardening checklist

## Installation

```bash
mkdir -p ~/.claude/commands
cp skill.md ~/.claude/commands/remote-control-setup.md
```

## Example Usage

```
/remote-control-setup

Set up remote access to Claude Code on this Mac using Tailscale
```

```
/remote-control-setup

I want to control Claude Code from my iPhone — walk me through the setup
```

```
/remote-control-setup

Configure the task runner and launchd service so I can submit tasks via SSH
```

## Requirements

- **SSH server** — Built into macOS and Linux
- **Tailscale** (recommended), **Cloudflare Tunnel**, or **ngrok** — For remote connectivity
- **Claude Code CLI** — Must be installed and authenticated on the server
- **Phone SSH client** — Termius, Blink Shell (iOS), or Termux (Android)

## Architecture

```
Phone (SSH client)
    |
    v
[Tailscale/Cloudflare/ngrok tunnel]
    |
    v
Server running Claude Code
    |
    ├── ~/claude-remote/task-runner.sh  (background service)
    ├── ~/claude-remote/queue/          (task files dropped here)
    ├── ~/claude-remote/logs/           (task output logs)
    └── ~/claude-remote/status.json     (current status)
```
