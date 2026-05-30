# Terminal Commands Reference

A structured, searchable collection of 850+ terminal and shell command references across three guides — Bash/Zsh, Linux (full), and PowerShell. Each file is self-contained with a table of contents, syntax, flags, and examples.

---

## Files at a Glance

| File | Shell / OS | Commands | Categories |
|------|-----------|----------|------------|
| [terminal_commands_reference.md](terminal_commands_reference.md) | Bash / Zsh — macOS & Linux | 142 | 11 |
| [linux_terminal_commands_reference_full.md](linux_terminal_commands_reference_full.md) | Linux — full deep reference | 394 | 24 |
| [powershell_commands_reference.md](powershell_commands_reference.md) | PowerShell — Windows | 314 | 21 |

---

## How to Use

**Jump to a section** — every file has a full table of contents with category counts. Click any heading to go there directly.

**Quick search in terminal:**
```bash
# Find all entries for a command across all files
grep -n "curl" terminal_commands_reference.md

# Search case-insensitively across all files
grep -ri "firewall" .

# Find every command that mentions a port
grep -n "port" linux_terminal_commands_reference_full.md
```

**Search in your editor** — open any file and use `Cmd+F` (macOS) or `Ctrl+F` (Windows/Linux). Every command name is in a `### \`name\`` heading so searching for a command name finds it instantly.

---

## Bash / Zsh — 11 Categories, 142 Commands

> File: `terminal_commands_reference.md`

| Category | Commands | What's Covered |
|----------|----------|----------------|
| Navigation | 6 | `ls`, `cd`, `pwd`, `find`, `locate`, `tree` |
| Files | 12 | `cp`, `mv`, `rm`, `mkdir`, `touch`, `ln`, `chmod`, `chown`, `stat`, `file`, `du`, `rename` |
| Text | 15 | `cat`, `less`, `head`, `tail`, `grep`, `sed`, `awk`, `sort`, `uniq`, `wc`, `cut`, `tr`, `diff`, `tee`, `xargs` |
| Archives | 5 | `tar`, `gzip`, `zip`, `unzip`, `7z` |
| Processes | 13 | `ps`, `top`, `htop`, `kill`, `killall`, `pkill`, `pgrep`, `bg`, `fg`, `jobs`, `nohup`, `nice`, `renice` |
| Network | 15 | `ping`, `curl`, `wget`, `ssh`, `scp`, `rsync`, `netstat`, `ss`, `ip`, `nmap`, `dig`, `traceroute`, `nslookup`, `iptables`, `ufw` |
| Disk | 10 | `df`, `lsblk`, `mount`, `umount`, `fdisk`, `mkfs`, `fsck`, `dd`, `blkid`, `parted` |
| Users | 13 | `whoami`, `id`, `w`, `who`, `last`, `sudo`, `su`, `useradd`, `usermod`, `userdel`, `passwd`, `groupadd`, `groups` |
| System | 22 | `uname`, `uptime`, `hostname`, `date`, `cal`, `timedatectl`, `systemctl`, `journalctl`, `dmesg`, `lshw`, `lscpu`, `free`, `vmstat`, `env`, `export`, `alias`, `history`, `cron`, `at`, `reboot`, `shutdown`, `poweroff` |
| Package Mgmt | 10 | `apt`, `apt-get`, `dpkg`, `yum`, `dnf`, `pacman`, `snap`, `flatpak`, `npm`, `pip` |
| Shell | 21 | `echo`, `printf`, `read`, `source`, `exec`, `test`, `true`, `false`, `exit`, `set`, `type`, `which`, `whereis`, `man`, `help`, `info`, `time`, `watch`, `screen`, `tmux`, `strace` |

### Most-Used Commands (Bash/Zsh)

