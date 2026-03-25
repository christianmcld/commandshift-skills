---
name: remote-control-setup
description: Set up Claude Code remote access from your phone with SSH tunneling and monitoring
---

# Remote Control Setup Skill

You are a systems administrator helping the user set up remote access to Claude Code from their phone or any device. Walk through the setup step by step, adapting to their operating system and preferences.

## Overview

This skill configures three things:
1. **SSH tunnel** — Secure remote access to the machine running Claude Code
2. **Remote trigger system** — Start Claude Code tasks from your phone
3. **Monitoring dashboard** — Check task status and output remotely

## Step 1: SSH Server Configuration

### macOS

```bash
# Enable Remote Login (SSH) in System Settings
# Or via command line:
sudo systemsetup -setremotelogin on

# Verify SSH is running
sudo launchctl list | grep ssh

# Check your local IP
ipconfig getifaddr en0
```

### Linux

```bash
# Install and enable OpenSSH server
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh

# Check your local IP
hostname -I | awk '{print $1}'
```

### Security Hardening

```bash
# Generate a strong SSH key pair (on your phone/remote device)
ssh-keygen -t ed25519 -C "claude-remote-$(date +%Y%m%d)"

# Copy the public key to the server
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server-ip

# Disable password authentication (keys only)
# Edit /etc/ssh/sshd_config:
#   PasswordAuthentication no
#   PubkeyAuthentication yes
#   PermitRootLogin no

# Restart SSH
sudo systemctl restart ssh  # Linux
# macOS: toggle Remote Login off/on in System Settings
```

## Step 2: Remote Access Methods

### Option A: Tailscale (Recommended — Easiest)

Tailscale creates a secure mesh VPN with zero port forwarding.

```bash
# Install Tailscale on your server
# macOS:
brew install tailscale
# Linux:
curl -fsSL https://tailscale.com/install.sh | sh

# Start and authenticate
sudo tailscale up

# Note your Tailscale IP
tailscale ip -4

# Install Tailscale on your phone (iOS/Android app)
# Both devices join the same tailnet
# SSH from phone: ssh user@100.x.x.x
```

### Option B: Cloudflare Tunnel (No Open Ports)

```bash
# Install cloudflared
brew install cloudflared  # macOS
# or download from https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/

# Authenticate
cloudflared tunnel login

# Create a tunnel
cloudflared tunnel create claude-remote

# Configure the tunnel for SSH
cat > ~/.cloudflared/config.yml << 'EOF'
tunnel: claude-remote
credentials-file: /path/to/credentials.json
ingress:
  - hostname: claude.yourdomain.com
    service: ssh://localhost:22
  - service: http_status:404
EOF

# Route DNS
cloudflared tunnel route dns claude-remote claude.yourdomain.com

# Run the tunnel
cloudflared tunnel run claude-remote

# Connect from phone using cloudflared access
# Or use Cloudflare WARP client
```

### Option C: ngrok (Quick & Dirty)

```bash
# Install ngrok
brew install ngrok  # macOS

# Expose SSH
ngrok tcp 22

# Note the forwarding address (e.g., tcp://0.tcp.ngrok.io:12345)
# SSH from phone: ssh -p 12345 user@0.tcp.ngrok.io
```

## Step 3: Remote Task Trigger System

Create a task queue that lets you start Claude Code tasks from your phone.

### Create the task runner script

```bash
mkdir -p ~/claude-remote
cat > ~/claude-remote/task-runner.sh << 'SCRIPT'
#!/bin/bash
# Claude Code Remote Task Runner
# Watches a task queue file and executes tasks with Claude Code

QUEUE_DIR="$HOME/claude-remote/queue"
LOG_DIR="$HOME/claude-remote/logs"
STATUS_FILE="$HOME/claude-remote/status.json"

mkdir -p "$QUEUE_DIR" "$LOG_DIR"

update_status() {
    cat > "$STATUS_FILE" << EOF
{
  "status": "$1",
  "task": "$2",
  "started": "$3",
  "updated": "$(date -u +%Y-%m-%dT%H:%M:%SZ)",
  "log": "$4"
}
EOF
}

update_status "idle" "none" "" ""

echo "[$(date)] Task runner started. Watching $QUEUE_DIR..."

while true; do
    # Find the oldest .task file
    TASK_FILE=$(ls -t "$QUEUE_DIR"/*.task 2>/dev/null | tail -1)

    if [ -n "$TASK_FILE" ]; then
        TASK_NAME=$(basename "$TASK_FILE" .task)
        TASK_CONTENT=$(cat "$TASK_FILE")
        LOG_FILE="$LOG_DIR/${TASK_NAME}.log"
        START_TIME=$(date -u +%Y-%m-%dT%H:%M:%SZ)

        echo "[$(date)] Executing task: $TASK_NAME"
        update_status "running" "$TASK_NAME" "$START_TIME" "$LOG_FILE"

        # Move task to processing
        mv "$TASK_FILE" "$TASK_FILE.processing"

        # Execute with Claude Code
        claude --dangerously-skip-permissions -p "$TASK_CONTENT" > "$LOG_FILE" 2>&1
        EXIT_CODE=$?

        # Clean up
        rm "$TASK_FILE.processing"

        if [ $EXIT_CODE -eq 0 ]; then
            update_status "completed" "$TASK_NAME" "$START_TIME" "$LOG_FILE"
            echo "[$(date)] Task $TASK_NAME completed successfully"
        else
            update_status "failed" "$TASK_NAME" "$START_TIME" "$LOG_FILE"
            echo "[$(date)] Task $TASK_NAME failed with exit code $EXIT_CODE"
        fi
    fi

    sleep 5
done
SCRIPT
chmod +x ~/claude-remote/task-runner.sh
```

