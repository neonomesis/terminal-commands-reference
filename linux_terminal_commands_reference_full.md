# 🐧 Linux Terminal Commands

> Complete command & flag reference

**394 commands** across **24 categories** — Generated May 30, 2026

---

## Table of Contents

- [Navigation](#navigation) `10`
- [Files](#files) `16`
- [Text](#text) `32`
- [Search](#search) `8`
- [Archives](#archives) `11`
- [Processes](#processes) `22`
- [Network](#network) `26`
- [Disk](#disk) `24`
- [Users & Groups](#users--groups) `23`
- [Permissions](#permissions) `10`
- [System Info](#system-info) `18`
- [Services](#services) `9`
- [Kernel & Modules](#kernel--modules) `10`
- [Memory](#memory) `7`
- [Monitoring](#monitoring) `13`
- [Package Mgmt](#package-mgmt) `15`
- [SSH & Remote](#ssh--remote) `11`
- [Firewall](#firewall) `6`
- [Containers](#containers) `6`
- [Git](#git) `28`
- [Shell & Scripting](#shell--scripting) `36`
- [Environment](#environment) `8`
- [Cron & Jobs](#cron--jobs) `8`
- [Misc](#misc) `37`

---

## Navigation

### `ls`

List directory

**Syntax**

```bash
ls [opts] [path]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `-a`      | hidden      |
| `-l`      | long        |
| `-h`      | sizes       |
| `-R`      | recurse     |
| `-t`      | by time     |
| `--color` | colorize    |

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
| `~`  | home         |
| `..` | parent       |
| `-`  | previous dir |

---

### `pwd`

Print working dir

**Syntax**

```bash
pwd
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-L` | logical path  |
| `-P` | physical path |

---

### `pushd`

Push dir to stack

**Syntax**

```bash
pushd [dir]
```

---

### `popd`

Pop dir from stack

**Syntax**

```bash
popd
```

---

### `dirs`

Show dir stack

**Syntax**

```bash
dirs
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-v` | numbered    |
| `-c` | clear stack |

---

### `tree`

Tree view of dirs

**Syntax**

```bash
tree [path]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-L` | depth       |
| `-a` | hidden      |
| `-d` | dirs only   |
| `-f` | full paths  |

---

### `realpath`

Resolve absolute path

**Syntax**

```bash
realpath [path]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-m` | missing ok  |
| `-q` | quiet       |

---

### `basename`

Strip directory from path

**Syntax**

```bash
basename path
```

---

### `dirname`

Strip file from path

**Syntax**

```bash
dirname path
```

---

## Files

### `cp`

Copy files

**Syntax**

```bash
cp [opts] src dst
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | recurse     |
| `-p` | preserve    |
| `-u` | update only |
| `-v` | verbose     |
| `-i` | interactive |
| `-l` | hardlink    |

---

### `mv`

Move / rename

**Syntax**

```bash
mv [opts] src dst
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-i` | interactive  |
| `-u` | update only  |
| `-v` | verbose      |
| `-n` | no overwrite |

---

### `rm`

Remove files

**Syntax**

```bash
rm [opts] file
```

**Options**

| Flag              | Description |
| ----------------- | ----------- |
| `-r`              | recursive   |
| `-f`              | force       |
| `-i`              | interactive |
| `-v`              | verbose     |
| `--preserve-root` | —           |

---

### `mkdir`

Create directory

**Syntax**

```bash
mkdir [opts] dir
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | parents     |
| `-m` | mode        |
| `-v` | verbose     |

---

### `rmdir`

Remove empty dir

**Syntax**

```bash
rmdir dir
```

**Options**

| Flag                         | Description |
| ---------------------------- | ----------- |
| `--ignore-fail-on-non-empty` | —           |
| `-p`                         | parents     |

---

### `touch`

Create / update timestamp

**Syntax**

```bash
touch file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | access time |
| `-m` | modify time |
| `-t` | timestamp   |
| `-c` | no create   |

---

### `ln`

Create link

**Syntax**

```bash
ln [opts] src dst
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | symbolic    |
| `-f` | force       |
| `-v` | verbose     |
| `-b` | backup      |

---

### `rename`

Batch rename

**Syntax**

```bash
rename 's/old/new/' files
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | dry run     |
| `-v` | verbose     |

---

### `install`

Copy with permissions

**Syntax**

```bash
install [opts] src dst
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-m` | mode        |
| `-o` | owner       |
| `-g` | group       |
| `-d` | create dir  |

---

### `shred`

Securely delete file

**Syntax**

```bash
shred [opts] file
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-u` | remove after |
| `-n` | passes       |
| `-z` | zero final   |

---

### `truncate`

Shrink or extend file

**Syntax**

```bash
truncate -s size file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | size        |
| `-r` | ref file    |

---

### `mktemp`

Create temp file/dir

**Syntax**

```bash
mktemp [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | create dir  |
| `-p` | dir         |
| `-t` | template    |

---

### `file`

Determine file type

**Syntax**

```bash
file file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-b` | brief       |
| `-i` | MIME type   |
| `-L` | follow link |

---

### `stat`

File status

**Syntax**

```bash
stat file
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-c` | format          |
| `-L` | follow link     |
| `-f` | filesystem info |

---

### `readlink`

Read symlink target

**Syntax**

```bash
readlink [opts] link
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-f` | canonicalize     |
| `-e` | must exist       |
| `-m` | tolerate missing |

---

### `lsof`

List open files

**Syntax**

```bash
lsof [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | user        |
| `-p` | PID         |
| `-i` | network     |
| `+d` | dir         |
| `-t` | terse       |

---

## Text

### `cat`

Concatenate / print

**Syntax**

```bash
cat [opts] file
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-n` | line numbers     |
| `-A` | show special     |
| `-s` | squeeze blanks   |
| `-b` | number non-blank |

---

### `tac`

Reverse cat

**Syntax**

```bash
tac file
```

---

### `less`

Page through file

**Syntax**

```bash
less [opts] file
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-N` | numbers          |
| `-S` | chop lines       |
| `-R` | color            |
| `-F` | quit if 1 screen |
| `-X` | no clear         |

---

### `more`

Page forward only

**Syntax**

```bash
more file
```

---

### `head`

First N lines

**Syntax**

```bash
head [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | lines       |
| `-c` | bytes       |
| `-q` | quiet       |

---

### `tail`

Last N lines

**Syntax**

```bash
tail [opts] file
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `-n`      | lines       |
| `-f`      | follow      |
| `-c`      | bytes       |
| `--retry` | —           |

---

### `grep`

Search patterns

**Syntax**

```bash
grep [opts] pattern file
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `-r`      | recurse        |
| `-i`      | ignore case    |
| `-n`      | line nums      |
| `-v`      | invert         |
| `-l`      | files only     |
| `-c`      | count          |
| `-E`      | extended regex |
| `-P`      | perl regex     |
| `-A/B/C`  | context        |
| `-o`      | only match     |
| `--color` | —              |

---

### `egrep`

Extended grep

**Syntax**

```bash
egrep pattern file
```

---

### `fgrep`

Fixed string grep

**Syntax**

```bash
fgrep pattern file
```

---

### `sed`

Stream editor

**Syntax**

```bash
sed 's/old/new/g' file
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-i` | in-place       |
| `-n` | suppress       |
| `-e` | expression     |
| `-f` | script         |
| `-r` | extended regex |

---

### `awk`

Text processing

**Syntax**

```bash
awk '{print $1}' file
```

**Options**

| Flag  | Description |
| ----- | ----------- |
| `-F`  | separator   |
| `-v`  | variable    |
| `-f`  | script      |
| `-NR` | line number |

---

### `sort`

Sort lines

**Syntax**

```bash
sort [opts] file
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-n` | numeric       |
| `-r` | reverse       |
| `-u` | unique        |
| `-k` | key           |
| `-t` | delimiter     |
| `-h` | human numeric |
| `-R` | random        |

---

### `uniq`

Filter duplicates

**Syntax**

```bash
uniq [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | count       |
| `-d` | show dupes  |
| `-u` | unique only |
| `-i` | ignore case |

---

### `wc`

Count lines/words/bytes

**Syntax**

```bash
wc [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | lines       |
| `-w` | words       |
| `-c` | bytes       |
| `-m` | chars       |

---

### `cut`

Extract columns

**Syntax**

```bash
cut [opts] file
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `-d`           | delimiter   |
| `-f`           | fields      |
| `-c`           | characters  |
| `--complement` | —           |

---

### `paste`

Merge lines of files

**Syntax**

```bash
paste file1 file2
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | delimiter   |
| `-s` | serial      |

---

### `join`

Join on common field

**Syntax**

```bash
join file1 file2
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-1` | field1      |
| `-2` | field2      |
| `-t` | separator   |

---

### `tr`

Translate characters

**Syntax**

```bash
tr set1 set2
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | delete      |
| `-s` | squeeze     |
| `-c` | complement  |

---

### `fold`

Wrap lines

**Syntax**

```bash
fold -w N file
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-w` | width         |
| `-s` | word boundary |

---

### `fmt`

Format paragraphs

**Syntax**

```bash
fmt [opts] file
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-w` | width           |
| `-u` | uniform spacing |

---

### `column`

Format into columns

**Syntax**

```bash
column [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | table       |
| `-s` | separator   |
| `-R` | right align |

---

### `pr`

Paginate file

**Syntax**

```bash
pr [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-h` | header      |
| `-n` | number      |
| `-N` | page start  |

---

### `diff`

Compare files

**Syntax**

```bash
diff [opts] file1 file2
```

**Options**

| Flag      | Description       |
| --------- | ----------------- |
| `-u`      | unified           |
| `-r`      | recursive         |
| `-i`      | ignore case       |
| `-w`      | ignore whitespace |
| `--brief` | —                 |

---

### `patch`

Apply diff patch

**Syntax**

```bash
patch [opts] [file] < patch
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | strip level |
| `-R` | reverse     |
| `-b` | backup      |
| `-d` | dir         |

---

### `vimdiff`

Visual diff in vim

**Syntax**

```bash
vimdiff file1 file2
```

---

### `comm`

Compare sorted files

**Syntax**

```bash
comm file1 file2
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-1` | suppress col1 |
| `-2` | suppress col2 |
| `-3` | suppress col3 |

---

### `tee`

Fork stdout to file

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

Build commands from stdin

**Syntax**

```bash
cmd | xargs [cmd]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | max args    |
| `-I` | replace str |
| `-0` | null sep    |
| `-P` | parallel    |
| `-t` | trace       |

---

### `strings`

Extract printable strings

**Syntax**

```bash
strings [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | min len     |
| `-o` | offsets     |

---

### `hexdump`

Hex dump of file

**Syntax**

```bash
hexdump [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-C` | canonical   |
| `-n` | count       |

---

### `od`

Octal/hex dump

**Syntax**

```bash
od [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-x` | hex         |
| `-d` | decimal     |
| `-c` | chars       |
| `-A` | addr format |

---

### `iconv`

Convert encoding

**Syntax**

```bash
iconv -f from -t to file
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-f` | from encoding |
| `-t` | to encoding   |
| `-o` | output file   |
| `-l` | list codecs   |

---

## Search

### `find`

Search files

**Syntax**

```bash
find [path] [expr]
```

**Options**

| Flag        | Description      |
| ----------- | ---------------- |
| `-name`     | by name          |
| `-iname`    | case insensitive |
| `-type`     | f/d/l            |
| `-mtime`    | modified         |
| `-size`     | size             |
| `-user`     | owner            |
| `-perm`     | permissions      |
| `-exec`     | run cmd          |
| `!`         | negate           |
| `-maxdepth` | limit depth      |

---

### `locate`

Fast file search (db)

**Syntax**

```bash
locate pattern
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-i` | case insensitive |
| `-n` | limit            |
| `-e` | check exists     |
| `-r` | regex            |
| `-c` | count            |

---

### `updatedb`

Update locate database

**Syntax**

```bash
updatedb
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `--output`     | file        |
| `--prunepaths` | exclude     |

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

Locate binary/man/src

**Syntax**

```bash
whereis cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-b` | binary only |
| `-m` | manual only |
| `-s` | source only |

---

### `type`

Describe command type

**Syntax**

```bash
type name
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-a` | all locations |
| `-t` | type          |
| `-P` | path only     |

---

### `whatis`

One-line man description

**Syntax**

```bash
whatis cmd
```

---

### `apropos`

Search man descriptions

**Syntax**

```bash
apropos keyword
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-a` | all words match |
| `-l` | no trim         |

---

## Archives

### `tar`

Tape archive

**Syntax**

```bash
tar [opts] archive files
```

**Options**

| Flag                 | Description       |
| -------------------- | ----------------- |
| `c`                  | create x extract  |
| `v`                  | verbose f file    |
| `z`                  | gzip j bzip2 J xz |
| `t`                  | list r append     |
| `--delete`           | remove entry      |
| `--strip-components` | —                 |

---

### `gzip`

Compress gzip

**Syntax**

```bash
gzip [opts] file
```

**Options**

| Flag     | Description   |
| -------- | ------------- |
| `-d`     | decompress    |
| `-k`     | keep original |
| `-v`     | verbose       |
| `-r`     | recursive     |
| `-9`     | max           |
| `--best` | / --fast      |

---

### `gunzip`

Decompress gzip

**Syntax**

```bash
gunzip file.gz
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-k` | keep archive |
| `-v` | verbose      |

---

### `bzip2`

Compress bzip2

**Syntax**

```bash
bzip2 [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | decompress  |
| `-k` | keep        |
| `-v` | verbose     |
| `-9` | best        |

---

### `xz`

Compress xz

**Syntax**

```bash
xz [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | decompress  |
| `-k` | keep        |
| `-v` | verbose     |
| `-9` | max         |

---

### `zip`

Create ZIP

**Syntax**

```bash
zip archive.zip files
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-r` | recursive    |
| `-e` | encrypt      |
| `-9` | max compress |
| `-u` | update       |
| `-d` | delete       |

---

### `unzip`

Extract ZIP

**Syntax**

```bash
unzip archive.zip
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | output dir  |
| `-l` | list        |
| `-o` | overwrite   |
| `-q` | quiet       |
| `-p` | to stdout   |

---

### `7z`

7-Zip archiver

**Syntax**

```bash
7z [cmd] archive files
```

**Options**

| Flag   | Description            |
| ------ | ---------------------- |
| `a`    | add e extract x full   |
| `l`    | list d delete u update |
| `-p`   | password               |
| `-mhe` | encrypt names          |

---

### `zcat`

View gzip without extract

**Syntax**

```bash
zcat file.gz
```

---

### `bzcat`

View bzip2 without extract

**Syntax**

```bash
bzcat file.bz2
```

---

### `zgrep`

Grep in compressed file

**Syntax**

```bash
zgrep pattern file.gz
```

---

## Processes

### `ps`

Snapshot of processes

**Syntax**

```bash
ps [opts]
```

**Options**

| Flag       | Description   |
| ---------- | ------------- |
| `aux`      | all + BSD     |
| `ef`       | all + full    |
| `-u`       | user          |
| `--forest` | tree          |
| `-o`       | custom output |
| `-p`       | by PID        |

---

### `top`

Interactive process viewer

**Syntax**

```bash
top
```

**Options**

| Flag | Description         |
| ---- | ------------------- |
| `q`  | quit k kill         |
| `r`  | renice M mem sort   |
| `P`  | cpu sort 1 per-cpu  |
| `c`  | full cmdline u user |

---

### `htop`

Enhanced top

**Syntax**

```bash
htop
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `F5` | tree F9 kill   |
| `F6` | sort F4 filter |
| `u`  | user H threads |

---

### `kill`

Send signal to PID

**Syntax**

```bash
kill [signal] PID
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `-9`  | SIGKILL      |
| `-15` | SIGTERM      |
| `-1`  | SIGHUP       |
| `-2`  | SIGINT       |
| `-l`  | list signals |

---

### `killall`

Kill by name

**Syntax**

```bash
killall [opts] name
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-9` | force       |
| `-u` | user        |
| `-s` | signal      |
| `-i` | interactive |
| `-w` | wait        |

---

### `pkill`

Kill by pattern

**Syntax**

```bash
pkill [opts] pattern
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `-f`      | match full cmd |
| `-u`      | user           |
| `-signal` | signal         |
| `-n`      | newest         |
| `-o`      | oldest         |

---

### `pgrep`

Get PID by pattern

**Syntax**

```bash
pgrep [opts] pattern
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | show names  |
| `-a` | full cmd    |
| `-u` | user        |
| `-x` | exact match |

---

### `pidof`

PID of running program

**Syntax**

```bash
pidof name
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | single      |
| `-o` | omit PID    |

---

### `bg`

Resume in background

**Syntax**

```bash
bg [job]
```

---

### `fg`

Bring to foreground

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
| `-p` | PID only    |
| `-r` | running     |
| `-s` | stopped     |

---

### `nohup`

Immune to hangup

**Syntax**

```bash
nohup cmd &
```

---

### `disown`

Remove job from shell

**Syntax**

```bash
disown [job]
```

**Options**

| Flag | Description         |
| ---- | ------------------- |
| `-h` | keep but ignore HUP |
| `-a` | all jobs            |

---

### `nice`

Set process priority

**Syntax**

```bash
nice -n N cmd
```

---

### `renice`

Change running priority

**Syntax**

```bash
renice N -p PID
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | by user     |
| `-g` | by group    |

---

### `ionice`

I/O scheduling priority

**Syntax**

```bash
ionice -c class cmd
```

**Options**

| Flag | Description             |
| ---- | ----------------------- |
| `c1` | realtime c2 best-effort |
| `c3` | idle                    |
| `-n` | level 0-7               |

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
| `-p` | PID          |
| `-e` | filter       |
| `-o` | output       |
| `-f` | follow forks |
| `-c` | count        |

---

### `ltrace`

Trace library calls

**Syntax**

```bash
ltrace cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | PID         |
| `-o` | output      |

---

### `timeout`

Run with time limit

**Syntax**

```bash
timeout N cmd
```

**Options**

| Flag                | Description |
| ------------------- | ----------- |
| `--preserve-status` | —           |
| `-s`                | signal      |

---

### `wait`

Wait for process

**Syntax**

```bash
wait [PID]
```

---

### `trap`

Trap shell signals

**Syntax**

```bash
trap cmd SIGNAL
```

**Options**

| Flag  | Description   |
| ----- | ------------- |
| `INT` | TERM EXIT ERR |

---

### `fuser`

Identify users of files/sockets

**Syntax**

```bash
fuser [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-k` | kill procs  |
| `-m` | all on fs   |
| `-u` | show users  |
| `-v` | verbose     |

---

## Network

### `ping`

Test connectivity

**Syntax**

```bash
ping [opts] host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | count       |
| `-i` | interval    |
| `-t` | TTL         |
| `-s` | packet size |
| `-W` | timeout     |
| `-6` | IPv6        |

---

### `ping6`

IPv6 ping

**Syntax**

```bash
ping6 host
```

---

### `traceroute`

Trace route to host

**Syntax**

```bash
traceroute host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | no DNS      |
| `-m` | max hops    |
| `-I` | ICMP        |
| `-T` | TCP         |
| `-p` | port        |

---

### `mtr`

Traceroute + ping combined

**Syntax**

```bash
mtr host
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `--report` | batch mode  |
| `-c`       | count       |
| `-n`       | no DNS      |

---

### `curl`

Transfer data

**Syntax**

```bash
curl [opts] URL
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `-o`      | output      |
| `-X`      | method      |
| `-H`      | header      |
| `-d`      | data        |
| `-s`      | silent      |
| `-L`      | follow      |
| `-k`      | insecure    |
| `-u`      | user:pass   |
| `-F`      | form data   |
| `-v`      | verbose     |
| `--retry` | N           |

---

### `wget`

Download files

**Syntax**

```bash
wget [opts] URL
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `-O`           | output      |
| `-r`           | recursive   |
| `-q`           | quiet       |
| `--limit-rate` | —           |
| `--continue`   | —           |
| `-P`           | dir         |
| `-np`          | no parent   |

---

### `ip`

Network interfaces/routes

**Syntax**

```bash
ip [obj] [cmd]
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `addr`    | show IPs       |
| `link`    | interfaces     |
| `route`   | routes         |
| `neigh`   | neighbors      |
| `rule`    | policy routing |
| `monitor` | watch          |

---

### `ifconfig`

Interface config (legacy)

**Syntax**

```bash
ifconfig [iface]
```

**Options**

| Flag        | Description |
| ----------- | ----------- |
| `up`        | / down      |
| `netmask`   | —           |
| `broadcast` | —           |
| `-a`        | all         |

---

### `ss`

Socket statistics

**Syntax**

```bash
ss [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | TCP         |
| `-u` | UDP         |
| `-l` | listening   |
| `-a` | all         |
| `-p` | process     |
| `-n` | numeric     |
| `-s` | summary     |
| `-r` | resolve     |

---

### `netstat`

Network stats (legacy)

**Syntax**

```bash
netstat [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | TCP         |
| `-u` | UDP         |
| `-l` | listening   |
| `-n` | numeric     |
| `-p` | PID         |
| `-r` | routes      |

---

### `nmap`

Network scanner

**Syntax**

```bash
nmap [opts] target
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `-sS`      | SYN scan    |
| `-sV`      | versions    |
| `-p`       | ports       |
| `-A`       | aggressive  |
| `-O`       | OS detect   |
| `-Pn`      | no ping     |
| `--script` | NSE         |

---

### `ncat / nc`

Netcat

**Syntax**

```bash
nc [opts] host port
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | listen      |
| `-u` | UDP         |
| `-v` | verbose     |
| `-z` | port scan   |
| `-k` | keep open   |

---

### `dig`

DNS lookup

**Syntax**

```bash
dig [opts] domain
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `+short`  | —              |
| `+noall`  | +answer        |
| `@server` | —              |
| `-t`      | record type    |
| `MX`      | A NS CNAME TXT |
| `+trace`  | full trace     |

---

### `host`

DNS lookup (simple)

**Syntax**

```bash
host domain
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | record type |
| `-v` | verbose     |
| `-a` | all info    |

---

### `nslookup`

Interactive DNS

**Syntax**

```bash
nslookup domain
```

---

### `resolvectl`

Resolve DNS (systemd)

**Syntax**

```bash
resolvectl query domain
```

**Options**

| Flag     | Description       |
| -------- | ----------------- |
| `status` | flush-caches      |
| `dns`    | domain statistics |

---

### `arp`

ARP table

**Syntax**

```bash
arp [opts]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-a` | show all     |
| `-d` | delete entry |
| `-s` | add entry    |

---

### `ethtool`

Ethernet driver info

**Syntax**

```bash
ethtool iface
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `-i`      | driver      |
| `-S`      | statistics  |
| `-g`      | ring params |
| `--speed` | —           |

---

### `iwconfig`

Wireless config

**Syntax**

```bash
iwconfig [iface]
```

---

### `nmcli`

NetworkManager CLI

**Syntax**

```bash
nmcli [opts] obj cmd
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `device`     | wifi list   |
| `connection` | up/down     |
| `general`    | status      |
| `con`        | show        |

---

### `tcpdump`

Capture packets

**Syntax**

```bash
tcpdump [opts]
```

**Options**

| Flag   | Description |
| ------ | ----------- |
| `-i`   | interface   |
| `-n`   | no DNS      |
| `-v`   | verbose     |
| `-w`   | write pcap  |
| `-r`   | read pcap   |
| `port` | filter      |
| `-c`   | count       |
| `-X`   | hex+ASCII   |

---

### `iperf3`

Network bandwidth test

**Syntax**

```bash
iperf3 -s / -c host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | port        |
| `-t` | duration    |
| `-u` | UDP         |
| `-b` | bandwidth   |
| `-P` | parallel    |

---

### `telnet`

Telnet / port test

**Syntax**

```bash
telnet host port
```

---

### `openssl`

SSL/TLS toolkit

**Syntax**

```bash
openssl [cmd]
```

**Options**

| Flag       | Description     |
| ---------- | --------------- |
| `s_client` | -connect        |
| `req`      | -new cert       |
| `x509`     | -text           |
| `genrsa`   | private key     |
| `enc`      | encrypt/decrypt |

---

### `sshkeygen`

SSH key generation

**Syntax**

```bash
ssh-keygen [opts]
```

**Options**

| Flag | Description        |
| ---- | ------------------ |
| `-t` | type (rsa ed25519) |
| `-b` | bits               |
| `-f` | file               |
| `-C` | comment            |

---

### `nftables/nft`

Modern firewall

**Syntax**

```bash
nft [cmd]
```

**Options**

| Flag     | Description      |
| -------- | ---------------- |
| `list`   | ruleset          |
| `add`    | table/chain/rule |
| `delete` | —                |
| `flush`  | ruleset          |

---

## Disk

### `df`

Disk space (filesystems)

**Syntax**

```bash
df [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-h` | human       |
| `-T` | fs type     |
| `-i` | inodes      |
| `-a` | all         |

---

### `du`

Disk usage (dirs)

**Syntax**

```bash
du [opts] path
```

**Options**

| Flag          | Description |
| ------------- | ----------- |
| `-s`          | summary     |
| `-h`          | human       |
| `-a`          | all files   |
| `-c`          | total       |
| `--max-depth` | N           |
| `-x`          | one fs      |

---

### `lsblk`

List block devices

**Syntax**

```bash
lsblk [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | filesystem  |
| `-o` | columns     |
| `-a` | all         |
| `-m` | permissions |
| `-t` | topology    |

---

### `blkid`

Block device attributes

**Syntax**

```bash
blkid [dev]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-t` | search          |
| `-o` | format          |
| `-p` | low-level probe |

---

### `fdisk`

Partition manager (MBR)

**Syntax**

```bash
fdisk [opts] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | list        |
| `-n` | new         |
| `-d` | delete      |
| `-t` | type        |
| `-p` | print       |

---

### `gdisk`

Partition manager (GPT)

**Syntax**

```bash
gdisk dev
```

---

### `parted`

Partition manager

**Syntax**

```bash
parted [dev]
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `print`      | mkpart rm   |
| `resizepart` | align-check |
| `unit`       | MB/GB/TiB   |

---

### `mkfs`

Create filesystem

**Syntax**

```bash
mkfs -t type dev
```

**Options**

| Flag   | Description     |
| ------ | --------------- |
| `ext4` | xfs btrfs fat32 |
| `ntfs` | f2fs            |
| `-L`   | label           |

---

### `mkswap`

Make swap space

**Syntax**

```bash
mkswap dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-L` | label       |

---

### `swapon`

Enable swap

**Syntax**

```bash
swapon dev
```

**Options**

| Flag    | Description |
| ------- | ----------- |
| `--all` | —           |
| `-s`    | show swap   |
| `-p`    | priority    |

---

### `swapoff`

Disable swap

**Syntax**

```bash
swapoff dev
```

**Options**

| Flag    | Description |
| ------- | ----------- |
| `--all` | —           |

---

### `mount`

Mount filesystem

**Syntax**

```bash
mount [opts] dev mnt
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `-t`     | type        |
| `-o`     | options     |
| `-a`     | fstab       |
| `--bind` | rebind      |

---

### `umount`

Unmount filesystem

**Syntax**

```bash
umount dev|mnt
```

**Options**

| Flag | Description       |
| ---- | ----------------- |
| `-l` | lazy              |
| `-f` | force             |
| `-r` | read-only on fail |

---

### `fsck`

Check/repair filesystem

**Syntax**

```bash
fsck [opts] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | auto repair |
| `-y` | yes to all  |
| `-t` | type        |
| `-n` | no write    |

---

### `e2fsck`

ext2/3/4 fsck

**Syntax**

```bash
e2fsck [opts] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | force       |
| `-y` | auto yes    |
| `-b` | superblock  |

---

### `tune2fs`

Tune ext filesystem

**Syntax**

```bash
tune2fs [opts] dev
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-L` | label        |
| `-i` | interval     |
| `-c` | max mounts   |
| `-m` | reserved pct |

---

### `xfs_repair`

Repair XFS filesystem

**Syntax**

```bash
xfs_repair dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | no modify   |

---

### `dd`

Raw copy (convert/copy)

**Syntax**

```bash
dd if=src of=dst
```

**Options**

| Flag                | Description |
| ------------------- | ----------- |
| `bs=`               | block size  |
| `count=`            | blocks      |
| `skip=`             | skip blocks |
| `status=progress`   | —           |
| `conv=sync,noerror` | —           |

---

### `sync`

Flush filesystem buffers

**Syntax**

```bash
sync
```

---

### `hdparm`

Hard disk parameters

**Syntax**

```bash
hdparm [opts] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-I` | identity    |
| `-t` | read timing |
| `-W` | cache       |
| `-S` | standby     |

---

### `smartctl`

SMART disk health

**Syntax**

```bash
smartctl [opts] dev
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all info    |
| `-H` | health      |
| `-t` | test type   |
| `-l` | log         |

---

### `cryptsetup`

LUKS encryption

**Syntax**

```bash
cryptsetup [cmd] dev
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `luksFormat` | luksOpen    |
| `luksClose`  | luksDump    |
| `status`     | resize      |

---

### `pvs/vgs/lvs`

LVM list PV/VG/LV

**Syntax**

```bash
pvs  vgs  lvs
```

---

### `lvcreate`

Create LVM volume

**Syntax**

```bash
lvcreate -n name -L size VG
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-L` | size        |
| `-l` | extents     |
| `-s` | snapshot    |

---

## Users & Groups

### `whoami`

Current username

**Syntax**

```bash
whoami
```

---

### `id`

User and group IDs

**Syntax**

```bash
id [user]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-u` | UID only        |
| `-g` | GID only        |
| `-G` | all groups      |
| `-n` | name not number |

---

### `w`

Who is logged in + activity

**Syntax**

```bash
w [user]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-h` | no header    |
| `-s` | short format |

---

### `who`

Who is logged in

**Syntax**

```bash
who [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all info    |
| `-H` | headers     |
| `-b` | last boot   |
| `-r` | runlevel    |

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
| `-F` | full dates     |
| `-i` | show IP        |

---

### `lastb`

Failed login attempts

**Syntax**

```bash
lastb
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | lines       |
| `-F` | full dates  |

---

### `lastlog`

Last login of all users

**Syntax**

```bash
lastlog
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | user        |
| `-t` | days        |

---

### `users`

Logged-in users

**Syntax**

```bash
users
```

---

### `sudo`

Run as superuser

**Syntax**

```bash
sudo [opts] cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | user        |
| `-i` | login shell |
| `-l` | list perms  |
| `-k` | invalidate  |
| `-s` | shell       |
| `-e` | edit files  |

---

### `su`

Switch user

**Syntax**

```bash
su [opts] [user]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-`  | login shell |
| `-c` | run cmd     |
| `-s` | shell       |

---

### `useradd`

Add user

**Syntax**

```bash
useradd [opts] user
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-m` | home dir    |
| `-s` | shell       |
| `-G` | groups      |
| `-c` | comment     |
| `-e` | expiry      |
| `-u` | UID         |

---

### `usermod`

Modify user

**Syntax**

```bash
usermod [opts] user
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `-aG` | add to group |
| `-l`  | rename       |
| `-s`  | shell        |
| `-d`  | home         |
| `-L`  | lock         |
| `-U`  | unlock       |

---

### `userdel`

Delete user

**Syntax**

```bash
userdel [opts] user
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | remove home |
| `-f` | force       |

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
| `-d` | delete      |
| `-S` | status      |

---

### `chpasswd`

Batch password change

**Syntax**

```bash
chpasswd < file
```

---

### `groupadd`

Create group

**Syntax**

```bash
groupadd [opts] group
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-g` | GID          |
| `-r` | system group |

---

### `groupmod`

Modify group

**Syntax**

```bash
groupmod [opts] group
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | rename      |
| `-g` | GID         |

---

### `groupdel`

Delete group

**Syntax**

```bash
groupdel group
```

---

### `gpasswd`

Manage group passwords

**Syntax**

```bash
gpasswd [opts] group
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | add user    |
| `-d` | remove user |
| `-M` | set members |
| `-A` | set admins  |

---

### `groups`

List user groups

**Syntax**

```bash
groups [user]
```

---

### `newgrp`

Log in to new group

**Syntax**

```bash
newgrp group
```

---

### `visudo`

Edit sudoers safely

**Syntax**

```bash
visudo
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | file        |
| `-c` | check only  |

---

### `getent`

Get entries from databases

**Syntax**

```bash
getent passwd|group|hosts name
```

---

## Permissions

### `chmod`

Change permissions

**Syntax**

```bash
chmod [opts] mode file
```

**Options**

| Flag          | Description |
| ------------- | ----------- |
| `-R`          | recursive   |
| `u/g/o/a`     | targets     |
| `+/-/=`       | operators   |
| `r/w/x/X/s/t` | bits        |
| `numeric`     | e.g. 755    |

---

### `chown`

Change owner

**Syntax**

```bash
chown user:group file
```

**Options**

| Flag          | Description    |
| ------------- | -------------- |
| `-R`          | recursive      |
| `-L`          | follow links   |
| `--reference` | copy from file |

---

### `chgrp`

Change group

**Syntax**

```bash
chgrp group file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-R` | recursive   |

---

### `umask`

Set default permissions

**Syntax**

```bash
umask [mode]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-S` | symbolic    |

---

### `getfacl`

Get ACL

**Syntax**

```bash
getfacl file
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-R` | recursive      |
| `-n` | numeric        |
| `-p` | absolute names |

---

### `setfacl`

Set ACL

**Syntax**

```bash
setfacl [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-m` | modify      |
| `-x` | remove      |
| `-b` | clear       |
| `-R` | recursive   |
| `-d` | default ACL |

---

### `chattr`

Change file attributes

**Syntax**

```bash
chattr [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `+i` | immutable   |
| `+a` | append only |
| `-R` | recursive   |
| `-v` | version     |

---

### `lsattr`

List file attributes

**Syntax**

```bash
lsattr [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-R` | recursive   |
| `-a` | all         |
| `-d` | dirs        |

---

### `getfattr`

Get extended attributes

**Syntax**

```bash
getfattr -n attr file
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `--dump` | all         |
| `-n`     | name        |

---

### `setfattr`

Set extended attributes

**Syntax**

```bash
setfattr -n attr -v val file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | name        |
| `-v` | value       |
| `-x` | remove      |

---

## System Info

### `uname`

Kernel / system info

**Syntax**

```bash
uname [opts]
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-a` | all            |
| `-r` | kernel release |
| `-m` | machine        |
| `-n` | hostname       |
| `-v` | kernel version |
| `-s` | kernel name    |

---

### `hostname`

Show / set hostname

**Syntax**

```bash
hostname [name]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-I` | show IPs    |
| `-f` | FQDN        |
| `-s` | short       |

---

### `hostnamectl`

systemd hostname control

**Syntax**

```bash
hostnamectl [cmd]
```

**Options**

| Flag            | Description  |
| --------------- | ------------ |
| `status`        | set-hostname |
| `set-icon-name` | set-chassis  |

---

### `uptime`

System uptime & load

**Syntax**

```bash
uptime
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | pretty      |
| `-s` | since       |

---

### `date`

Date and time

**Syntax**

```bash
date [opts] [+fmt]
```

**Options**

| Flag        | Description |
| ----------- | ----------- |
| `-u`        | UTC         |
| `-s`        | set date    |
| `-R`        | RFC 2822    |
| `+%Y-%m-%d` | +%s unix    |

---

### `timedatectl`

Time/date control

**Syntax**

```bash
timedatectl [cmd]
```

**Options**

| Flag             | Description |
| ---------------- | ----------- |
| `status`         | set-time    |
| `set-timezone`   | —           |
| `list-timezones` | —           |
| `set-ntp`        | —           |

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
| `-j` | julian days  |

---

### `locale`

Locale settings

**Syntax**

```bash
locale [opts]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-a` | all locales  |
| `-m` | all charmaps |

---

### `lshw`

Hardware info

**Syntax**

```bash
lshw [opts]
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `-short` | summary     |
| `-class` | filter      |
| `-json`  | output      |
| `-html`  | output      |
| `-quiet` | no prompt   |

---

### `lscpu`

CPU architecture

**Syntax**

```bash
lscpu
```

**Options**

| Flag | Description           |
| ---- | --------------------- |
| `-e` | extended              |
| `-a` | all including offline |
| `-J` | JSON output           |

---

### `lspci`

PCI devices

**Syntax**

```bash
lspci [opts]
```

**Options**

| Flag  | Description   |
| ----- | ------------- |
| `-v`  | verbose       |
| `-k`  | kernel driver |
| `-nn` | show codes    |
| `-t`  | tree          |

---

### `lsusb`

USB devices

**Syntax**

```bash
lsusb [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-v` | verbose     |
| `-t` | tree        |
| `-s` | bus:dev     |

---

### `dmidecode`

DMI/SMBIOS hardware info

**Syntax**

```bash
dmidecode [opts]
```

**Options**

| Flag | Description         |
| ---- | ------------------- |
| `-t` | type (bios mem sys) |
| `-s` | string              |
| `-q` | quiet               |

---

### `hwinfo`

Detailed hardware info

**Syntax**

```bash
hwinfo [opts]
```

**Options**

| Flag      | Description  |
| --------- | ------------ |
| `--short` | --all        |
| `--cpu`   | --disk --net |

---

### `inxi`

System information

**Syntax**

```bash
inxi [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-F` | full        |
| `-G` | graphics    |
| `-N` | network     |
| `-D` | disk        |
| `-C` | CPU         |

---

### `arch`

Machine architecture

**Syntax**

```bash
arch
```

---

### `nproc`

Number of processors

**Syntax**

```bash
nproc
```

**Options**

| Flag    | Description |
| ------- | ----------- |
| `--all` | all CPUs    |

---

### `getconf`

System configuration

**Syntax**

```bash
getconf LONG_BIT
```

---

## Services

### `systemctl`

Manage systemd services

**Syntax**

```bash
systemctl [cmd] [unit]
```

**Options**

| Flag            | Description    |
| --------------- | -------------- |
| `start`         | stop restart   |
| `status`        | enable disable |
| `list-units`    | list-sockets   |
| `daemon-reload` | —              |
| `is-active`     | is-enabled     |
| `mask`          | unmask isolate |

---

### `journalctl`

Query systemd journal

**Syntax**

```bash
journalctl [opts]
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `-u`           | unit        |
| `-f`           | follow      |
| `-b`           | this boot   |
| `-k`           | kernel      |
| `-n`           | lines       |
| `--since`      | date        |
| `--until`      | date        |
| `-p`           | priority    |
| `-o`           | json        |
| `--disk-usage` | —           |
| `--rotate`     | —           |

---

### `service`

Init.d service control

**Syntax**

```bash
service name cmd
```

**Options**

| Flag     | Description  |
| -------- | ------------ |
| `start`  | stop restart |
| `status` | reload       |

---

### `chkconfig`

Manage service autostart

**Syntax**

```bash
chkconfig name on|off
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `--list`  | —           |
| `--level` | —           |

---

### `update-rc.d`

Manage init scripts

**Syntax**

```bash
update-rc.d name defaults
```

**Options**

| Flag     | Description    |
| -------- | -------------- |
| `remove` | disable enable |

---

### `loginctl`

Login session control

**Syntax**

```bash
loginctl [cmd]
```

**Options**

| Flag                | Description  |
| ------------------- | ------------ |
| `list-sessions`     | —            |
| `list-users`        | list-seats   |
| `terminate-session` | lock-session |

---

### `runlevel`

Current runlevel

**Syntax**

```bash
runlevel
```

---

### `telinit`

Change runlevel

**Syntax**

```bash
telinit N
```

---

### `systemd-analyze`

Boot performance

**Syntax**

```bash
systemd-analyze [cmd]
```

**Options**

| Flag     | Description          |
| -------- | -------------------- |
| `time`   | blame critical-chain |
| `plot`   | > boot.svg           |
| `verify` | unit file            |

---

## Kernel & Modules

### `lsmod`

List loaded modules

**Syntax**

```bash
lsmod
```

---

### `modinfo`

Module information

**Syntax**

```bash
modinfo module
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | description |
| `-a` | author      |
| `-p` | parameters  |

---

### `insmod`

Insert kernel module

**Syntax**

```bash
insmod module.ko
```

---

### `rmmod`

Remove kernel module

**Syntax**

```bash
rmmod module
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | force       |
| `-v` | verbose     |

---

### `modprobe`

Add/remove with deps

**Syntax**

```bash
modprobe [opts] module
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | remove      |
| `-n` | dry run     |
| `-v` | verbose     |
| `-a` | all         |
| `-l` | list        |

---

### `depmod`

Dependency file for modules

**Syntax**

```bash
depmod
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all         |
| `-n` | no write    |
| `-v` | verbose     |

---

### `dmesg`

Kernel ring buffer

**Syntax**

```bash
dmesg [opts]
```

**Options**

| Flag       | Description    |
| ---------- | -------------- |
| `-H`       | human readable |
| `-T`       | timestamps     |
| `-l`       | log level      |
| `-f`       | facility       |
| `--follow` | -w             |
| `--clear`  | —              |

---

### `sysctl`

Kernel parameters

**Syntax**

```bash
sysctl [opts] key
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `-a`       | all         |
| `-w`       | set value   |
| `-p`       | load file   |
| `-n`       | value only  |
| `--system` | —           |

---

### `kexec`

Load new kernel

**Syntax**

```bash
kexec [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | load        |
| `-e` | execute     |

---

### `udevadm`

Udev management

**Syntax**

```bash
udevadm [cmd]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `info`    | trigger     |
| `monitor` | settle      |
| `test`    | device      |

---

## Memory

### `free`

Memory usage

**Syntax**

```bash
free [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-h` | human       |
| `-m` | MB          |
| `-g` | GB          |
| `-s` | interval    |
| `-t` | total       |
| `-w` | wide        |

---

### `vmstat`

Virtual memory stats

**Syntax**

```bash
vmstat [interval]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-s` | summary         |
| `-d` | disk            |
| `-p` | partition       |
| `-a` | active/inactive |
| `-S` | units           |

---

### `pmap`

Process memory map

**Syntax**

```bash
pmap PID
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-x` | extended    |
| `-d` | device      |
| `-q` | quiet       |

---

### `slabtop`

Kernel slab caches

**Syntax**

```bash
slabtop
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | delay       |
| `-s` | sort        |
| `-o` | once        |

---

### `smem`

Per-process memory

**Syntax**

```bash
smem [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | by RSS      |
| `-p` | percent     |
| `-u` | user        |

---

### `numactl`

NUMA topology

**Syntax**

```bash
numactl [opts] cmd
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `--hardware`   | —           |
| `--interleave` | —           |
| `--membind`    | node        |

---

### `sync; echo 3 > /proc/sys/vm/drop_caches`

Drop page/slab caches

---

## Monitoring

### `iotop`

I/O by process

**Syntax**

```bash
iotop
```

**Options**

| Flag | Description    |
| ---- | -------------- |
| `-o` | only active    |
| `-a` | accumulated    |
| `-P` | processes only |
| `-u` | user           |
| `-d` | delay          |

---

### `iostat`

CPU and I/O stats

**Syntax**

```bash
iostat [opts] [interval]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-x` | extended    |
| `-d` | device      |
| `-c` | CPU         |
| `-h` | human       |
| `-m` | MB/s        |

---

### `mpstat`

Per-CPU stats

**Syntax**

```bash
mpstat [opts] [interval]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-P` | ALL per CPU |
| `-u` | utilization |
| `-I` | interrupt   |

---

### `sar`

System activity reporter

**Syntax**

```bash
sar [opts] [interval]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | CPU         |
| `-r` | memory      |
| `-d` | disk        |
| `-n` | net         |
| `-b` | I/O         |
| `-q` | load        |
| `-f` | file        |

---

### `perf`

Performance analysis

**Syntax**

```bash
perf [cmd]
```

**Options**

| Flag   | Description   |
| ------ | ------------- |
| `stat` | record report |
| `top`  | annotate      |
| `list` | events script |

---

### `lsof`

Open files per process

**Syntax**

```bash
lsof [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-u` | user        |
| `-p` | PID         |
| `-i` | network     |
| `-c` | cmd         |
| `+d` | dir         |
| `-t` | terse PIDs  |

---

### `atop`

Advanced system monitor

**Syntax**

```bash
atop
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-d` | interval      |
| `-r` | playback file |
| `-w` | write log     |

---

### `glances`

System overview tool

**Syntax**

```bash
glances
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-w` | web server  |
| `-c` | client      |
| `-t` | interval    |

---

### `nethogs`

Bandwidth by process

**Syntax**

```bash
nethogs [iface]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-d` | delay       |
| `-p` | promisc     |

---

### `bmon`

Bandwidth monitor

**Syntax**

```bash
bmon
```

---

### `nload`

Real-time bandwidth

**Syntax**

```bash
nload [iface]
```

---

### `dstat`

System stats combined

**Syntax**

```bash
dstat [opts]
```

**Options**

| Flag        | Description |
| ----------- | ----------- |
| `-c`        | CPU         |
| `-d`        | disk        |
| `-n`        | net         |
| `-m`        | mem         |
| `-p`        | paging      |
| `-s`        | swap        |
| `--top-cpu` | —           |
| `--full`    | —           |

---

### `sysdig`

Deep system tracing

**Syntax**

```bash
sysdig [filter]
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `-c`  | chisel       |
| `-w`  | write        |
| `-r`  | read         |
| `-cl` | list chisels |

---

## Package Mgmt

### `apt`

Debian/Ubuntu packages

**Syntax**

```bash
apt [cmd] [pkg]
```

**Options**

| Flag         | Description          |
| ------------ | -------------------- |
| `install`    | remove purge         |
| `update`     | upgrade full-upgrade |
| `search`     | show list            |
| `autoremove` | autoclean            |
| `depends`    | rdepends             |

---

### `apt-get`

APT low-level tool

**Syntax**

```bash
apt-get [cmd] [pkg]
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `install`      | remove      |
| `update`       | upgrade     |
| `dist-upgrade` | build-dep   |
| `-y`           | auto yes    |
| `-s`           | simulate    |

---

### `apt-cache`

Query APT cache

**Syntax**

```bash
apt-cache [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `search`  | show policy |
| `depends` | rdepends    |
| `dump`    | stats       |

---

### `dpkg`

Debian package tool

**Syntax**

```bash
dpkg [opts] pkg
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-i` | install .deb |
| `-r` | remove       |
| `-P` | purge        |
| `-l` | list         |
| `-s` | status       |
| `-L` | list files   |
| `-S` | find owner   |

---

### `snap`

Snap packages

**Syntax**

```bash
snap [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | remove      |
| `list`    | refresh     |
| `find`    | info        |
| `run`     | connect     |

---

### `flatpak`

Flatpak packages

**Syntax**

```bash
flatpak [cmd] [pkg]
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `install`    | uninstall   |
| `list`       | update run  |
| `remote-add` | remote-list |

---

### `yum`

RPM package manager

**Syntax**

```bash
yum [cmd] [pkg]
```

**Options**

| Flag       | Description  |
| ---------- | ------------ |
| `install`  | remove       |
| `update`   | check-update |
| `search`   | info list    |
| `repolist` | groupinstall |

---

### `dnf`

Fedora/RHEL packages

**Syntax**

```bash
dnf [cmd] [pkg]
```

**Options**

| Flag             | Description |
| ---------------- | ----------- |
| `install`        | remove      |
| `update`         | search      |
| `autoremove`     | history     |
| `module`         | group       |
| `config-manager` | —           |

---

### `rpm`

RPM package tool

**Syntax**

```bash
rpm [opts] pkg
```

**Options**

| Flag  | Description |
| ----- | ----------- |
| `-i`  | install     |
| `-U`  | upgrade     |
| `-e`  | erase       |
| `-q`  | query       |
| `-V`  | verify      |
| `-qa` | list all    |
| `-ql` | list files  |

---

### `pacman`

Arch Linux packages

**Syntax**

```bash
pacman [opts] [pkg]
```

**Options**

| Flag   | Description  |
| ------ | ------------ |
| `-S`   | install      |
| `-R`   | remove       |
| `-U`   | upgrade file |
| `-Ss`  | search       |
| `-Q`   | installed    |
| `-Si`  | info         |
| `-Syu` | full upgrade |

---

### `zypper`

OpenSUSE packages

**Syntax**

```bash
zypper [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | remove      |
| `refresh` | update      |
| `search`  | info        |
| `repos`   | addrepo     |

---

### `pip`

Python packages

**Syntax**

```bash
pip [cmd] pkg
```

**Options**

| Flag      | Description         |
| --------- | ------------------- |
| `install` | uninstall           |
| `freeze`  | list                |
| `show`    | search              |
| `install` | -r requirements.txt |
| `install` | -e editable         |

---

### `pip3`

Python 3 pip

**Syntax**

```bash
pip3 [cmd] pkg
```

---

### `npm`

Node packages

**Syntax**

```bash
npm [cmd] [pkg]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `install` | uninstall   |
| `update`  | list        |
| `run`     | init        |
| `publish` | audit       |
| `ci`      | link        |

---

### `cargo`

Rust packages

**Syntax**

```bash
cargo [cmd]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `build`   | run test    |
| `install` | update      |
| `search`  | publish     |
| `doc`     | check fmt   |
| `clippy`  | bench       |

---

## SSH & Remote

### `ssh`

Secure shell login

**Syntax**

```bash
ssh [opts] user@host
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-p` | port          |
| `-i` | key           |
| `-L` | local fwd     |
| `-R` | remote fwd    |
| `-D` | dynamic/SOCKS |
| `-N` | no cmd        |
| `-f` | background    |
| `-v` | verbose       |
| `-J` | jump host     |
| `-X` | X11           |

---

### `ssh-keygen`

Generate SSH key

**Syntax**

```bash
ssh-keygen [opts]
```

**Options**

| Flag | Description        |
| ---- | ------------------ |
| `-t` | type (ed25519 rsa) |
| `-b` | bits               |
| `-f` | file               |
| `-C` | comment            |
| `-N` | passphrase         |
| `-p` | change passphrase  |

---

### `ssh-copy-id`

Install public key

**Syntax**

```bash
ssh-copy-id user@host
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-i` | key file    |
| `-p` | port        |

---

### `ssh-add`

Add key to agent

**Syntax**

```bash
ssh-add [key]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | list        |
| `-D` | delete all  |
| `-t` | lifetime    |
| `-k` | PKCS11      |

---

### `ssh-agent`

SSH authentication agent

**Syntax**

```bash
eval $(ssh-agent)
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-k` | kill agent  |

---

### `scp`

Secure copy

**Syntax**

```bash
scp [opts] src user@host:dst
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | recursive   |
| `-P` | port        |
| `-i` | key         |
| `-p` | preserve    |
| `-C` | compress    |
| `-3` | via local   |

---

### `sftp`

Secure FTP

**Syntax**

```bash
sftp user@host
```

**Options**

| Flag  | Description |
| ----- | ----------- |
| `-P`  | port        |
| `-i`  | key         |
| `get` | put ls cd   |

---

### `rsync`

Remote file sync

**Syntax**

```bash
rsync [opts] src dst
```

**Options**

| Flag        | Description      |
| ----------- | ---------------- |
| `-a`        | archive          |
| `-v`        | verbose          |
| `-z`        | compress         |
| `-n`        | dry run          |
| `--delete`  | —                |
| `--exclude` | —                |
| `--bwlimit` | —                |
| `-e`        | ssh              |
| `-P`        | progress+partial |

---

### `sshfs`

Mount remote fs over SSH

**Syntax**

```bash
sshfs user@host:path mnt
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `-p`         | port        |
| `-o`         | opts        |
| `fusermount` | -u unmount  |

---

### `tmux`

Terminal multiplexer

**Syntax**

```bash
tmux [cmd]
```

**Options**

| Flag     | Description  |
| -------- | ------------ |
| `new`    | -s name      |
| `attach` | -t name      |
| `ls`     | kill-session |
| `C-b`    | d detach     |
| `C-b`    | c new window |
| `C-b`    | % split v    |
| `C-b`    | " split h    |

---

### `screen`

Terminal multiplexer

**Syntax**

```bash
screen [opts]
```

**Options**

| Flag  | Description  |
| ----- | ------------ |
| `-S`  | name         |
| `-r`  | reattach     |
| `-ls` | list         |
| `C-a` | d detach     |
| `C-a` | c new window |

---

## Firewall

### `ufw`

Uncomplicated firewall

**Syntax**

```bash
ufw [cmd]
```

**Options**

| Flag      | Description      |
| --------- | ---------------- |
| `enable`  | disable reset    |
| `allow`   | deny reject port |
| `allow`   | from IP          |
| `status`  | verbose numbered |
| `delete`  | N                |
| `default` | policy           |
| `logging` | —                |

---

### `iptables`

IPv4 firewall rules

**Syntax**

```bash
iptables [opts]
```

**Options**

| Flag | Description                 |
| ---- | --------------------------- |
| `-L` | list                        |
| `-A` | append                      |
| `-I` | insert                      |
| `-D` | delete                      |
| `-F` | flush                       |
| `-P` | policy                      |
| `-n` | numeric                     |
| `-t` | table (nat mangle)          |
| `-j` | target (ACCEPT DROP REJECT) |

---

### `ip6tables`

IPv6 firewall rules

**Syntax**

```bash
ip6tables [opts]
```

**Options**

| Flag   | Description |
| ------ | ----------- |
| `same` | as iptables |

---

### `nft`

nftables (modern)

**Syntax**

```bash
nft [cmd]
```

**Options**

| Flag      | Description      |
| --------- | ---------------- |
| `list`    | ruleset          |
| `add`     | table/chain/rule |
| `delete`  | flush ruleset    |
| `monitor` | -f script        |

---

### `firewalld`

Dynamic firewall

**Syntax**

```bash
firewall-cmd [opts]
```

**Options**

| Flag            | Description |
| --------------- | ----------- |
| `--list-all`    | —           |
| `--add-service` | —           |
| `--add-port`    | —           |
| `--reload`      | —           |
| `--zone`        | —           |
| `--permanent`   | —           |
| `--state`       | —           |

---

### `fail2ban`

Ban repeated failures

**Syntax**

```bash
fail2ban-client [cmd]
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `status` | start stop  |
| `status` | jailname    |
| `set`    | jail banip  |
| `unban`  | IP          |

---

## Containers

### `docker`

Container management

**Syntax**

```bash
docker [cmd]
```

**Options**

| Flag     | Description    |
| -------- | -------------- |
| `run`    | exec ps stop   |
| `kill`   | rm rmi         |
| `build`  | pull push      |
| `images` | volume network |
| `logs`   | inspect stats  |
| `cp`     | commit tag     |

---

### `docker-compose`

Multi-container apps

**Syntax**

```bash
docker-compose [cmd]
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `up`     | -d down     |
| `build`  | pull        |
| `logs`   | -f          |
| `exec`   | run         |
| `ps`     | restart     |
| `config` | scale       |

---

### `docker compose`

Docker Compose v2

**Syntax**

```bash
docker compose [cmd]
```

**Options**

| Flag   | Description       |
| ------ | ----------------- |
| `same` | as docker-compose |

---

### `podman`

Daemonless containers

**Syntax**

```bash
podman [cmd]
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `run`      | exec ps     |
| `build`    | pull push   |
| `volume`   | network pod |
| `generate` | systemd     |

---

### `kubectl`

Kubernetes CLI

**Syntax**

```bash
kubectl [cmd] [resource]
```

**Options**

| Flag      | Description       |
| --------- | ----------------- |
| `get`     | describe delete   |
| `apply`   | -f create         |
| `logs`    | exec port-forward |
| `rollout` | scale             |
| `config`  | namespace         |
| `top`     | events cordon     |

---

### `crictl`

Container runtime tool

**Syntax**

```bash
crictl [cmd]
```

**Options**

| Flag    | Description  |
| ------- | ------------ |
| `ps`    | pods images  |
| `exec`  | logs inspect |
| `start` | stop rm      |
| `pull`  | rmi          |

---

## Git

### `git init`

Create repository

**Syntax**

```bash
git init [dir]
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `--bare` | server repo |

---

### `git clone`

Clone repository

**Syntax**

```bash
git clone URL [dir]
```

**Options**

| Flag                   | Description |
| ---------------------- | ----------- |
| `--depth`              | N shallow   |
| `--branch`             | name        |
| `--recurse-submodules` | —           |
| `--single-branch`      | —           |

---

### `git status`

Working tree status

**Syntax**

```bash
git status
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | short       |
| `-b` | branch      |
| `-u` | untracked   |

---

### `git add`

Stage changes

**Syntax**

```bash
git add [file|.]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-A` | all          |
| `-p` | interactive  |
| `-u` | tracked only |

---

### `git commit`

Record changes

**Syntax**

```bash
git commit [opts]
```

**Options**

| Flag      | Description    |
| --------- | -------------- |
| `-m`      | message        |
| `-a`      | stage modified |
| `-v`      | verbose        |
| `--amend` | rewrite last   |

---

### `git push`

Upload to remote

**Syntax**

```bash
git push [remote] [branch]
```

**Options**

| Flag        | Description          |
| ----------- | -------------------- |
| `-u`        | set upstream         |
| `-f`        | force                |
| `--tags`    | —                    |
| `-d`        | delete remote branch |
| `--dry-run` | —                    |

---

### `git pull`

Fetch + merge

**Syntax**

```bash
git pull [remote] [branch]
```

**Options**

| Flag       | Description       |
| ---------- | ----------------- |
| `--rebase` | —                 |
| `-ff`      | fast-forward only |
| `--all`    | all remotes       |

---

### `git fetch`

Download from remote

**Syntax**

```bash
git fetch [remote]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `--all`   | remotes     |
| `--prune` | —           |
| `--tags`  | —           |

---

### `git branch`

List / manage branches

**Syntax**

```bash
git branch [opts] [name]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-a` | all          |
| `-r` | remote       |
| `-d` | delete       |
| `-D` | force delete |
| `-m` | rename       |
| `-v` | verbose      |

---

### `git checkout`

Switch branches/restore

**Syntax**

```bash
git checkout [branch|file]
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-b` | create+switch   |
| `--` | file restore    |
| `-t` | tracking remote |

---

### `git switch`

Switch branches

**Syntax**

```bash
git switch [branch]
```

**Options**

| Flag       | Description  |
| ---------- | ------------ |
| `-c`       | create       |
| `-d`       | detach       |
| `--orphan` | empty branch |

---

### `git merge`

Merge branches

**Syntax**

```bash
git merge [branch]
```

**Options**

| Flag         | Description        |
| ------------ | ------------------ |
| `--no-ff`    | force merge commit |
| `--squash`   | --abort            |
| `--strategy` | —                  |

---

### `git rebase`

Rebase commits

**Syntax**

```bash
git rebase [branch|opts]
```

**Options**

| Flag           | Description       |
| -------------- | ----------------- |
| `-i`           | interactive       |
| `--onto`       | —                 |
| `--autosquash` | —                 |
| `--abort`      | --continue --skip |

---

### `git stash`

Shelve changes

**Syntax**

```bash
git stash [cmd]
```

**Options**

| Flag     | Description       |
| -------- | ----------------- |
| `push`   | pop apply         |
| `list`   | drop show         |
| `branch` | clear             |
| `-u`     | include untracked |

---

### `git log`

Commit history

**Syntax**

```bash
git log [opts]
```

**Options**

| Flag        | Description    |
| ----------- | -------------- |
| `--oneline` | --graph        |
| `--all`     | --author       |
| `--since`   | --until        |
| `-n`        | count          |
| `--stat`    | -p diff        |
| `--follow`  | file           |
| `-S`        | search content |

---

### `git diff`

Show changes

**Syntax**

```bash
git diff [opts]
```

**Options**

| Flag               | Description |
| ------------------ | ----------- |
| `--staged`         | cached      |
| `--stat`           | --name-only |
| `HEAD~N`           | previous    |
| `branch1..branch2` | —           |

---

### `git reset`

Undo commits

**Syntax**

```bash
git reset [opts] [commit]
```

**Options**

| Flag      | Description |
| --------- | ----------- |
| `--soft`  | keep staged |
| `--mixed` | unstage     |
| `--hard`  | discard all |

---

### `git revert`

Reverse a commit

**Syntax**

```bash
git revert commit
```

**Options**

| Flag          | Description |
| ------------- | ----------- |
| `--no-commit` | -n          |
| `--mainline`  | M merge     |

---

### `git tag`

Mark release points

**Syntax**

```bash
git tag [opts] name
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `-a`     | annotated   |
| `-m`     | message     |
| `-d`     | delete      |
| `-l`     | list        |
| `--sort` | —           |
| `-v`     | verify      |

---

### `git remote`

Manage remotes

**Syntax**

```bash
git remote [cmd]
```

**Options**

| Flag   | Description   |
| ------ | ------------- |
| `add`  | remove rename |
| `show` | set-url prune |
| `-v`   | verbose       |

---

### `git cherry-pick`

Apply specific commit

**Syntax**

```bash
git cherry-pick commit
```

**Options**

| Flag      | Description  |
| --------- | ------------ |
| `-n`      | no commit    |
| `--abort` | --continue   |
| `--ff`    | fast-forward |

---

### `git bisect`

Binary search bug

**Syntax**

```bash
git bisect start
```

**Options**

| Flag   | Description |
| ------ | ----------- |
| `good` | bad reset   |
| `run`  | cmd auto    |

---

### `git blame`

Per-line last change

**Syntax**

```bash
git blame file
```

**Options**

| Flag | Description       |
| ---- | ----------------- |
| `-L` | from,to lines     |
| `-w` | ignore whitespace |
| `-C` | detect moved      |

---

### `git clean`

Remove untracked files

**Syntax**

```bash
git clean [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | force       |
| `-d` | dirs        |
| `-n` | dry run     |
| `-x` | ignored too |

---

### `git submodule`

Manage submodules

**Syntax**

```bash
git submodule [cmd]
```

**Options**

| Flag          | Description |
| ------------- | ----------- |
| `add`         | update init |
| `foreach`     | status      |
| `--recursive` | —           |

---

### `git worktree`

Multiple working trees

**Syntax**

```bash
git worktree [cmd]
```

**Options**

| Flag    | Description |
| ------- | ----------- |
| `add`   | list remove |
| `prune` | lock        |

---

### `git reflog`

History of HEAD

**Syntax**

```bash
git reflog
```

**Options**

| Flag     | Description |
| -------- | ----------- |
| `expire` | delete      |
| `show`   | --all       |

---

### `git gc`

Garbage collection

**Syntax**

```bash
git gc
```

**Options**

| Flag           | Description |
| -------------- | ----------- |
| `--aggressive` | —           |
| `--auto`       | —           |
| `--prune=date` | —           |

---

## Shell & Scripting

### `bash`

Bourne-again shell

**Syntax**

```bash
bash [opts] [script]
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-c` | command      |
| `-x` | trace        |
| `-n` | syntax check |
| `-v` | verbose      |
| `-i` | interactive  |
| `-l` | login        |

---

### `sh`

POSIX shell

**Syntax**

```bash
sh [opts] [script]
```

---

### `zsh`

Z shell

**Syntax**

```bash
zsh [opts]
```

---

### `echo`

Print to stdout

**Syntax**

```bash
echo [opts] text
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | no newline  |
| `-e` | escapes     |
| `-E` | no escapes  |

---

### `printf`

Formatted print

**Syntax**

```bash
printf format [args]
```

**Options**

| Flag | Description            |
| ---- | ---------------------- |
| `%s` | string %d int %f float |
| `\n` | \t \0 escapes          |

---

### `read`

Read stdin input

**Syntax**

```bash
read [opts] var
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | prompt      |
| `-s` | silent      |
| `-n` | chars       |
| `-t` | timeout     |
| `-a` | array       |
| `-d` | delimiter   |

---

### `source / .`

Run script in current shell

**Syntax**

```bash
source file  |  . file
```

---

### `exec`

Replace shell process

**Syntax**

```bash
exec cmd
```

**Options**

| Flag   | Description    |
| ------ | -------------- |
| `-a`   | name           |
| `exec` | >file redirect |

---

### `eval`

Evaluate and execute

**Syntax**

```bash
eval string
```

---

### `test / [ ]`

Evaluate condition

**Syntax**

```bash
test expr  |  [ expr ]
```

**Options**

| Flag  | Description         |
| ----- | ------------------- |
| `-f`  | file                |
| `-d`  | dir                 |
| `-e`  | exists              |
| `-z`  | empty string        |
| `-n`  | non-empty           |
| `-eq` | -ne -lt -gt compare |

---

### `[[ ]]`

Extended test (bash)

**Syntax**

```bash
[[ expr ]]
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `=~` | regex         |
| `==` | != match      |
| `-z` | -n string     |
| `-f` | -d file tests |

---

### `let`

Arithmetic evaluation

**Syntax**

```bash
let expr
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `var=expr` | —           |
| `++`       | -- += etc   |

---

### `(( ))`

Arithmetic in bash

**Syntax**

```bash
(( expr ))
```

---

### `set`

Set shell options

**Syntax**

```bash
set [opts]
```

**Options**

| Flag       | Description      |
| ---------- | ---------------- |
| `-e`       | exit on error    |
| `-x`       | trace            |
| `-u`       | undefined error  |
| `-o`       | pipefail         |
| `pipefail` | noglob noclobber |

---

### `shopt`

Set bash options

**Syntax**

```bash
shopt [-su] opt
```

**Options**

| Flag         | Description |
| ------------ | ----------- |
| `globstar`   | extglob     |
| `nocaseglob` | direxpand   |
| `histappend` | cdspell     |

---

### `declare`

Declare variables

**Syntax**

```bash
declare [opts] var
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-i` | integer     |
| `-a` | array       |
| `-A` | assoc array |
| `-r` | readonly    |
| `-x` | export      |
| `-f` | functions   |

---

### `local`

Local function variable

**Syntax**

```bash
local var=val
```

---

### `export`

Export variable

**Syntax**

```bash
export VAR=value
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | unexport    |
| `-f` | function    |
| `-p` | print all   |

---

### `unset`

Unset variable

**Syntax**

```bash
unset var
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | function    |
| `-v` | variable    |

---

### `alias`

Create alias

**Syntax**

```bash
alias name='cmd'
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | print all   |

---

### `unalias`

Remove alias

**Syntax**

```bash
unalias name
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | remove all  |

---

### `function`

Define function

**Syntax**

```bash
function name { }
```

---

### `return`

Return from function

**Syntax**

```bash
return [code]
```

---

### `exit`

Exit shell

**Syntax**

```bash
exit [code]
```

---

### `true / false`

Return 0 or 1

**Syntax**

```bash
true  |  false
```

---

### `getopts`

Parse options in scripts

**Syntax**

```bash
getopts optstring var
```

---

### `select`

Generate menu

**Syntax**

```bash
select var in list
```

---

### `mapfile`

Read array from stdin

**Syntax**

```bash
mapfile -t arr < file
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-t` | trim newlines |
| `-n` | lines         |
| `-s` | skip          |

---

### `command`

Run ignoring aliases

**Syntax**

```bash
command cmd
```

**Options**

| Flag | Description  |
| ---- | ------------ |
| `-v` | locate       |
| `-p` | default PATH |
| `-n` | no function  |

---

### `builtin`

Run shell builtin

**Syntax**

```bash
builtin cmd
```

---

### `hash`

Cache command locations

**Syntax**

```bash
hash [cmd]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-r` | reset       |
| `-p` | path        |
| `-l` | list        |

---

### `history`

Command history

**Syntax**

```bash
history [n]
```

**Options**

| Flag   | Description   |
| ------ | ------------- |
| `!!`   | last cmd      |
| `!n`   | run nth       |
| `!str` | last matching |
| `!!`   | last cmd      |
| `-c`   | clear         |
| `-d`   | N delete      |
| `-r`   | read file     |
| `-w`   | write         |

---

### `time`

Time command execution

**Syntax**

```bash
time cmd
```

---

### `watch`

Repeat command

**Syntax**

```bash
watch [opts] cmd
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-n` | interval        |
| `-d` | highlight diffs |
| `-e` | exit on error   |
| `-t` | no header       |
| `-x` | pass to exec    |

---

### `xdg-open`

Open with default app

**Syntax**

```bash
xdg-open file|URL
```

---

### `notify-send`

Desktop notification

**Syntax**

```bash
notify-send title body
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-t` | timeout ms  |
| `-u` | urgency     |
| `-i` | icon        |

---

## Environment

### `env`

Show / run with env

**Syntax**

```bash
env [name=val] cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-i` | empty env   |
| `-u` | unset       |
| `-C` | dir         |
| `--` | end of opts |

---

### `printenv`

Print env variables

**Syntax**

```bash
printenv [var]
```

---

### `locale`

Show locale settings

**Syntax**

```bash
locale [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | all locales |
| `-m` | charmaps    |

---

### `localectl`

Locale/keyboard control

**Syntax**

```bash
localectl [cmd]
```

**Options**

| Flag         | Description  |
| ------------ | ------------ |
| `status`     | set-locale   |
| `set-keymap` | list-locales |

---

### `pathvar`

Manage PATH variable

**Syntax**

```bash
export PATH=$PATH:dir
```

---

### `ldconfig`

Dynamic linker cache

**Syntax**

```bash
ldconfig [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-p` | print cache |
| `-v` | verbose     |
| `-n` | dir update  |

---

### `ldd`

Print shared dependencies

**Syntax**

```bash
ldd [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-v` | verbose     |
| `-r` | resolve     |

---

### `stdbuf`

Modify stream buffering

**Syntax**

```bash
stdbuf [opts] cmd
```

**Options**

| Flag | Description           |
| ---- | --------------------- |
| `-i` | -o -e buffer settings |
| `L`  | line 0 unbuffered     |

---

## Cron & Jobs

### `crontab`

Schedule cron jobs

**Syntax**

```bash
crontab [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-e` | edit        |
| `-l` | list        |
| `-r` | remove      |
| `-u` | user        |

---

### `at`

Run once at time

**Syntax**

```bash
at time
```

**Options**

| Flag  | Description        |
| ----- | ------------------ |
| `-l`  | list jobs          |
| `-d`  | delete             |
| `-c`  | show job           |
| `now` | +5min 3pm midnight |

---

### `atq`

List pending at jobs

**Syntax**

```bash
atq
```

---

### `atrm`

Remove at job

**Syntax**

```bash
atrm jobnum
```

---

### `batch`

Run when load allows

**Syntax**

```bash
batch < script
```

---

### `anacron`

Periodic jobs (days)

**Syntax**

```bash
anacron [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | run now     |
| `-f` | force       |
| `-s` | serial      |

---

### `systemd-run`

Transient systemd unit

**Syntax**

```bash
systemd-run --on-active=T cmd
```

**Options**

| Flag               | Description |
| ------------------ | ----------- |
| `--on-calendar`    | —           |
| `--timer-property` | —           |
| `--unit`           | name        |

---

### `flock`

Lock file for scripts

**Syntax**

```bash
flock lockfile cmd
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-e` | exclusive   |
| `-s` | shared      |
| `-n` | nonblock    |
| `-w` | timeout     |

---

## Misc

### `man`

User manual pages

**Syntax**

```bash
man [section] cmd
```

**Options**

| Flag               | Description         |
| ------------------ | ------------------- |
| `-k`               | keyword search      |
| `-f`               | brief description   |
| `-a`               | all sections        |
| `-P pager`         | set pager           |
| `-w`               | show page path      |
| `--no-hyphenation` | disable hyphenation |

**Sections**

| #   | Content           |
| --- | ----------------- |
| 1   | User commands     |
| 2   | System calls      |
| 3   | Library functions |
| 4   | Device files      |
| 5   | File formats      |
| 6   | Games             |
| 7   | Miscellaneous     |
| 8   | Admin commands    |
| 9   | Kernel routines   |

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
| `h`     | help           |

**Examples**

```bash
man ls                # manual for ls
man 3 printf          # library function, not shell printf
man -k "list files"   # search descriptions
man -f ls             # one-line summary
```

---

### `info`

GNU info pages

**Syntax**

```bash
info [cmd]
```

---

### `help`

Builtin help

**Syntax**

```bash
help [cmd]
```

---

### `tldr`

Simplified man pages

**Syntax**

```bash
tldr cmd
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `--update` | --list      |

---

### `clear`

Clear terminal

**Syntax**

```bash
clear
```

**Options**

| Flag | Description     |
| ---- | --------------- |
| `-x` | keep scrollback |

---

### `reset`

Reset terminal

**Syntax**

```bash
reset
```

---

### `tput`

Terminal control

**Syntax**

```bash
tput [cap]
```

**Options**

| Flag    | Description |
| ------- | ----------- |
| `cols`  | rows clear  |
| `bold`  | sgr0 rev    |
| `setaf` | N setab N   |

---

### `script`

Record terminal session

**Syntax**

```bash
script [opts] [file]
```

**Options**

| Flag | Description      |
| ---- | ---------------- |
| `-a` | append           |
| `-q` | quiet            |
| `-t` | timing           |
| `-e` | record exit code |

---

### `scriptreplay`

Replay terminal recording

**Syntax**

```bash
scriptreplay timing file
```

---

### `factor`

Factorize numbers

**Syntax**

```bash
factor [N]
```

---

### `bc`

Arbitrary precision calc

**Syntax**

```bash
bc [opts]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-l` | math lib    |
| `-q` | quiet       |
| `-i` | interactive |

---

### `expr`

Evaluate expression

**Syntax**

```bash
expr expr
```

**Options**

| Flag | Description                  |
| ---- | ---------------------------- |
| `+`  | - \* / %                     |
| `=`  | != < > <= >=                 |
| `&`  | \| match substr index length |

---

### `seq`

Print number sequence

**Syntax**

```bash
seq [first] [incr] last
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-s` | separator   |
| `-w` | pad zeros   |
| `-f` | format      |

---

### `shuf`

Shuffle lines

**Syntax**

```bash
shuf [opts] [file]
```

**Options**

| Flag | Description   |
| ---- | ------------- |
| `-n` | count         |
| `-e` | input as args |
| `-i` | range         |
| `-r` | repeat        |

---

### `yes`

Repeat string forever

**Syntax**

```bash
yes [string]
```

---

### `sleep`

Delay execution

**Syntax**

```bash
sleep N[smhd]
```

**Options**

| Flag | Description                |
| ---- | -------------------------- |
| `s`  | secs m mins h hours d days |

---

### `wall`

Broadcast message

**Syntax**

```bash
wall message
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-n` | no banner   |

---

### `write`

Message to user

**Syntax**

```bash
write user [tty]
```

---

### `mesg`

Control message perms

**Syntax**

```bash
mesg [y|n]
```

---

### `talk`

Two-way terminal chat

**Syntax**

```bash
talk user@host
```

---

### `nl`

Number lines of file

**Syntax**

```bash
nl [opts] file
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-b` | body type   |
| `-n` | format      |
| `-s` | separator   |
| `-v` | start num   |

---

### `rev`

Reverse lines

**Syntax**

```bash
rev [file]
```

---

### `lolcat`

Colorize output

**Syntax**

```bash
cmd | lolcat
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-a` | animate     |
| `-d` | delay       |
| `-F` | freq        |

---

### `cowsay`

ASCII cow message

**Syntax**

```bash
cowsay message
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | file        |
| `-l` | list        |

---

### `banner`

Large ASCII text

**Syntax**

```bash
banner text
```

---

### `figlet`

Large ASCII fonts

**Syntax**

```bash
figlet text
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-f` | font        |
| `-l` | list fonts  |
| `-c` | center      |

---

### `toilet`

Figlet alternative

**Syntax**

```bash
toilet text
```

**Options**

| Flag       | Description |
| ---------- | ----------- |
| `-f`       | font        |
| `--filter` | effect      |

---

### `base64`

Base64 encode/decode

**Syntax**

```bash
base64 [opts] [file]
```

**Options**

| Flag               | Description |
| ------------------ | ----------- |
| `-d`               | decode      |
| `-w`               | wrap width  |
| `--ignore-garbage` | —           |

---

### `md5sum`

MD5 checksum

**Syntax**

```bash
md5sum [opts] [file]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | check       |
| `-b` | binary      |
| `-t` | text        |

---

### `sha256sum`

SHA-256 checksum

**Syntax**

```bash
sha256sum [file]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | check       |

---

### `sha512sum`

SHA-512 checksum

**Syntax**

```bash
sha512sum [file]
```

**Options**

| Flag | Description |
| ---- | ----------- |
| `-c` | check       |

---

### `cksum`

CRC checksum

**Syntax**

```bash
cksum [file]
```

---

### `b2sum`

BLAKE2 checksum

**Syntax**

```bash
b2sum [file]
```

---

### `gpg`

GNU Privacy Guard

**Syntax**

```bash
gpg [opts]
```

**Options**

| Flag          | Description   |
| ------------- | ------------- |
| `--encrypt`   | --decrypt     |
| `--sign`      | --verify      |
| `--list-keys` | —             |
| `--import`    | --export      |
| `--gen-key`   | --fingerprint |

---

### `sudo !!`

Rerun last as sudo

**Syntax**

```bash
sudo !!
```

---

### `!$`

Last arg of prev cmd

**Syntax**

```bash
cmd !$
```

---

### `Ctrl+R`

Reverse history search

**Options**

| Flag    | Description              |
| ------- | ------------------------ |
| `type`  | to search                |
| `Enter` | to run Ctrl+R next match |

---
