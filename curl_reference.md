# curl Reference Guide

A complete reference for `curl` — a command-line tool for transferring data with URLs.

---

## Table of Contents

1. [Basics](#1-basics)
2. [HTTP Methods](#2-http-methods)
3. [Headers](#3-headers)
4. [Request Body & Data](#4-request-body--data)
5. [Authentication](#5-authentication)
6. [Output & Download](#6-output--download)
7. [Upload Files](#7-upload-files)
8. [TLS / SSL](#8-tls--ssl)
9. [Proxies](#9-proxies)
10. [Timeouts & Retries](#10-timeouts--retries)
11. [Cookies](#11-cookies)
12. [Redirects](#12-redirects)
13. [Verbose & Debugging](#13-verbose--debugging)
14. [Config Files](#14-config-files)
15. [Common Recipes](#15-common-recipes)

---

## 1. Basics

```bash
curl https://example.com                        # GET request, print body to stdout
curl -s https://example.com                     # Silent (no progress bar)
curl -S https://example.com                     # Show errors even in silent mode
curl -i https://example.com                     # Include response headers in output
curl -I https://example.com                     # HEAD request (headers only)
curl -o file.html https://example.com           # Save output to file
curl -O https://example.com/file.tar.gz         # Save with remote filename
curl --version                                  # Show curl version and supported protocols
```

### Flag Shorthand
Every short flag has a long equivalent:

| Short | Long            |
|-------|-----------------|
| `-X`  | `--request`     |
| `-H`  | `--header`      |
| `-d`  | `--data`        |
| `-u`  | `--user`        |
| `-o`  | `--output`      |
| `-s`  | `--silent`      |
| `-v`  | `--verbose`     |
| `-L`  | `--location`    |
| `-k`  | `--insecure`    |
| `-F`  | `--form`        |

---

## 2. HTTP Methods

```bash
curl -X GET    https://api.example.com/users    # GET (default, -X is optional)
curl -X POST   https://api.example.com/users    # POST
curl -X PUT    https://api.example.com/users/1  # PUT
curl -X PATCH  https://api.example.com/users/1  # PATCH
curl -X DELETE https://api.example.com/users/1  # DELETE
curl -X OPTIONS https://api.example.com         # OPTIONS (check CORS, allowed methods)
```

> curl defaults to GET unless `-d` / `--data` is used — then it becomes POST automatically.

---

## 3. Headers

```bash
curl -H "Authorization: Bearer TOKEN" https://api.example.com
curl -H "Content-Type: application/json" https://api.example.com
curl -H "Accept: application/json" https://api.example.com

# Multiple headers
curl \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -H "X-Custom-Header: value" \
  https://api.example.com

# Remove a default header (empty value)
curl -H "User-Agent:" https://example.com
```

---

## 4. Request Body & Data

### JSON
```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Alice", "email": "alice@example.com"}'

# From a file
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d @payload.json
```

### Form Data (URL-encoded)
```bash
curl -X POST https://example.com/login \
  -d "username=alice&password=secret"

# Each field separately
curl -X POST https://example.com/login \
  --data-urlencode "username=alice with spaces" \
  --data-urlencode "password=sec ret"
```

### Query Parameters
```bash
curl "https://api.example.com/search?q=curl&limit=10"

# Build params with -G and --data-urlencode
curl -G https://api.example.com/search \
  --data-urlencode "q=curl guide" \
  --data-urlencode "limit=10"
```

---

## 5. Authentication

```bash
# Basic auth
curl -u username:password https://api.example.com

# Bearer token
curl -H "Authorization: Bearer YOUR_TOKEN" https://api.example.com

# API key in header
curl -H "X-API-Key: YOUR_KEY" https://api.example.com

# API key in query string
curl "https://api.example.com/data?api_key=YOUR_KEY"

# Digest auth
curl --digest -u username:password https://api.example.com

# NetRC file (~/.netrc)
curl --netrc https://api.example.com
# ~/.netrc format:
#   machine api.example.com
#   login   myuser
#   password mypassword
```

---

## 6. Output & Download

```bash
curl -o output.html https://example.com          # Save to specific file
curl -O https://example.com/file.zip             # Save with server filename
curl -# -O https://example.com/large.zip         # Progress bar instead of stats

# Download multiple files
curl -O https://example.com/file1.zip \
     -O https://example.com/file2.zip

# Resume interrupted download
curl -C - -O https://example.com/large.zip

# Download only if newer than local file
curl -z local.zip -O https://example.com/file.zip

# Limit download speed (bytes per second)
curl --limit-rate 500k -O https://example.com/large.zip

# Print only specific part of response
curl -s https://api.example.com | jq '.data'     # pipe to jq for JSON
```

---

## 7. Upload Files

```bash
# Multipart form upload
curl -F "file=@/path/to/file.txt" https://example.com/upload

# With filename override
curl -F "file=@/path/to/file.txt;filename=renamed.txt" https://example.com/upload

# Multiple files
curl -F "photo=@photo.jpg" -F "doc=@doc.pdf" https://example.com/upload

# PUT upload (raw binary)
curl -X PUT --data-binary @file.bin https://example.com/upload
```

---

## 8. TLS / SSL

```bash
curl https://example.com                        # Verifies cert by default
curl -k https://example.com                     # Skip cert verification (insecure, dev only)

# Use custom CA certificate
curl --cacert /path/to/ca.crt https://example.com

# Client certificate (mutual TLS)
curl --cert client.crt --key client.key https://example.com

# Pin to specific TLS version
curl --tls-max 1.2 https://example.com          # Max TLS 1.2
curl --tlsv1.3 https://example.com              # Require TLS 1.3

# Show certificate info without connecting
curl --head --verbose https://example.com 2>&1 | grep -A5 "SSL"
```

---

## 9. Proxies

```bash
curl -x http://proxy.example.com:8080 https://target.com
curl --proxy socks5://127.0.0.1:1080 https://target.com

# Proxy with auth
curl -x http://proxy.example.com:8080 -U user:pass https://target.com

# Bypass proxy for specific hosts
curl --noproxy "localhost,192.168.*" https://target.com

# Use system proxy (reads env vars HTTP_PROXY / HTTPS_PROXY)
curl --proxy "" https://example.com             # Disable env proxy
```

---

## 10. Timeouts & Retries

```bash
curl --connect-timeout 5 https://example.com    # Max 5s to establish connection
curl --max-time 30 https://example.com          # Max 30s for entire request

# Retry on transient failures
curl --retry 3 https://example.com
curl --retry 3 --retry-delay 2 https://example.com
curl --retry 3 --retry-max-time 60 https://example.com

# Retry on specific HTTP codes (curl 7.71+)
curl --retry 3 --retry-all-errors https://example.com
```

---

## 11. Cookies

```bash
# Send a cookie
curl -b "session=abc123" https://example.com

# Save cookies to file
curl -c cookies.txt https://example.com

# Load cookies from file (session persistence)
curl -b cookies.txt https://example.com

# Save and load (full cookie jar workflow)
curl -c cookies.txt -b cookies.txt https://example.com/login \
  -d "user=alice&pass=secret"
curl -b cookies.txt https://example.com/dashboard
```

---

## 12. Redirects

```bash
curl -L https://example.com                     # Follow redirects (default: off)
curl -L --max-redirs 5 https://example.com      # Follow up to 5 redirects
curl -I -L https://example.com                  # Show headers for each redirect hop

# Don't follow redirects (default behavior)
curl https://example.com
```

---

## 13. Verbose & Debugging

```bash
curl -v https://example.com                     # Full request/response trace
curl --trace trace.txt https://example.com      # Hex dump to file
curl --trace-ascii trace.txt https://example.com # ASCII dump to file
curl -w "\n%{http_code}\n" https://example.com  # Print HTTP status code after body

# Common -w format variables
curl -w "
  http_code:      %{http_code}
  time_total:     %{time_total}s
  time_connect:   %{time_connect}s
  time_starttransfer: %{time_starttransfer}s
  size_download:  %{size_download} bytes
" -o /dev/null -s https://example.com
```

### Useful `-w` Variables

| Variable              | Description                        |
|-----------------------|------------------------------------|
| `%{http_code}`        | HTTP response status code          |
| `%{time_total}`       | Total time for the operation       |
| `%{time_connect}`     | Time to establish TCP connection   |
| `%{time_starttransfer}` | Time to first byte               |
| `%{size_download}`    | Bytes downloaded                   |
| `%{speed_download}`   | Download speed (bytes/sec)         |
| `%{url_effective}`    | Final URL after redirects          |
| `%{remote_ip}`        | Remote server IP                   |

---

## 14. Config Files

Store default flags in `~/.curlrc` to avoid repeating them:

```ini
# ~/.curlrc
silent
show-error
location
max-time = 30
retry = 3
```

```bash
# Ignore curlrc for a single run
curl -q https://example.com

# Use a specific config file
curl -K /path/to/config https://example.com
```

---

## 15. Common Recipes

### REST API Testing

```bash
# GET with auth and JSON response
curl -s \
  -H "Authorization: Bearer $TOKEN" \
  -H "Accept: application/json" \
  https://api.example.com/users | jq .

# POST JSON and capture status code
HTTP_CODE=$(curl -s -o response.json -w "%{http_code}" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"name":"Bob"}' \
  https://api.example.com/users)

echo "Status: $HTTP_CODE"
cat response.json | jq .
```

### Health Check in Scripts

```bash
if curl -fsS --max-time 5 https://api.example.com/health > /dev/null; then
  echo "Service is up"
else
  echo "Service is down"
fi
```

### Download with Retry & Resume

```bash
curl -C - --retry 5 --retry-delay 3 -O https://example.com/large.iso
```

### Check HTTP Response Code Only

```bash
curl -o /dev/null -s -w "%{http_code}" https://example.com
```

### Send Slack / Webhook Notification

```bash
curl -X POST -H "Content-Type: application/json" \
  -d '{"text": "Deploy complete!"}' \
  https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Parallel Downloads (with xargs)

```bash
cat urls.txt | xargs -P 4 -I{} curl -O {}
```

### GraphQL Request

```bash
curl -X POST https://api.example.com/graphql \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"query": "{ users { id name email } }"}'
```

---

## Quick Reference Card

```
curl [options] [URL]

  -X METHOD          HTTP method (GET/POST/PUT/PATCH/DELETE)
  -H "Key: Value"    Request header
  -d '...'           Request body (makes it POST)
  -d @file           Read body from file
  -u user:pass       Basic authentication
  -o file            Write output to file
  -O                 Write output to file named by URL
  -L                 Follow redirects
  -s                 Silent mode (no progress)
  -v                 Verbose (debug)
  -i                 Include response headers
  -I                 HEAD request only
  -k                 Allow insecure (skip TLS verify)
  -b "k=v"           Send cookie
  -c file            Save cookies to file
  -F "f=@file"       Multipart file upload
  --retry N          Retry N times on failure
  --max-time N       Max total time (seconds)
  --connect-timeout  Max connection time (seconds)
  -w "format"        Write output format after completion
```
