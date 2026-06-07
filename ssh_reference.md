# SSH Reference Guide

A complete reference for `ssh` — the Secure Shell protocol for remote login, tunneling, and file transfer.

---

## Table of Contents

1. [Basics](#1-basics)
2. [Key Management](#2-key-management)
3. [SSH Config File](#3-ssh-config-file)
4. [File Transfer — scp](#4-file-transfer--scp)
5. [File Transfer — sftp](#5-file-transfer--sftp)
6. [Port Forwarding & Tunneling](#6-port-forwarding--tunneling)
7. [Jump Hosts & Bastion](#7-jump-hosts--bastion)
8. [Agent Forwarding](#8-agent-forwarding)
9. [Multiplexing](#9-multiplexing)
10. [Remote Commands](#10-remote-commands)
11. [Server Configuration (sshd)](#11-server-configuration-sshd)
12. [Security Hardening](#12-security-hardening)
13. [Debugging & Troubleshooting](#13-debugging--troubleshooting)
14. [Common Recipes](#14-common-recipes)

---

## 1. Basics

```bash
ssh user@host                                   # Connect to host as user
ssh host                                        # Connect using current local username
ssh user@host -p 2222                           # Connect on non-default port
ssh user@192.168.1.10                           # Connect by IP

# With identity file (private key)
ssh -i ~/.ssh/my_key user@host

# Run a command and exit
ssh user@host "ls -la /var/log"

# Allocate a pseudo-TTY (needed for interactive remote commands)
ssh -t user@host "sudo vim /etc/hosts"

# Disable strict host key checking (dev/scripts only)
ssh -o StrictHostKeyChecking=no user@host
```

---

## 2. Key Management

### Generate Keys

```bash
# ED25519 (recommended — fast, secure, small)
ssh-keygen -t ed25519 -C "your@email.com"

# RSA 4096-bit (broader compatibility)
ssh-keygen -t rsa -b 4096 -C "your@email.com"

# Specify output file
ssh-keygen -t ed25519 -f ~/.ssh/my_server_key -C "server key"

# Generate with no passphrase (automation only)
ssh-keygen -t ed25519 -N "" -f ~/.ssh/deploy_key
```

### Copy Key to Server

```bash
# Recommended — appends to authorized_keys automatically
ssh-copy-id user@host
ssh-copy-id -i ~/.ssh/my_key.pub user@host
ssh-copy-id -i ~/.ssh/my_key.pub -p 2222 user@host

# Manual alternative
cat ~/.ssh/id_ed25519.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### Key Files

| File                     | Description                           |
| ------------------------ | ------------------------------------- |
| `~/.ssh/id_ed25519`      | Private key (never share)             |
| `~/.ssh/id_ed25519.pub`  | Public key (copy to servers)          |
| `~/.ssh/authorized_keys` | Keys allowed to log into this machine |
| `~/.ssh/known_hosts`     | Fingerprints of known servers         |
| `~/.ssh/config`          | SSH client configuration              |

### Manage known_hosts

```bash
# View fingerprint of a server before connecting
ssh-keyscan -t ed25519 host

# Remove a stale host entry (after server rebuild)
ssh-keygen -R hostname
ssh-keygen -R 192.168.1.10

# Add a host manually
ssh-keyscan host >> ~/.ssh/known_hosts
```

### ssh-agent (Avoid Retyping Passphrases)

```bash
eval "$(ssh-agent -s)"                          # Start agent
ssh-add ~/.ssh/id_ed25519                       # Add key to agent
ssh-add -l                                      # List loaded keys
ssh-add -d ~/.ssh/id_ed25519                    # Remove key from agent
ssh-add -D                                      # Remove all keys
ssh-add -t 3600 ~/.ssh/id_ed25519               # Add key, expire in 1 hour
```

---

## 3. SSH Config File

`~/.ssh/config` eliminates repetitive flags — define host aliases with all their options.

```
# ~/.ssh/config

# Default settings for all hosts
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_ed25519

# Simple alias
Host myserver
    HostName 203.0.113.10
    User alice
    Port 2222
    IdentityFile ~/.ssh/myserver_key

# Bastion / jump host
Host prod-app
    HostName 10.0.1.50
    User deploy
    ProxyJump bastion

Host bastion
    HostName bastion.example.com
    User alice

# Multiple aliases for the same host pattern
Host dev-*
    User developer
    IdentityFile ~/.ssh/dev_key
    ForwardAgent yes
```

```bash
# After config is set up
ssh myserver                                    # Uses all settings above
ssh prod-app                                    # Automatically jumps through bastion
```

### Useful Config Options

| Option                  | Description                             |
| ----------------------- | --------------------------------------- |
| `HostName`              | Real hostname or IP                     |
| `User`                  | Remote username                         |
| `Port`                  | SSH port                                |
| `IdentityFile`          | Path to private key                     |
| `ProxyJump`             | Jump through another host               |
| `ForwardAgent`          | Forward local SSH agent to remote       |
| `ServerAliveInterval`   | Keepalive ping interval (seconds)       |
| `ServerAliveCountMax`   | Max missed keepalives before disconnect |
| `StrictHostKeyChecking` | `yes` / `no` / `accept-new`             |
| `AddKeysToAgent`        | Auto-add key to ssh-agent on use        |
| `ControlMaster`         | Enable connection multiplexing          |
| `ControlPath`           | Socket path for multiplexed connections |
| `LocalForward`          | Local port forwarding                   |
| `RemoteForward`         | Remote port forwarding                  |
| `DynamicForward`        | SOCKS5 proxy port                       |

---

## 4. File Transfer — scp

`scp` copies files over SSH. Syntax mirrors `cp` but with `user@host:path` for remote paths.

```bash
# Local → Remote
scp file.txt user@host:/remote/path/
scp file.txt user@host:~                        # To home directory
scp -P 2222 file.txt user@host:/tmp/            # Non-default port (capital P)

# Remote → Local
scp user@host:/remote/file.txt ./local/
scp user@host:/var/log/app.log .

# Directory (recursive)
scp -r ./local-dir user@host:/remote/path/
scp -r user@host:/remote/dir ./local-copy/

# Remote → Remote
scp user1@host1:/file user2@host2:/dest/

# With identity file
scp -i ~/.ssh/my_key file.txt user@host:/path/

# Preserve timestamps and permissions
scp -p file.txt user@host:/path/

# Limit bandwidth (Kbps)
scp -l 1000 largefile.zip user@host:/path/
```

> For large or frequent transfers, prefer `rsync` over `scp` — it supports resume, compression, and delta transfers.

---

## 5. File Transfer — sftp

`sftp` is an interactive FTP-like session over SSH.

```bash
sftp user@host                                  # Open session
sftp -P 2222 user@host                          # Non-default port
sftp -i ~/.ssh/my_key user@host                 # With key
```

### sftp Interactive Commands

```
sftp> ls                    List remote directory
sftp> lls                   List local directory
sftp> pwd                   Remote working directory
sftp> lpwd                  Local working directory
sftp> cd /remote/path       Change remote directory
sftp> lcd /local/path       Change local directory
sftp> get file.txt          Download file to local
sftp> get file.txt local.txt  Download and rename
sftp> mget *.log            Download multiple files
sftp> put file.txt          Upload file to remote
sftp> put file.txt /remote/ Upload to specific path
sftp> mput *.csv            Upload multiple files
sftp> mkdir newdir          Create remote directory
sftp> rm file.txt           Delete remote file
sftp> rename old new        Rename remote file
sftp> chmod 644 file.txt    Change remote permissions
sftp> df -h                 Remote disk usage
sftp> bye / exit            Close session
```

### Non-interactive sftp

```bash
# Run a single command
sftp user@host <<< "get /remote/file.txt"

# Batch commands from file
sftp -b commands.txt user@host
# commands.txt:
#   cd /remote/path
#   mget *.log
#   bye
```

---

## 6. Port Forwarding & Tunneling

### Local Port Forwarding

Forwards a local port to a port on the remote server (or a host the remote can reach).

```bash
ssh -L local_port:target_host:target_port user@ssh_host

# Examples
ssh -L 8080:localhost:80 user@host       # Access remote port 80 at localhost:8080
ssh -L 5432:localhost:5432 user@host     # Tunnel remote Postgres to local 5432
ssh -L 8080:internal.server:80 user@bastion  # Reach internal host through bastion
```

### Remote Port Forwarding

Exposes a local port on the remote server — lets remote access your local machine.

```bash
ssh -R remote_port:local_host:local_port user@ssh_host

# Examples
ssh -R 8080:localhost:3000 user@host     # Remote port 8080 → your local :3000
ssh -R 2222:localhost:22 user@host       # Allow remote to SSH back to you
```

### Dynamic Forwarding (SOCKS5 Proxy)

Turns SSH into a full SOCKS5 proxy — route any traffic through the remote server.

```bash
ssh -D 1080 user@host                    # Start SOCKS5 proxy on local port 1080

# Then configure browser / app to use SOCKS5 proxy at 127.0.0.1:1080
curl --socks5 127.0.0.1:1080 https://example.com
```

### Keep Tunnel Running (No Shell)

```bash
ssh -N -L 5432:localhost:5432 user@host  # -N = no remote command, just tunnel
ssh -f -N -L 5432:localhost:5432 user@host  # -f = go to background
```

---

## 7. Jump Hosts & Bastion

A bastion (jump host) is a publicly accessible server used to reach private hosts.

```bash
# Single jump
ssh -J bastion_user@bastion user@private_host

# Multiple jumps
ssh -J user@hop1,user@hop2 user@final_host

# Via SSH config (cleaner)
# ~/.ssh/config:
#   Host private
#       HostName 10.0.0.5
#       User alice
#       ProxyJump bastion
#
#   Host bastion
#       HostName bastion.example.com
#       User alice

ssh private                                     # Automatically routes through bastion

# Old style (still works)
ssh -o ProxyCommand="ssh -W %h:%p user@bastion" user@private
```

---

## 8. Agent Forwarding

Lets you use your local SSH keys on remote servers without copying the private key there — safe for hopping through bastions.

```bash
ssh -A user@host                                # Forward local agent
ssh -A user@bastion                             # Then from bastion: ssh user@private (uses local keys)
```

In `~/.ssh/config`:

```
Host bastion
    ForwardAgent yes
```

> Only forward your agent to trusted hosts — a compromised server with agent forwarding can use your keys.

---

## 9. Multiplexing

Reuse an existing SSH connection — dramatically speeds up repeated connections to the same host.

```bash
# Start a master connection in background
ssh -M -S ~/.ssh/ctrl-%r@%h:%p -fN user@host

# Subsequent connections reuse it instantly
ssh -S ~/.ssh/ctrl-%r@%h:%p user@host

# Check master status
ssh -S ~/.ssh/ctrl-%r@%h:%p -O check user@host

# Close master
ssh -S ~/.ssh/ctrl-%r@%h:%p -O exit user@host
```

In `~/.ssh/config` (recommended approach):

```
Host myserver
    ControlMaster auto
    ControlPath ~/.ssh/sockets/%r@%h:%p
    ControlPersist 10m                          # Keep master open 10 min after last session
```

```bash
mkdir -p ~/.ssh/sockets
ssh myserver                                    # First connection — creates master
ssh myserver                                    # Instant — reuses socket
```

---

## 10. Remote Commands

```bash
# Run single command
ssh user@host "df -h"
ssh user@host "cat /etc/os-release"

# Multiple commands
ssh user@host "cd /app && git pull && systemctl restart app"

# Pipe local data to remote command
echo "hello" | ssh user@host "cat > /tmp/hello.txt"
tar czf - ./local-dir | ssh user@host "cat > /tmp/backup.tar.gz"

# Pipe remote output to local command
ssh user@host "cat /var/log/app.log" | grep ERROR

# Run local script on remote machine (without copying it first)
ssh user@host bash < local_script.sh

# Sudo on remote (requires TTY)
ssh -t user@host "sudo systemctl restart nginx"

# Keep session open after command (useful for port forwards)
ssh -t user@host "tmux attach || tmux new"
```

---

## 11. Server Configuration (sshd)

Server config lives at `/etc/ssh/sshd_config`.

```bash
sudo sshd -T                                    # Print effective config
sudo sshd -t                                    # Test config for syntax errors
sudo systemctl restart sshd                     # Apply changes
```

### Key sshd_config Options

```ini
Port 22                                         # Listening port
ListenAddress 0.0.0.0                           # Bind address

# Authentication
PermitRootLogin no                              # Disable root login
PasswordAuthentication no                       # Keys only (after key setup)
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

# Session limits
MaxAuthTries 3
MaxSessions 10
LoginGraceTime 30                               # Seconds to authenticate

# Keepalive
ClientAliveInterval 60
ClientAliveCountMax 3

# Restrict access
AllowUsers alice bob                            # Whitelist users
AllowGroups sshusers                            # Whitelist groups
DenyUsers root                                  # Blacklist users

# X11 / forwarding
X11Forwarding no
AllowAgentForwarding yes
AllowTcpForwarding yes

# Subsystems
Subsystem sftp /usr/lib/openssh/sftp-server
```

---

## 12. Security Hardening

```bash
# Use ed25519 keys only
ssh-keygen -t ed25519

# Disable password auth (after key setup)
# /etc/ssh/sshd_config:
#   PasswordAuthentication no
#   ChallengeResponseAuthentication no

# Change default port (minor obscurity, reduces automated scans)
# Port 2222

# Restrict to specific users
# AllowUsers alice deploy

# Fail2ban — auto-ban IPs with repeated failures
sudo apt install fail2ban
sudo systemctl enable --now fail2ban

# Verify authorized_keys permissions (must be 600 or 644)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# Rotate keys — generate new key, copy to all servers, remove old
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_new
ssh-copy-id -i ~/.ssh/id_ed25519_new.pub user@host
# Then remove old public key from ~/.ssh/authorized_keys on the server

# Audit who has access
cat ~/.ssh/authorized_keys                      # On the server
```

---

## 13. Debugging & Troubleshooting

```bash
# Verbose output (add more v's for more detail: -vv, -vvv)
ssh -v user@host
ssh -vvv user@host                              # Maximum debug output

# Test config for a specific host
ssh -G myserver                                 # Print resolved config options

# Check SSH service on server
sudo systemctl status sshd
sudo journalctl -u sshd -f                      # Live sshd logs

# Verify server is listening
ss -tlnp | grep 22
netstat -tlnp | grep :22

# Test connection without logging in
nc -zv host 22                                  # Check port is open
ssh-keyscan host                                # Fetch host public key

# Permission issues (most common cause of key auth failure)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519

# On the server — check auth logs
sudo tail -f /var/log/auth.log                  # Debian/Ubuntu
sudo tail -f /var/log/secure                    # RHEL/CentOS
sudo journalctl -fu sshd                        # systemd

# Force password auth to bypass key issues temporarily
ssh -o PreferredAuthentications=password user@host
```

### Common Errors

| Error                                             | Likely Cause                                                 |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `Permission denied (publickey)`                   | Wrong key, wrong user, bad file permissions                  |
| `Host key verification failed`                    | Server fingerprint changed — run `ssh-keygen -R host`        |
| `Connection refused`                              | sshd not running or port blocked by firewall                 |
| `Connection timed out`                            | Wrong IP, firewall blocking, server unreachable              |
| `Too many authentication failures`                | Agent has too many keys — use `-o IdentitiesOnly=yes -i key` |
| `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED` | Server rebuilt — remove from known_hosts                     |

---

## 14. Common Recipes

### Persistent Background Tunnel

```bash
# Forward remote Postgres to local port 5432 in background
ssh -f -N -L 5432:localhost:5432 user@db-host

# Kill it later
kill $(pgrep -f "ssh.*5432")
```

### Sync Files with rsync over SSH

```bash
rsync -avz --progress ./local-dir/ user@host:/remote/dir/
rsync -avz --progress user@host:/remote/dir/ ./local-backup/
rsync -avz -e "ssh -p 2222 -i ~/.ssh/my_key" ./dir/ user@host:/path/
```

### Copy SSH Key to Server (One-liner if ssh-copy-id unavailable)

```bash
cat ~/.ssh/id_ed25519.pub | ssh user@host "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

### Access a Remote Jupyter Notebook

```bash
# On remote: jupyter notebook --no-browser --port=8888
# On local:
ssh -N -L 8888:localhost:8888 user@host
# Open http://localhost:8888 in browser
```

### Auto-Reconnect Session with tmux

```bash
ssh user@host -t "tmux new -As main"
# Reconnect later — same command reattaches existing session
```

### Execute a Local Script on Remote

```bash
ssh user@host bash < deploy.sh
```

### Check Uptime on Multiple Servers

```bash
for host in server1 server2 server3; do
  echo -n "$host: "
  ssh -o ConnectTimeout=3 user@$host "uptime -p" 2>/dev/null || echo "unreachable"
done
```

### Two-Factor Auth Setup (TOTP)

```bash
# On server
sudo apt install libpam-google-authenticator
google-authenticator

# /etc/ssh/sshd_config:
#   AuthenticationMethods publickey,keyboard-interactive

# /etc/pam.d/sshd:
#   auth required pam_google_authenticator.so
```

---

## Quick Reference Card

```
ssh [options] user@host [command]

Connection
  -p PORT              Port (default 22)
  -i FILE              Identity (private key) file
  -F FILE              Use specific config file
  -o OPTION=VALUE      Set config option inline

Forwarding
  -L local:host:remote Local port forward
  -R remote:host:local Remote port forward
  -D PORT              Dynamic SOCKS5 proxy
  -J user@host         Jump through host (bastion)
  -A                   Forward SSH agent

Session
  -t                   Force TTY allocation
  -T                   Disable TTY allocation
  -N                   No remote command (tunnel only)
  -f                   Go to background before command
  -M                   Master mode (multiplexing)
  -S socket            Multiplexing socket path

Debug
  -v / -vv / -vvv      Verbosity levels
  -G                   Print config for host and exit

scp [options] source dest
  -P PORT              Port
  -i FILE              Identity file
  -r                   Recursive
  -p                   Preserve timestamps
  -l KBPS              Bandwidth limit

sftp [options] user@host
  -P PORT              Port
  -i FILE              Identity file
  -b FILE              Batch mode (read commands from file)

ssh-keygen
  -t ed25519           Key type (prefer ed25519)
  -b 4096              Bits (for RSA)
  -C "comment"         Key comment
  -f FILE              Output file
  -N "passphrase"      Passphrase (empty string = none)
  -R host              Remove host from known_hosts
  -l -f FILE           Show key fingerprint

ssh-copy-id
  -i FILE.pub          Public key to copy
  -p PORT              Remote port
```