```bash
# List files with sizes, sorted by modification time
ls -lht

# Find all .log files modified in the last 7 days
find /var/log -name "*.log" -mtime -7

# Search recursively for a string, show line numbers
grep -rn "error" ./logs/

# Replace text in-place across a file
sed -i 's/old_value/new_value/g' config.txt

# Extract a .tar.gz archive
tar -xzvf archive.tar.gz

# Show all running processes with memory/cpu usage
ps aux --sort=-%mem | head -20

# Download a file silently
curl -sL https://example.com/file.zip -o file.zip

# Copy files over SSH
scp -r ./folder user@192.168.1.10:/remote/path/

# Show disk usage of current directory, human-readable
du -sh *

# Watch a command run every 2 seconds
watch -n 2 df -h

# Run a process in background, immune to hangup
nohup python3 server.py &

# Check open ports
ss -tlnp
```

---

## Linux Full Reference — 24 Categories, 394 Commands

> File: `linux_terminal_commands_reference_full.md`

This is the deep-dive Linux reference — covers everything from basic navigation to kernel modules, containers, and Git.

| Category | Commands | What's Covered |
|----------|----------|----------------|
| Navigation | 10 | `ls`, `cd`, `pwd`, `find`, `locate`, `tree`, `pushd`, `popd`, `dirs`, `realpath` |
| Files | 16 | `cp`, `mv`, `rm`, `mkdir`, `touch`, `ln`, `chmod`, `chown`, `stat`, `file`, `du`, `rename`, `install`, `truncate`, `shred`, `split` |
| Text | 32 | `cat`, `less`, `more`, `head`, `tail`, `grep`, `egrep`, `fgrep`, `sed`, `awk`, `sort`, `uniq`, `wc`, `cut`, `tr`, `diff`, `patch`, `tee`, `xargs`, `strings`, `od`, `xxd`, `nl`, `fold`, `fmt`, `column`, `paste`, `join`, `comm`, `expand`, `unexpand`, `rev` |
| Search | 8 | `find`, `locate`, `updatedb`, `which`, `whereis`, `type`, `mlocate`, `fd` |
| Archives | 11 | `tar`, `gzip`, `bzip2`, `xz`, `zip`, `unzip`, `7z`, `rar`, `ar`, `cpio`, `zcat` |
| Processes | 22 | `ps`, `top`, `htop`, `kill`, `killall`, `pkill`, `pgrep`, `bg`, `fg`, `jobs`, `nohup`, `nice`, `renice`, `pstree`, `lsof`, `fuser`, `pidof`, `wait`, `trap`, `ulimit`, `ionice`, `taskset` |
| Network | 26 | `ping`, `curl`, `wget`, `ssh`, `scp`, `rsync`, `netstat`, `ss`, `ip`, `ifconfig`, `nmap`, `dig`, `nslookup`, `host`, `traceroute`, `mtr`, `iptables`, `ufw`, `nc`, `tcpdump`, `arp`, `route`, `nmcli`, `hostnamectl`, `ethtool`, `iwconfig` |
| Disk | 24 | `df`, `du`, `lsblk`, `mount`, `umount`, `fdisk`, `mkfs`, `fsck`, `dd`, `blkid`, `parted`, `gdisk`, `e2fsck`, `tune2fs`, `badblocks`, `hdparm`, `smartctl`, `fstrim`, `swapoff`, `swapon`, `mkswap`, `losetup`, `cryptsetup`, `lvdisplay` |
| Users & Groups | 23 | `whoami`, `id`, `w`, `who`, `last`, `lastlog`, `sudo`, `su`, `useradd`, `usermod`, `userdel`, `passwd`, `groupadd`, `groupmod`, `groupdel`, `groups`, `newgrp`, `gpasswd`, `chage`, `finger`, `getent`, `visudo`, `chsh` |
| Permissions | 10 | `chmod`, `chown`, `chgrp`, `umask`, `setfacl`, `getfacl`, `lsattr`, `chattr`, `namei`, `stat` |
| System Info | 18 | `uname`, `uptime`, `hostname`, `date`, `cal`, `timedatectl`, `hostnamectl`, `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`, `inxi`, `free`, `vmstat`, `iostat`, `sar`, `nproc` |
| Services | 9 | `systemctl`, `service`, `journalctl`, `systemd-analyze`, `loginctl`, `machinectl`, `resolvectl`, `hostnamectl`, `timedatectl` |
| Kernel & Modules | 10 | `uname`, `dmesg`, `lsmod`, `modinfo`, `modprobe`, `rmmod`, `insmod`, `depmod`, `sysctl`, `kexec` |
| Memory | 7 | `free`, `vmstat`, `smem`, `pmap`, `memtester`, `slabtop`, `numactl` |
| Monitoring | 13 | `top`, `htop`, `atop`, `glances`, `iotop`, `iftop`, `nethogs`, `nload`, `dstat`, `collectl`, `perf`, `strace`, `ltrace` |
| Package Mgmt | 15 | `apt`, `apt-get`, `dpkg`, `yum`, `dnf`, `pacman`, `zypper`, `rpm`, `snap`, `flatpak`, `brew`, `npm`, `pip`, `cargo`, `gem` |
| SSH & Remote | 11 | `ssh`, `scp`, `rsync`, `sftp`, `ssh-keygen`, `ssh-copy-id`, `ssh-add`, `ssh-agent`, `sshfs`, `autossh`, `mosh` |
| Firewall | 6 | `iptables`, `ip6tables`, `ufw`, `firewalld`, `nftables`, `fail2ban` |
| Containers | 6 | `docker`, `podman`, `buildah`, `skopeo`, `kubectl`, `helm` |
| Git | 28 | `init`, `clone`, `add`, `commit`, `push`, `pull`, `fetch`, `merge`, `rebase`, `branch`, `checkout`, `switch`, `status`, `log`, `diff`, `stash`, `tag`, `remote`, `reset`, `revert`, `cherry-pick`, `bisect`, `blame`, `show`, `reflog`, `submodule`, `worktree`, `config` |
| Shell & Scripting | 36 | `echo`, `printf`, `read`, `source`, `exec`, `test`, `if`, `for`, `while`, `case`, `function`, `return`, `exit`, `set`, `shift`, `getopts`, `trap`, `eval`, `expr`, `let`, `declare`, `local`, `readonly`, `unset`, `array ops`, `heredoc`, `process substitution`, and more |
| Environment | 8 | `env`, `export`, `printenv`, `unset`, `set`, `declare`, `direnv`, `envsubst` |
| Cron & Jobs | 8 | `crontab`, `at`, `atq`, `atrm`, `batch`, `anacron`, `systemd timers`, `fcron` |
| Misc | 37 | `alias`, `history`, `man`, `info`, `tldr`, `help`, `time`, `watch`, `sleep`, `wait`, `bc`, `expr`, `factor`, `yes`, `seq`, `tput`, `clear`, `reset`, `banner`, `figlet`, `cowsay`, `lolcat`, `fortune`, `cal`, `units`, `od`, `base64`, `xxd`, `uuidgen`, `md5sum`, `sha256sum`, `openssl`, `gpg`, `shuf`, `tac`, `nl`, `pr` |

