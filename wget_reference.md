# wget Reference Guide

A complete reference for `wget` — a non-interactive command-line tool for downloading files from the web.

---

## Table of Contents

1. [Basics](#1-basics)
2. [Output & Naming](#2-output--naming)
3. [Download Behavior](#3-download-behavior)
4. [Recursive Download](#4-recursive-download)
5. [Authentication](#5-authentication)
6. [Headers & User Agent](#6-headers--user-agent)
7. [Proxies](#7-proxies)
8. [TLS / SSL](#8-tls--ssl)
9. [Timeouts & Retries](#9-timeouts--retries)
10. [Cookies](#10-cookies)
11. [Logging & Debugging](#11-logging--debugging)
12. [Config File](#12-config-file)
13. [wget vs curl](#13-wget-vs-curl)
14. [Common Recipes](#14-common-recipes)

---

## 1. Basics

```bash
wget https://example.com                        # Download index page to current dir
wget https://example.com/file.zip               # Download file
wget -q https://example.com/file.zip            # Quiet (no output)
wget -nv https://example.com/file.zip           # No verbose (errors + basic info only)
wget --version                                  # Show wget version
```

> Unlike curl, wget saves to a file by default — it does **not** print to stdout unless you use `-O -`.

---

## 2. Output & Naming

```bash
wget -O output.zip https://example.com/file.zip      # Save to specific filename
wget -O - https://example.com                         # Print to stdout (like curl)
wget -P /tmp/downloads https://example.com/file.zip  # Save to specific directory
wget -N https://example.com/file.zip                 # Only download if newer than local

# Auto-generate filename from URL (default behavior)
wget https://example.com/archive.tar.gz              # Saves as archive.tar.gz

# If file exists, wget appends .1, .2, etc.
wget -nc https://example.com/file.zip                # Skip if file already exists
```

---

## 3. Download Behavior

```bash
# Resume an interrupted download
wget -c https://example.com/large.iso

# Download multiple URLs from a file (one URL per line)
wget -i urls.txt

# Limit download speed
wget --limit-rate=500k https://example.com/large.iso

# Download in background
wget -b https://example.com/large.iso
tail -f wget-log                                      # Follow background log

# Mirror a file and timestamp it
wget -N https://example.com/data.csv                  # Skip if local is same age or newer

# Download a list of files matching a pattern (not recursive)
wget https://example.com/files/report-{01..12}.pdf
```

---

## 4. Recursive Download

wget's recursive mode is its killer feature over curl — it can crawl and mirror entire sites.

```bash
# Basic recursive download (depth 1)
wget -r https://example.com

# Set recursion depth
wget -r -l 3 https://example.com                     # Follow links 3 levels deep
wget -r -l inf https://example.com                   # Unlimited depth (careful)

# Mirror a website (recursive + timestamps + no host dirs)
wget -m https://example.com

# Mirror with converted links (make local copy work offline)
wget -m -k https://example.com                       # -k = convert links
wget -m -k -p https://example.com                    # -p = get all page assets (css, img)

# Download only specific file types
wget -r -A "*.pdf,*.zip" https://example.com
wget -r --accept pdf,zip https://example.com

# Reject specific file types
wget -r -R "*.jpg,*.png" https://example.com

# Restrict to same domain (don't follow external links)
wget -r --no-parent https://example.com/docs/

# Span subdomains
wget -r -H --domains=example.com https://example.com

# Exclude certain directories
wget -r -X /private,/admin https://example.com
```

### Recursive Flags Cheat Sheet

| Flag              | Meaning                                      |
|-------------------|----------------------------------------------|
| `-r`              | Enable recursive download                    |
| `-l N`            | Recursion depth (default: 5)                 |
| `-m`              | Mirror mode (`-r -l inf -N`)                 |
| `-k`              | Convert links for offline viewing            |
| `-p`              | Download all assets for each page            |
| `-np` / `--no-parent` | Don't ascend above starting directory   |
| `-A "*.ext"`      | Accept only matching files                   |
| `-R "*.ext"`      | Reject matching files                        |
| `-X /dir`         | Exclude directories                          |
| `-H`              | Span across hosts                            |
| `--domains=x,y`   | Limit spanned hosts                          |

---

## 5. Authentication

```bash
# Basic auth
wget --user=alice --password=secret https://example.com

# Prompt for password (don't expose in shell history)
wget --user=alice --ask-password https://example.com

# Auth via URL (not recommended — leaks credentials in logs)
wget https://alice:secret@example.com/file

# HTTP auth for a specific realm
wget --auth-no-challenge --user=alice --password=secret https://example.com

# NetRC file (~/.netrc)
wget --netrc https://example.com
# ~/.netrc format:
#   machine example.com
#   login   alice
#   password secret
```

---

## 6. Headers & User Agent

```bash
# Custom header
wget --header="Authorization: Bearer TOKEN" https://api.example.com

# Multiple headers
wget \
  --header="Authorization: Bearer TOKEN" \
  --header="Accept: application/json" \
  https://api.example.com

# Change User-Agent
wget -U "Mozilla/5.0" https://example.com
wget --user-agent="MyBot/1.0" https://example.com

# Use a browser User-Agent to bypass basic bot blocks
wget -U "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36" \
  https://example.com

# Add referer header
wget --referer="https://google.com" https://example.com/file
```

---

## 7. Proxies

```bash
# HTTP proxy
wget -e use_proxy=yes -e http_proxy=http://proxy.example.com:8080 https://target.com

# Or via environment variables
export http_proxy=http://proxy.example.com:8080
export https_proxy=http://proxy.example.com:8080
wget https://target.com

# SOCKS proxy (wget2 / with SOCKS support compiled in)
wget --proxy=socks5://127.0.0.1:1080 https://target.com

# Bypass proxy for specific domains
wget --no-proxy=localhost,192.168.1.0/24 https://target.com
```

---

## 8. TLS / SSL

```bash
wget https://example.com                         # Verifies certificate by default
wget --no-check-certificate https://example.com  # Skip cert check (insecure, dev only)

# Use custom CA bundle
wget --ca-certificate=/etc/ssl/my-ca.crt https://example.com

# Client certificate (mutual TLS)
wget --certificate=client.crt --private-key=client.key https://example.com

# Secure protocols only
wget --secure-protocol=TLSv1_3 https://example.com
```

---

## 9. Timeouts & Retries

```bash
wget --timeout=30 https://example.com           # Total timeout (connect + read), seconds
wget --connect-timeout=10 https://example.com   # Connection timeout only
wget --read-timeout=15 https://example.com      # Stalled read timeout

# Retries
wget --tries=5 https://example.com              # Retry up to 5 times (default: 20)
wget --tries=0 https://example.com              # Retry indefinitely
wget --wait=3 https://example.com               # Wait 3s between retries
wget --waitretry=5 https://example.com          # Wait up to 5s between retries (exponential)

# Retry with resume
wget -c --tries=10 https://example.com/large.iso
```

---

## 10. Cookies

```bash
# Send a cookie string
wget --header="Cookie: session=abc123" https://example.com

# Save cookies to file
wget --save-cookies cookies.txt https://example.com

# Load cookies from file
wget --load-cookies cookies.txt https://example.com

# Keep session alive (save + load workflow)
wget --save-cookies cookies.txt --keep-session-cookies \
  --post-data="user=alice&pass=secret" https://example.com/login

wget --load-cookies cookies.txt https://example.com/dashboard
```

---

## 11. Logging & Debugging

```bash
wget -v https://example.com                     # Verbose output (default)
wget -q https://example.com                     # Quiet (no output unless error)
wget -nv https://example.com                    # Non-verbose (minimal output)
wget -d https://example.com                     # Debug (very detailed)

# Log to file
wget -o download.log https://example.com        # Replace stdout with log file
wget -a download.log https://example.com        # Append to log file

# Show server response headers
wget -S https://example.com                     # Print server headers
wget -S -q -O /dev/null https://example.com     # Headers only, discard body

# Dry run (spider mode — check links without downloading)
wget --spider https://example.com
wget --spider -r https://example.com            # Check all links recursively
```

---

## 12. Config File

Store default options in `~/.wgetrc` to avoid repeating flags:

```ini
# ~/.wgetrc
quiet = off
tries = 5
timeout = 30
continue = on
user-agent = Mozilla/5.0
no_check_certificate = off
```

```bash
# Use a custom config file
wget --config=/path/to/custom.wgetrc https://example.com
```

---

## 13. wget vs curl

| Feature                  | wget                          | curl                        |
|--------------------------|-------------------------------|-----------------------------|
| Default behavior         | Saves file                    | Prints to stdout            |
| Recursive download       | Yes (`-r`, `-m`)              | No                          |
| Resume download          | Yes (`-c`)                    | Yes (`-C -`)                |
| Background download      | Yes (`-b`)                    | No (use `&` / `nohup`)      |
| HTTP methods             | GET and POST only             | All methods (`-X`)          |
| Request body control     | Limited (`--post-data`)       | Full (`-d`, `@file`, etc.)  |
| REST API testing         | Awkward                       | Excellent                   |
| Protocols                | HTTP, HTTPS, FTP              | 25+ protocols               |
| Scripting flexibility    | Moderate                      | Excellent                   |
| Site mirroring           | Excellent (`-m -k -p`)        | Not built-in                |

> **Rule of thumb:** Use `wget` for downloading files and mirroring sites. Use `curl` for API calls and custom HTTP requests.

---

## 14. Common Recipes

### Download a File and Resume if Interrupted

```bash
wget -c https://example.com/large.iso
```

### Mirror an Entire Website for Offline Use

```bash
wget -m -k -p --no-parent https://example.com
```

### Download All PDFs from a Page

```bash
wget -r -l 1 -A "*.pdf" --no-parent https://example.com/reports/
```

### Health Check in a Script

```bash
if wget -q --spider https://example.com/health; then
  echo "Up"
else
  echo "Down"
fi
```

### Batch Download from a File

```bash
wget -i urls.txt -P /downloads/
```

### Download with Rate Limiting (polite scraping)

```bash
wget -r -l 2 --wait=2 --limit-rate=200k https://example.com
```

### Check for Broken Links (Spider Mode)

```bash
wget --spider -r -nd -nv -o spider.log https://example.com
grep -i "broken\|error\|404" spider.log
```

### Authenticated Download Behind Login Form

```bash
# Step 1: login and save cookies
wget --save-cookies cookies.txt \
     --keep-session-cookies \
     --post-data="username=alice&password=secret" \
     -O /dev/null \
     https://example.com/login

# Step 2: use session to download protected file
wget --load-cookies cookies.txt \
     -O protected-file.pdf \
     https://example.com/private/file.pdf
```

### Download FTP Directory Recursively

```bash
wget -r ftp://ftp.example.com/pub/
wget -r --ftp-user=alice --ftp-password=secret ftp://ftp.example.com/private/
```

---

## Quick Reference Card

```
wget [options] [URL]

  -O file            Save to specific file (-O - prints to stdout)
  -P dir             Save to specific directory
  -q                 Quiet mode
  -nv                Non-verbose (minimal output)
  -c                 Resume/continue download
  -N                 Download only if newer than local file
  -i file            Read URLs from file
  -r                 Recursive download
  -l N               Recursion depth (default 5)
  -m                 Mirror mode
  -k                 Convert links for offline viewing
  -p                 Download all page assets
  -np                Don't ascend to parent directory
  -A "*.ext"         Accept only these file types
  -R "*.ext"         Reject these file types
  --limit-rate=Nk    Throttle download speed
  --wait=N           Wait N seconds between downloads
  --tries=N          Number of retries
  --timeout=N        Total timeout in seconds
  --user=name        Username for auth
  --password=pass    Password for auth
  --no-check-certificate  Skip TLS verification
  --spider           Check URLs without downloading
  -b                 Run in background
  -o logfile         Log output to file
  -a logfile         Append log to file
  -U "agent"         Set User-Agent string
  --header="K: V"    Add custom header
  --save-cookies f   Save cookies to file
  --load-cookies f   Load cookies from file
```