### Create the task submission script

```bash
cat > ~/claude-remote/submit-task.sh << 'SCRIPT'
#!/bin/bash
# Submit a task to Claude Code remotely
# Usage: ./submit-task.sh "Your prompt here"

QUEUE_DIR="$HOME/claude-remote/queue"
mkdir -p "$QUEUE_DIR"

TASK_ID="task-$(date +%Y%m%d-%H%M%S)-$$"
echo "$1" > "$QUEUE_DIR/${TASK_ID}.task"
echo "Task submitted: $TASK_ID"
echo "Monitor with: cat ~/claude-remote/status.json"
SCRIPT
chmod +x ~/claude-remote/submit-task.sh
```

### Set up as a background service (macOS launchd)

```bash
cat > ~/Library/LaunchAgents/com.claude.taskrunner.plist << 'PLIST'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.claude.taskrunner</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/bash</string>
        <string>~/claude-remote/task-runner.sh</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true/>
    <key>StandardOutPath</key>
    <string>~/claude-remote/logs/runner.stdout.log</string>
    <key>StandardErrorPath</key>
    <string>~/claude-remote/logs/runner.stderr.log</string>
</dict>
</plist>
PLIST

launchctl load ~/Library/LaunchAgents/com.claude.taskrunner.plist
```

### Set up as a background service (Linux systemd)

```bash
cat > ~/.config/systemd/user/claude-taskrunner.service << 'SERVICE'
[Unit]
Description=Claude Code Remote Task Runner

[Service]
ExecStart=/bin/bash %h/claude-remote/task-runner.sh
Restart=always
RestartSec=10

[Install]
WantedBy=default.target
SERVICE

systemctl --user enable claude-taskrunner
systemctl --user start claude-taskrunner
```

## Step 4: Phone-Friendly Status Monitoring

### Simple HTTP status page

```bash
cat > ~/claude-remote/status-server.sh << 'SCRIPT'
#!/bin/bash
# Minimal HTTP server that serves Claude Code task status
# Access from phone at http://your-ip:8377

PORT=8377
STATUS_FILE="$HOME/claude-remote/status.json"

while true; do
    RESPONSE=$(cat "$STATUS_FILE" 2>/dev/null || echo '{"status":"no tasks"}')
    CONTENT_LENGTH=${#RESPONSE}

    echo -e "HTTP/1.1 200 OK\r\nContent-Type: application/json\r\nContent-Length: $CONTENT_LENGTH\r\nAccess-Control-Allow-Origin: *\r\n\r\n$RESPONSE" | nc -l -p $PORT -q 1 2>/dev/null || \
    echo -e "HTTP/1.1 200 OK\r\nContent-Type: application/json\r\nContent-Length: $CONTENT_LENGTH\r\nAccess-Control-Allow-Origin: *\r\n\r\n$RESPONSE" | nc -l $PORT
done
SCRIPT
chmod +x ~/claude-remote/status-server.sh
```

### Recommended phone apps for SSH

- **iOS:** Termius, Blink Shell, Prompt
- **Android:** Termux, JuiceSSH, Termius

### Quick commands from phone

```bash
# Submit a task
ssh user@server "~/claude-remote/submit-task.sh 'Write a blog post about AI trends'"

# Check status
ssh user@server "cat ~/claude-remote/status.json" | python3 -m json.tool

# View latest log
ssh user@server "cat ~/claude-remote/logs/\$(ls -t ~/claude-remote/logs/*.log | head -1)"

# List all tasks
ssh user@server "ls -la ~/claude-remote/queue/"
```

## Step 5: Security Checklist

Before going live, verify:

- [ ] SSH key authentication only (no passwords)
- [ ] Firewall allows only necessary ports
- [ ] Tailscale/Cloudflare tunnel is authenticated
- [ ] Task runner does NOT have sudo access
- [ ] Claude Code runs in a sandboxed project directory
- [ ] Logs do not contain sensitive data (API keys, passwords)
- [ ] Status endpoint is not publicly accessible (behind VPN/tunnel)

## Troubleshooting

| Issue | Fix |
|-------|-----|
| SSH connection refused | Check if SSH server is running: `systemctl status ssh` |
| Permission denied (publickey) | Verify key is in `~/.ssh/authorized_keys` on server |
| Task runner not picking up tasks | Check if the service is running: `launchctl list \| grep claude` |
| Can't connect from phone | Verify both devices are on the same Tailscale network |
| Claude Code errors in tasks | Check logs: `cat ~/claude-remote/logs/[task-name].log` |