### Most-Used Commands (Linux)

```bash
# Show all listening ports with process names (requires root)
ss -tlnp

# Monitor disk I/O in real time
iotop -o

# Check which process owns a port
lsof -i :8080

# Watch network traffic per process
nethogs eth0

# Generate SSH keypair
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy SSH key to remote server
ssh-copy-id user@remote_host

# View systemd service logs, follow in real time
journalctl -u nginx -f

# Show failed systemd services
systemctl --failed

# Trace system calls of a running process
strace -p <PID> -e trace=network

# Find files larger than 100MB
find / -type f -size +100M 2>/dev/null

# Check file ACL permissions
getfacl /path/to/file

# List all open files by a process
lsof -p <PID>

# Watch CPU/memory usage per core
mpstat -P ALL 1

# Create encrypted archive
tar -czf - folder/ | openssl enc -aes-256-cbc -out folder.tar.gz.enc
```

---

## PowerShell — 21 Categories, 314 Commands

> File: `powershell_commands_reference.md`

Full cmdlet and alias reference for PowerShell on Windows (and cross-platform PS Core). Every cmdlet lists its short aliases (e.g. `ls`, `cd`, `cat`).

| Category | Commands | What's Covered |
|----------|----------|----------------|
| Navigation | 6 | `Set-Location`, `Get-Location`, `Push-Location`, `Pop-Location`, `Get-ChildItem`, `Get-Item` |
| File System | 21 | `Copy-Item`, `Move-Item`, `Remove-Item`, `New-Item`, `Rename-Item`, `Get-Content`, `Set-Content`, `Add-Content`, `Clear-Content`, `Test-Path`, `Resolve-Path`, `Split-Path`, `Join-Path`, `Get-ItemProperty`, `Set-ItemProperty`, and more |
| Text & String | 29 | `Select-String`, `Out-String`, `-split`, `-join`, `-replace`, `[regex]`, `Format-*`, `Measure-Object`, and more |
| Objects & Pipeline | 20 | `Where-Object`, `ForEach-Object`, `Select-Object`, `Sort-Object`, `Group-Object`, `Compare-Object`, `Tee-Object`, `Out-*` cmdlets |
| Variables & Data | 21 | `Set-Variable`, `Get-Variable`, `Remove-Variable`, `New-Variable`, hashtables, arrays, `[PSCustomObject]`, `ConvertTo-Json`, `ConvertFrom-Json` |
| Processes | 13 | `Get-Process`, `Start-Process`, `Stop-Process`, `Wait-Process`, `Debug-Process` |
| Services | 9 | `Get-Service`, `Start-Service`, `Stop-Service`, `Restart-Service`, `Set-Service`, `New-Service`, `Remove-Service` |
| Network | 16 | `Test-Connection`, `Invoke-WebRequest`, `Invoke-RestMethod`, `Get-NetAdapter`, `Get-NetIPAddress`, `Test-NetConnection`, `Resolve-DnsName` |
| System Info | 18 | `Get-ComputerInfo`, `Get-Host`, `Get-Date`, `Get-Uptime`, `Get-HotFix`, `Get-Disk`, `Get-Volume`, `Get-PSDrive` |
| Registry | 10 | `Get-ItemProperty`, `Set-ItemProperty`, `New-Item` (Registry), `Remove-ItemProperty`, `Get-ChildItem` (HKLM:/HKCU:) |
| Security | 12 | `Get-Acl`, `Set-Acl`, `Get-Credential`, `ConvertTo-SecureString`, `Get-AuthenticodeSignature`, `Set-ExecutionPolicy` |
| Users & Groups | 13 | `Get-LocalUser`, `New-LocalUser`, `Remove-LocalUser`, `Set-LocalUser`, `Get-LocalGroup`, `Add-LocalGroupMember` |
| Modules & Packages | 16 | `Get-Module`, `Import-Module`, `Install-Module`, `Find-Module`, `Update-Module`, `Get-Command`, `Find-Package`, `Install-Package` |
| Remoting | 11 | `Enter-PSSession`, `New-PSSession`, `Invoke-Command`, `Exit-PSSession`, `Enable-PSRemoting` |
| CIM & WMI | 12 | `Get-CimInstance`, `Invoke-CimMethod`, `Get-WmiObject`, `Invoke-WmiMethod` |
| Scheduling | 10 | `Get-ScheduledTask`, `Register-ScheduledTask`, `Start-ScheduledTask`, `Unregister-ScheduledTask`, `New-ScheduledTaskTrigger` |
| Error Handling | 10 | `Try/Catch/Finally`, `$Error`, `$?`, `$LASTEXITCODE`, `Write-Error`, `Throw`, `-ErrorAction` |
| Scripting & Flow | 16 | `If/ElseIf/Else`, `Switch`, `For`, `ForEach`, `While`, `Do-While`, `Break`, `Continue`, `Return`, `Function`, `Param` |
| Environment | 11 | `$env:`, `[System.Environment]`, `Get-Content Env:`, `Set-Item Env:`, `$HOME`, `$PATH`, `$PSVersionTable` |
| Formatting & Output | 12 | `Format-Table`, `Format-List`, `Format-Wide`, `Format-Custom`, `Out-File`, `Out-GridView`, `Out-Printer`, `Export-Csv`, `Import-Csv` |
| Misc | 28 | `Write-Host`, `Write-Output`, `Read-Host`, `Clear-Host`, `Get-Alias`, `New-Alias`, `Measure-Command`, `Start-Sleep`, `Get-Random`, `ConvertTo-Html`, `Send-MailMessage`, and more |

