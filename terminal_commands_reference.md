# 💻 Terminal Commands Reference

> Essential shell commands & options

**142 commands** across **11 categories** — Generated May 30, 2026

---

## Table of Contents

- [Navigation](#navigation) `6`
- [Files](#files) `12`
- [Text](#text) `15`
- [Archives](#archives) `5`
- [Processes](#processes) `13`
- [Network](#network) `15`
- [Disk](#disk) `10`
- [Users](#users) `13`
- [System](#system) `22`
- [Package Mgmt](#package-mgmt) `10`
- [Shell](#shell) `21`

---

## Navigation

### `ls`

List directory contents

**Syntax**

```bash
ls [options] [path]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-a` | show hidden  |
| `-l` | long listing |
| `-h` | human sizes  |
| `-R` | recursive    |
| `-t` | sort by time |

---

### `cd`

Change directory

**Syntax**

```bash
cd [path]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `~`  | home dir     |
| `..` | parent dir   |
| `-`  | previous dir |

---

### `pwd`

Print working directory

**Syntax**

```bash
pwd
```

---

### `find`

Search for files

**Syntax**

```bash
find [path] [expr]
```

**Options**

| Flag     | Description     |
| -------- | --------------- |
| `-name`  | by name         |
| `-type`  | f/d file or dir |
| `-mtime` | modified time   |
| `-size`  | by size         |
| `-exec`  | run command     |

---

### `locate`

Find files by name (db)

**Syntax**

```bash
locate pattern
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-i` | case insensitive |
| `-n` | limit results    |

---

### `tree`

Directory tree view

**Syntax**

```bash
tree [path]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-L` | depth limit |
| `-a` | show hidden |
| `-d` | dirs only   |

---

## Files

### `cp`

Copy files/dirs

**Syntax**

```bash
cp [options] src dst
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-r` | recursive      |
| `-p` | preserve attrs |
| `-u` | update only    |
| `-v` | verbose        |

---

### `mv`

Move / rename

**Syntax**

```bash
mv [options] src dst
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-i` | interactive |
| `-u` | update only |
| `-v` | verbose     |

---

### `rm`

Remove files/dirs

**Syntax**

```bash
rm [options] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | recursive   |
| `-f` | force       |
| `-i` | interactive |
| `-v` | verbose     |

---

### `mkdir`

Create directory

**Syntax**

```bash
mkdir [options] dir
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-p` | create parents |
| `-v` | verbose        |

---

### `touch`

Create file / update timestamp

**Syntax**

```bash
touch file
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-a` | access time only |
| `-m` | modify time only |

---

### `ln`

Create link

**Syntax**

```bash
ln [options] src dst
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-s` | symbolic link |
| `-f` | force         |

---

### `chmod`

Change permissions

**Syntax**

```bash
chmod [options] mode file
```

**Options**

| Flag      | Description          |
| --------- | -------------------- |
| `-R`      | recursive            |
| `u/g/o/a` | user/group/other/all |
| `+x`      | add execute          |

---

### `chown`

Change ownership

**Syntax**

```bash
chown user:group file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-R` | recursive   |

---

### `stat`

File status/metadata

**Syntax**

```bash
stat file
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-c` | format output |

---

### `file`

Determine file type

**Syntax**

```bash
file file
```

---

### `du`

Disk usage of files

**Syntax**

```bash
du [options] path
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-s` | summary        |
| `-h` | human readable |
| `-a` | all files      |

---

### `rename`

Batch rename files

**Syntax**

```bash
rename 's/old/new/' files
```

---

## Text

### `cat`

Concatenate / view files

**Syntax**

```bash
cat [options] file
```

**Options**

| Flag | Description        |
| ---- | ------------------ |
| `-n` | line numbers       |
| `-A` | show special chars |
| `-s` | squeeze blanks     |

---

### `less`

Page through file

**Syntax**

```bash
less file
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-N` | line numbers |
| `-S` | no wrap      |
| `/`  | search       |

---

### `head`

Show first N lines

**Syntax**

```bash
head -n N file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | lines       |
| `-c` | bytes       |

---

### `tail`

Show last N lines

**Syntax**

```bash
tail -n N file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | lines       |
| `-f` | follow      |
| `-c` | bytes       |

---

### `grep`

Search text patterns

**Syntax**

```bash
grep [options] pattern file
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-r` | recursive        |
| `-i` | case insensitive |
| `-n` | line numbers     |
| `-v` | invert match     |
| `-l` | files only       |
| `-E` | extended regex   |
| `-c` | count matches    |

---

### `sed`

Stream editor

**Syntax**

```bash
sed 's/old/new/g' file
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-i` | edit in place   |
| `-n` | suppress output |
| `-e` | add expression  |

---

### `awk`

Text processing

**Syntax**

```bash
awk '{print $1}' file
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-F` | field separator |
| `-v` | set variable    |
| `-f` | script file     |

---

### `sort`

Sort lines

**Syntax**

```bash
sort [options] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | numeric     |
| `-r` | reverse     |
| `-u` | unique      |
| `-k` | key field   |

---

### `uniq`

Filter duplicate lines

**Syntax**

```bash
uniq [options] file
```

**Options**

| Flag | Description       |
| ---- | ----------------- |
| `-c` | count occurrences |
| `-d` | show duplicates   |
| `-u` | unique only       |

---

### `wc`

Word / line / byte count

**Syntax**

```bash
wc [options] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | lines       |
| `-w` | words       |
| `-c` | bytes       |

---

### `cut`

Extract columns

**Syntax**

```bash
cut [options] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | delimiter   |
| `-f` | fields      |
| `-c` | characters  |

---

### `tr`

Translate characters

**Syntax**

```bash
tr set1 set2
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-d` | delete chars    |
| `-s` | squeeze repeats |

---

### `diff`

Compare two files

**Syntax**

```bash
diff [options] file1 file2
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | unified     |
| `-r` | recursive   |
| `-i` | ignore case |

---

### `tee`

Read stdin, write to file+stdout

**Syntax**

```bash
cmd | tee file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | append      |

---

### `xargs`

Build and run commands

**Syntax**

```bash
cmd | xargs [cmd]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-n` | max args       |
| `-I` | replace string |
| `-0` | null separated |

---

## Archives

### `tar`

Archive files

**Syntax**

```bash
tar [options] archive files
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-c` | create        |
| `-x` | extract       |
| `-v` | verbose       |
| `-f` | filename      |
| `-z` | gzip          |
| `-j` | bzip2         |
| `-t` | list contents |

---

### `gzip`

Compress / decompress

**Syntax**

```bash
gzip [options] file
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-d` | decompress      |
| `-k` | keep original   |
| `-v` | verbose         |
| `-9` | max compression |

---

### `zip`

Create ZIP archive

**Syntax**

```bash
zip archive.zip files
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-r` | recursive       |
| `-e` | encrypt         |
| `-9` | max compression |
| `-u` | update          |

---

### `unzip`

Extract ZIP archive

**Syntax**

```bash
unzip archive.zip
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-d` | output dir    |
| `-l` | list contents |
| `-o` | overwrite     |

---

### `7z`

7-Zip archiver

**Syntax**

```bash
7z [cmd] archive files
```

**Options**

| Flag | Description          |
| ---- | -------------------- |
| `a`  | add e extract l list |
| `-p` | password             |

---

## Processes

### `ps`

List processes

**Syntax**

```bash
ps [options]
```

**Options**

| Flag       | Description          |
| ---------- | -------------------- |
| `aux`      | all processes        |
| `-ef`      | all with full format |
| `--forest` | tree view            |

---

### `top`

Real-time process viewer

**Syntax**

```bash
top
```

**Options**

| Flag | Description          |
| ---- | -------------------- |
| `q`  | quit k kill r renice |
| `M`  | sort by memory       |

---

### `htop`

Interactive process viewer

**Syntax**

```bash
htop
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `F5` | tree F9 kill |
| `F6` | sort         |

---

### `kill`

Send signal to process

**Syntax**

```bash
kill [signal] PID
```

**Options**

| Flag  | Description      |
| ----- | ---------------- |
| `-9`  | SIGKILL force    |
| `-15` | SIGTERM graceful |
| `-l`  | list signals     |

---

### `killall`

Kill by name

**Syntax**

```bash
killall name
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-9` | force       |
| `-u` | user        |

---

### `pkill`

Kill by pattern

**Syntax**

```bash
pkill pattern
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `-f`      | match full cmd |
| `-u`      | user           |
| `-signal` | signal         |

---

### `pgrep`

Find PID by pattern

**Syntax**

```bash
pgrep pattern
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | show name   |
| `-a` | full cmd    |
| `-u` | user        |

---

### `bg`

Resume job in background

**Syntax**

```bash
bg [job]
```

---

### `fg`

Bring job to foreground

**Syntax**

```bash
fg [job]
```

---

### `jobs`

List background jobs

**Syntax**

```bash
jobs
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | show PID    |

---

### `nohup`

Run immune to hangup

**Syntax**

```bash
nohup cmd &
```

---

### `nice`

Run with priority

**Syntax**

```bash
nice -n N cmd
```

---

### `renice`

Change process priority

**Syntax**

```bash
renice N -p PID
```

---

## Network

### `ping`

Test network connectivity

**Syntax**

```bash
ping [options] host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | count       |
| `-i` | interval    |
| `-t` | TTL         |

---

### `curl`

Transfer data from URL

**Syntax**

```bash
curl [options] URL
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-o` | output file     |
| `-X` | method          |
| `-H` | header          |
| `-d` | data            |
| `-s` | silent          |
| `-L` | follow redirect |
| `-k` | insecure        |

---

### `wget`

Download from URL

**Syntax**

```bash
wget [options] URL
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `-O`           | output      |
| `-r`           | recursive   |
| `-q`           | quiet       |
| `--limit-rate` | —           |

---

### `ssh`

Secure shell remote login

**Syntax**

```bash
ssh user@host
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-p` | port           |
| `-i` | key file       |
| `-L` | local forward  |
| `-R` | remote forward |
| `-N` | no command     |

---

### `scp`

Secure copy over SSH

**Syntax**

```bash
scp src user@host:dst
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-r` | recursive      |
| `-P` | port           |
| `-i` | key            |
| `-p` | preserve attrs |

---

### `rsync`

Remote / local file sync

**Syntax**

```bash
rsync [options] src dst
```

**Options**

| Flag       | Description  |
| ---------- | ------------ |
| `-a`       | archive mode |
| `-v`       | verbose      |
| `-z`       | compress     |
| `-n`       | dry run      |
| `--delete` | remove extra |
| `-e`       | ssh use SSH  |

---

### `netstat`

Network connections

**Syntax**

```bash
netstat [options]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | TCP         |
| `-u` | UDP         |
| `-l` | listening   |
| `-n` | numeric     |
| `-p` | show PID    |

---

### `ss`

Socket statistics

**Syntax**

```bash
ss [options]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | TCP         |
| `-u` | UDP         |
| `-l` | listening   |
| `-p` | process     |
| `-n` | numeric     |

---

### `ip`

IP address / routing

**Syntax**

```bash
ip [obj] [cmd]
```

**Options**

| Flag    | Description     |
| ------- | --------------- |
| `addr`  | show IP addrs   |
| `route` | show routes     |
| `link`  | show interfaces |

---

### `nmap`

Network scanner

**Syntax**

```bash
nmap [options] target
```

**Options**

| Flag  | Description    |
| ----- | -------------- |
| `-sV` | version detect |
| `-p`  | ports          |
| `-A`  | aggressive     |
| `-O`  | OS detect      |

---

### `dig`

DNS lookup

**Syntax**

```bash
dig [options] domain
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `+short`  | —           |
| `+noall`  | +answer     |
| `@server` | use server  |
| `A/MX/NS` | record type |

---

### `traceroute`

Trace network path

**Syntax**

```bash
traceroute host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | no DNS      |
| `-m` | max hops    |

---

### `nslookup`

DNS name query

**Syntax**

```bash
nslookup domain
```

---

### `iptables`

Firewall rules

**Syntax**

```bash
iptables [options]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-L` | list        |
| `-A` | append      |
| `-D` | delete      |
| `-I` | insert      |
| `-F` | flush       |

---

### `ufw`

Uncomplicated firewall

**Syntax**

```bash
ufw [cmd]
```

**Options**

| Flag             | Description |
| ---------------- | ----------- |
| `enable/disable` | —           |
| `allow/deny`     | port        |
| `status`         | verbose     |

---

## Disk

### `df`

Disk space usage

**Syntax**

```bash
df [options]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-h` | human readable |
| `-T` | show fs type   |
| `-i` | show inodes    |

---

### `lsblk`

List block devices

**Syntax**

```bash
lsblk [options]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-f` | show filesystem |
| `-o` | columns         |
| `-a` | all devices     |

---

### `mount`

Mount filesystem

**Syntax**

```bash
mount [options] dev mnt
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-t` | fs type         |
| `-o` | options         |
| `-a` | mount all fstab |

---

### `umount`

Unmount filesystem

**Syntax**

```bash
umount dev|mnt
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | lazy        |
| `-f` | force       |

---

### `fdisk`

Partition table manager

**Syntax**

```bash
fdisk [options] dev
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-l` | list partitions |
| `-n` | new partition   |

---

### `mkfs`

Make filesystem

**Syntax**

```bash
mkfs -t type dev
```

**Options**

| Flag   | Description    |
| ------ | -------------- |
| `ext4` | xfs fat32 ntfs |

---

### `fsck`

Filesystem check / repair

**Syntax**

```bash
fsck [options] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | auto repair |
| `-y` | answer yes  |

---

### `dd`

Convert and copy raw data

**Syntax**

```bash
dd if=src of=dst
```

**Options**

| Flag              | Description |
| ----------------- | ----------- |
| `bs=`             | block size  |
| `count=`          | blocks      |
| `status=progress` | —           |

---

### `blkid`

Block device attributes

**Syntax**

```bash
blkid [dev]
```

---

### `parted`

Partition manager

**Syntax**

```bash
parted [dev]
```

**Options**

| Flag    | Description          |
| ------- | -------------------- |
| `print` | mkpart rm resizepart |

---

## Users

### `whoami`

Current username

**Syntax**

```bash
whoami
```

---

### `id`

User/group IDs

**Syntax**

```bash
id [user]
```

---

### `w`

Who is logged in + activity

**Syntax**

```bash
w
```

---

### `who`

Who is logged in

**Syntax**

```bash
who
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all info    |

---

### `last`

Login history

**Syntax**

```bash
last [user]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-n` | lines          |
| `-x` | show shutdowns |

---

### `sudo`

Run as superuser

**Syntax**

```bash
sudo [options] cmd
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-u` | user             |
| `-i` | login shell      |
| `-l` | list permissions |

---

### `su`

Switch user

**Syntax**

```bash
su [user]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-`  | login shell |
| `-c` | run command |

---

### `useradd`

Add user

**Syntax**

```bash
useradd [options] user
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-m` | create home |
| `-s` | shell       |
| `-G` | groups      |
| `-c` | comment     |

---

### `usermod`

Modify user

**Syntax**

```bash
usermod [options] user
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `-aG` | add to group |
| `-l`  | rename       |
| `-s`  | change shell |

---

### `userdel`

Delete user

**Syntax**

```bash
userdel [options] user
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | remove home |

---

### `passwd`

Change password

**Syntax**

```bash
passwd [user]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | lock        |
| `-u` | unlock      |
| `-e` | expire      |

---

### `groupadd`

Create group

**Syntax**

```bash
groupadd group
```

---

### `groups`

Show user groups

**Syntax**

```bash
groups [user]
```

---

## System

### `uname`

System information

**Syntax**

```bash
uname [options]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-a` | all info       |
| `-r` | kernel release |
| `-m` | machine type   |

---

### `uptime`

System uptime

**Syntax**

```bash
uptime
```

---

### `hostname`

Show / set hostname

**Syntax**

```bash
hostname [name]
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-I` | show IP addrs |
| `-f` | FQDN          |

---

### `date`

Show / set date & time

**Syntax**

```bash
date [options] [+format]
```

**Options**

| Flag        | Description |
| ----------- | ----------- |
| `+%Y-%m-%d` | +%H:%M:%S   |
| `-s`        | set date    |

---

### `cal`

Calendar

**Syntax**

```bash
cal [month] [year]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-3` | three months |
| `-y` | full year    |

---

### `timedatectl`

System time/date control

**Syntax**

```bash
timedatectl [cmd]
```

**Options**

| Flag             | Description           |
| ---------------- | --------------------- |
| `status`         | set-time set-timezone |
| `list-timezones` | —                     |

---

### `systemctl`

Service manager

**Syntax**

```bash
systemctl [cmd] service
```

**Options**

| Flag         | Description    |
| ------------ | -------------- |
| `start`      | stop restart   |
| `status`     | enable disable |
| `list-units` | —              |

---

### `journalctl`

Query systemd logs

**Syntax**

```bash
journalctl [options]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `-u`      | unit        |
| `-f`      | follow      |
| `-b`      | this boot   |
| `--since` | date        |

---

### `dmesg`

Kernel ring buffer

**Syntax**

```bash
dmesg [options]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-H` | human readable |
| `-T` | timestamps     |
| `-l` | log levels     |

---

### `lshw`

Hardware info

**Syntax**

```bash
lshw [options]
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `-short` | summary     |
| `-class` | filter      |
| `-html`  | output      |

---

### `lscpu`

CPU architecture info

**Syntax**

```bash
lscpu
```

---

### `free`

Memory usage

**Syntax**

```bash
free [options]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-h` | human readable  |
| `-s` | seconds (watch) |
| `-m` | MB              |

---

### `vmstat`

Virtual memory stats

**Syntax**

```bash
vmstat [interval]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | summary     |
| `-d` | disk        |
| `-p` | partition   |

---

### `env`

Show environment variables

**Syntax**

```bash
env
```

**Options**

| Flag | Description       |
| ---- | ----------------- |
| `-i` | empty environment |
| `-u` | unset variable    |

---

### `export`

Set env variable

**Syntax**

```bash
export VAR=value
```

---

### `alias`

Create command alias

**Syntax**

```bash
alias name='cmd'
```

---

### `history`

Command history

**Syntax**

```bash
history [n]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `!!` | last command    |
| `!n` | run nth command |
| `-c` | clear history   |

---

### `cron`

Schedule tasks (crontab)

**Syntax**

```bash
crontab [options]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-e` | edit        |
| `-l` | list        |
| `-r` | remove      |

---

### `at`

Run command once later

**Syntax**

```bash
at time
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | list jobs   |
| `-d` | delete job  |

---

### `reboot`

Reboot system

**Syntax**

```bash
reboot
```

**Options**

| Flag        | Description |
| ----------- | ----------- |
| `-f`        | force       |
| `--no-wall` | no message  |

---

### `shutdown`

Shutdown system

**Syntax**

```bash
shutdown [options] [time]
```

**Options**

| Flag  | Description |
| ----- | ----------- |
| `-h`  | halt        |
| `-r`  | reboot      |
| `-c`  | cancel      |
| `now` | +5 23:00    |

---

### `poweroff`

Power off system

**Syntax**

```bash
poweroff
```

---

## Package Mgmt

### `apt`

Debian/Ubuntu packages

**Syntax**

```bash
apt [cmd] [pkg]
```

**Options**

| Flag         | Description  |
| ------------ | ------------ |
| `install`    | remove purge |
| `update`     | upgrade      |
| `search`     | show         |
| `autoremove` | clean        |

---

### `apt-get`

APT package tool

**Syntax**

```bash
apt-get [cmd] [pkg]
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `install`      | remove      |
| `update`       | upgrade     |
| `dist-upgrade` | —           |

---

### `dpkg`

Debian package manager

**Syntax**

```bash
dpkg [options] pkg
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-i` | install .deb |
| `-r` | remove       |
| `-l` | list         |
| `-s` | status       |

---

### `yum`

RPM package manager

**Syntax**

```bash
yum [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | remove      |
| `update`  | search      |
| `list`    | info        |

---

### `dnf`

Fedora/RHEL packages

**Syntax**

```bash
dnf [cmd] [pkg]
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `install`    | remove      |
| `update`     | search      |
| `autoremove` | —           |

---

### `pacman`

Arch Linux packages

**Syntax**

```bash
pacman [options] [pkg]
```

**Options**

| Flag  | Description    |
| ----- | -------------- |
| `-S`  | install        |
| `-R`  | remove         |
| `-U`  | upgrade        |
| `-Ss` | search         |
| `-Q`  | list installed |

---

### `snap`

Snap package manager

**Syntax**

```bash
snap [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | remove      |
| `list`    | refresh     |
| `find`    | —           |

---

### `flatpak`

Flatpak packages

**Syntax**

```bash
flatpak [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | uninstall   |
| `list`    | update      |
| `run`     | —           |

---

### `npm`

Node package manager

**Syntax**

```bash
npm [cmd] [pkg]
```

**Options**

| Flag      | Description  |
| --------- | ------------ |
| `install` | uninstall    |
| `update`  | list         |
| `run`     | init publish |

---

### `pip`

Python packages

**Syntax**

```bash
pip install pkg
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | uninstall   |
| `freeze`  | list        |
| `show`    | search      |

---

## Shell

### `echo`

Print text to stdout

**Syntax**

```bash
echo [options] text
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-n` | no newline       |
| `-e` | escape sequences |
| `-E` | disable escapes  |

---

### `printf`

Formatted print

**Syntax**

```bash
printf format [args]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `\n` | newline \t tab |
| `%s` | string %d int  |

---

### `read`

Read input from stdin

**Syntax**

```bash
read [options] var
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | prompt      |
| `-s` | silent      |
| `-n` | chars       |
| `-t` | timeout     |

---

### `source`

Execute script in current shell

**Syntax**

```bash
source file  or  . file
```

---

### `exec`

Replace shell with command

**Syntax**

```bash
exec cmd
```

---

### `test`

Evaluate expression

**Syntax**

```bash
test expr  or  [ expr ]
```

**Options**

| Flag  | Description         |
| ----- | ------------------- |
| `-f`  | file exists         |
| `-d`  | directory           |
| `-z`  | string empty        |
| `-n`  | string not empty    |
| `-eq` | -ne -lt -gt numeric |

---

### `true`

Exit with success (0)

**Syntax**

```bash
true
```

---

### `false`

Exit with failure (1)

**Syntax**

```bash
false
```

---

### `exit`

Exit shell

**Syntax**

```bash
exit [code]
```

---

### `set`

Set shell options

**Syntax**

```bash
set [options]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-e` | exit on error  |
| `-x` | debug trace    |
| `-u` | undefined vars |
| `-o` | pipefail       |

---

### `type`

How command is interpreted

**Syntax**

```bash
type name
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-a` | all locations |
| `-t` | type only     |

---

### `which`

Locate command

**Syntax**

```bash
which cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all matches |

---

### `whereis`

Locate binary/man/source

**Syntax**

```bash
whereis cmd
```

---

### `man`

User manual pages

**Syntax**

```bash
man [section] cmd
```

**Options**

| Flag       | Description       |
| ---------- | ----------------- |
| `-k`       | keyword search    |
| `-f`       | brief description |
| `-a`       | all sections      |
| `-P pager` | set pager         |
| `-w`       | show page path    |

**Sections**

| # | Content           |
| - | ----------------- |
| 1 | User commands     |
| 2 | System calls      |
| 3 | Library functions |
| 4 | Device files      |
| 5 | File formats      |
| 6 | Games             |
| 7 | Miscellaneous     |
| 8 | Admin commands    |
| 9 | Kernel routines   |

**Navigation** (uses `less`)

| Key     | Action         |
| ------- | -------------- |
| `q`     | quit           |
| `Space` | next page      |
| `b`     | previous page  |
| `/term` | search forward |
| `n`     | next match     |
| `N`     | prev match     |
| `g`     | top            |
| `G`     | bottom         |

**Examples**

```bash
man ls               # manual for ls
man 3 printf         # library function, not shell printf
man -k "list files"  # search descriptions
man -f ls            # one-line summary
```

---

### `help`

Shell builtin help

**Syntax**

```bash
help [cmd]
```

---

### `info`

Info page reader

**Syntax**

```bash
info [cmd]
```

---

### `time`

Time command execution

**Syntax**

```bash
time cmd
```

---

### `watch`

Run command repeatedly

**Syntax**

```bash
watch [options] cmd
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-n` | interval (secs) |
| `-d` | highlight diffs |
| `-e` | exit on error   |

---

### `screen`

Terminal multiplexer

**Syntax**

```bash
screen [options]
```

**Options**

| Flag  | Description      |
| ----- | ---------------- |
| `-S`  | name new session |
| `-r`  | reattach         |
| `-ls` | list sessions    |
| `C-a` | d detach         |

---

### `tmux`

Terminal multiplexer

**Syntax**

```bash
tmux [cmd]
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `new` | attach ls    |
| `-s`  | session name |
| `C-b` | d detach     |

---

### `strace`

Trace system calls

**Syntax**

```bash
strace cmd
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-p` | PID attach   |
| `-e` | trace filter |
| `-o` | output file  |

---