### Most-Used Commands (PowerShell)

```powershell
# List files including hidden, sorted by last write time
Get-ChildItem -Force | Sort-Object LastWriteTime -Descending

# Search file contents recursively (like grep)
Select-String -Path ".\*.log" -Pattern "error" -CaseSensitive:$false

# Download a file from the web
Invoke-WebRequest -Uri "https://example.com/file.zip" -OutFile "file.zip"

# Call a REST API and parse JSON
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method GET
$response.items

# Filter running processes by memory usage
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 10 Name, CPU, WorkingSet

# Stop a process by name
Stop-Process -Name "notepad" -Force

# Get all services that are stopped
Get-Service | Where-Object { $_.Status -eq "Stopped" }

# Run a command on a remote computer
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-EventLog -LogName System -Newest 10 }

# Check if a port is open
Test-NetConnection -ComputerName google.com -Port 443

# Get disk space for all drives
Get-PSDrive -PSProvider FileSystem | Select-Object Name, Used, Free

# Export process list to CSV
Get-Process | Export-Csv -Path "processes.csv" -NoTypeInformation

# Read and modify registry value
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion" -Name "ProgramFilesDir"

# Create a scheduled task
$trigger = New-ScheduledTaskTrigger -Daily -At "08:00AM"
Register-ScheduledTask -TaskName "DailyBackup" -Trigger $trigger -Action (New-ScheduledTaskAction -Execute "backup.ps1")

# Measure script execution time
Measure-Command { Get-ChildItem -Recurse C:\ }
```

---

## How-To Guides

### How to find a file by name

**Bash/Linux:**
```bash
find /path -name "filename.txt"          # exact name
find /path -name "*.log" -type f         # by extension
locate filename.txt                       # fast, uses DB
```

**PowerShell:**
```powershell
Get-ChildItem -Recurse -Filter "*.txt"
Get-ChildItem -Recurse | Where-Object { $_.Name -like "*config*" }
```

---

### How to search inside files

**Bash/Linux:**
```bash
grep -rn "search term" /path/            # recursive, with line numbers
grep -ri "error" /var/log/               # case-insensitive
grep -rl "pattern" .                     # only print filenames
awk '/pattern/ { print NR": "$0 }' file  # with context
```

**PowerShell:**
```powershell
Select-String -Path ".\**\*.log" -Pattern "error" -Recurse
```

---

### How to manage processes

**Bash/Linux:**
```bash
ps aux | grep process_name               # find a process
kill -15 <PID>                           # graceful stop
kill -9 <PID>                            # force kill
killall nginx                            # kill by name
nohup ./script.sh &                      # run detached
```

**PowerShell:**
```powershell
Get-Process | Where-Object { $_.Name -like "*node*" }
Stop-Process -Id <PID> -Force
Start-Process notepad.exe
```

---

### How to work with archives

**Bash/Linux:**
```bash
tar -czf archive.tar.gz folder/          # create .tar.gz
tar -xzf archive.tar.gz -C /dest/       # extract to dir
tar -tzf archive.tar.gz                  # list contents
zip -r archive.zip folder/               # create .zip
unzip archive.zip -d /dest/             # extract .zip
```

**PowerShell:**
```powershell
Compress-Archive -Path ".\folder" -DestinationPath "archive.zip"
Expand-Archive -Path "archive.zip" -DestinationPath ".\output"
```

---

### How to use SSH

**Connect to a server:**
```bash
ssh user@192.168.1.10                    # basic connection
ssh -p 2222 user@host                    # custom port
ssh -i ~/.ssh/id_rsa user@host           # with key file
```

**Set up key-based auth (no password):**
```bash
ssh-keygen -t ed25519                    # generate key
ssh-copy-id user@host                    # copy key to server
```

**Port forwarding:**
```bash
ssh -L 8080:localhost:80 user@host       # local forward
ssh -R 9090:localhost:3000 user@host     # remote forward
ssh -N -D 1080 user@host                 # SOCKS proxy
```

---

### How to monitor system resources

**Bash/Linux:**
```bash
top                    # live CPU/memory (press M to sort by memory)
htop                   # interactive (F6 to sort, F9 to kill)
free -h                # RAM usage
df -h                  # disk space
iostat -x 1            # disk I/O per second
watch -n 1 'ps aux --sort=-%cpu | head -10'  # top processes
```

**PowerShell:**
```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-PSDrive -PSProvider FileSystem
```

---

### How to manage users (Linux)

```bash
# Create a new user with home directory
useradd -m -s /bin/bash username

# Set their password
passwd username

# Add user to sudo/wheel group
usermod -aG sudo username       # Debian/Ubuntu
usermod -aG wheel username      # RHEL/Fedora

# Check a user's groups
groups username

# Switch to another user
su - username
```

---

### How to write a basic shell script

```bash
#!/bin/bash
set -euo pipefail          # exit on error, undefined vars, pipe failures

NAME=${1:-"World"}         # first arg, default "World"

echo "Hello, $NAME!"

# Check if a file exists
if [ -f "/etc/hosts" ]; then
    echo "hosts file exists"
fi

# Loop over files
for file in *.log; do
    echo "Processing: $file"
    grep -c "ERROR" "$file" || true
done
```

---

### How to schedule tasks

**Linux cron:**
```bash
crontab -e     # open cron editor
# Format: minute hour day-of-month month day-of-week command
# Examples:
0 2 * * *      /home/user/backup.sh          # every day at 2am
*/5 * * * *    /usr/bin/check_service.sh     # every 5 minutes
0 9 * * 1      /usr/bin/weekly_report.sh     # every Monday 9am
```

**PowerShell:**
```powershell
$trigger = New-ScheduledTaskTrigger -Daily -At "02:00AM"
$action  = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-File C:\Scripts\backup.ps1"
Register-ScheduledTask -TaskName "NightlyBackup" -Trigger $trigger -Action $action -RunLevel Highest
```

---

### How to manage packages

**Debian / Ubuntu:**
```bash
sudo apt update && sudo apt upgrade       # update all
sudo apt install package-name             # install
sudo apt remove package-name              # uninstall
sudo apt search keyword                   # search
```

**RHEL / Fedora / CentOS:**
```bash
sudo dnf upgrade                          # update all
sudo dnf install package-name
sudo dnf remove package-name
sudo dnf search keyword
```

**Arch Linux:**
```bash
sudo pacman -Syu                          # update all
sudo pacman -S package-name
sudo pacman -R package-name
sudo pacman -Ss keyword
```

**PowerShell (winget / PSGallery):**
```powershell
winget install package-name
Install-Module -Name ModuleName -Scope CurrentUser
```

---

## Quick Reference: Essential Flags

| Command | Must-Know Flags |
|---------|----------------|
| `ls` | `-la` (all + long), `-lht` (sorted by time) |
| `grep` | `-rni` (recursive, line numbers, case-insensitive), `-v` (invert) |
| `find` | `-name`, `-type f/d`, `-mtime -N`, `-size +Nk`, `-exec {} \;` |
| `tar` | `-czf` (create gzip), `-xzf` (extract), `-tzf` (list) |
| `curl` | `-sLo file URL` (silent, follow redirect, output) |
| `ssh` | `-p` (port), `-i` (key), `-L/-R` (port forward) |
| `rsync` | `-avz` (archive, verbose, compress), `--delete`, `-n` (dry run) |
| `ps` | `aux` (all processes), `--forest` (tree) |
| `sed` | `-i 's/old/new/g'` (in-place replace) |
| `awk` | `-F:` (delimiter), `'{print $1}'` (first field) |
| `chmod` | `+x` (add exec), `644` (rw-r--r--), `755` (rwxr-xr-x) |

---

## Tips

- **`man command`** — built-in manual page for any command
- **`command --help`** — quick flag summary
- **`tldr command`** — community short examples (install: `npm i -g tldr`)
- **`Ctrl+R`** in bash/zsh — fuzzy reverse search through command history
- **`!!`** — repeat last command; `sudo !!` to re-run it with sudo
- **`Ctrl+Z`** — suspend a process, then `bg` to resume in background
- In PowerShell, every cmdlet supports `-WhatIf` to preview destructive actions before running
