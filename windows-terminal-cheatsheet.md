# 🪟 Windows Terminal — Complete Command Reference

> **CMD** (Command Prompt) & **PowerShell** — Every command, every category

---

## 📑 Table of Contents

1. [Navigation](#-navigation)
2. [Files & Directories](#-files--directories)
3. [Viewing & Editing Files](#-viewing--editing-files)
4. [Search & Find](#-search--find)
5. [Disk & Drive Management](#-disk--drive-management)
6. [System Information](#-system-information)
7. [Processes & Tasks](#-processes--tasks)
8. [Networking](#-networking)
9. [Users & Groups](#-users--groups)
10. [Permissions & Security](#-permissions--security)
11. [Registry](#-registry)
12. [Services](#-services)
13. [Scheduled Tasks](#-scheduled-tasks)
14. [Environment Variables](#-environment-variables)
15. [Package Management](#-package-management-winget)
16. [Startup & Shutdown](#-startup--shutdown)
17. [Backup & Recovery](#-backup--recovery)
18. [Event Logs](#-event-logs)
19. [Hardware & Drivers](#-hardware--drivers)
20. [Power Management](#-power-management)
21. [Redirects, Pipes & Chaining](#-redirects-pipes--chaining)
22. [Scripting & Automation](#-scripting--automation)
23. [Keyboard Shortcuts](#-keyboard-shortcuts)
24. [Complete CMD Command A–Z](#-complete-cmd-command-az)
25. [Complete PowerShell Cmdlet A–Z](#-complete-powershell-cmdlet-az)

---

## 🧭 Navigation

| Action                    | CMD                | PowerShell                                                           |
| ------------------------- | ------------------ | -------------------------------------------------------------------- |
| Print current directory   | `cd`               | `pwd`                                                                |
| Change directory          | `cd <path>`        | `cd <path>`                                                          |
| Go up one level           | `cd ..`            | `cd ..`                                                              |
| Go up two levels          | `cd ..\..`         | `cd ..\..`                                                           |
| Go to drive root          | `cd \`             | `cd \`                                                               |
| Go to home directory      | `cd %USERPROFILE%` | `cd ~`                                                               |
| Switch drive              | `D:`               | `Set-Location D:\`                                                   |
| Push current dir to stack | `pushd <path>`     | `Push-Location <path>`                                               |
| Pop back to previous dir  | `popd`             | `Pop-Location`                                                       |
| Show directory tree       | `tree`             | `tree`                                                               |
| Tree with files           | `tree /f`          | `tree /f`                                                            |
| List contents             | `dir`              | `ls` / `Get-ChildItem`                                               |
| List all (incl. hidden)   | `dir /a`           | `ls -Force`                                                          |
| List subdirectories only  | `dir /ad`          | `ls \| Where-Object PSIsContainer`                                   |
| List files only           | `dir /a-d`         | `ls \| Where-Object { !$_.PSIsContainer }`                           |
| List sorted by date       | `dir /od`          | `ls \| Sort-Object LastWriteTime`                                    |
| List sorted by size       | `dir /os`          | `ls \| Sort-Object Length`                                           |
| List reverse sorted       | `dir /o-n`         | `ls \| Sort-Object Name -Descending`                                 |
| Wide list format          | `dir /w`           | —                                                                    |
| Bare format (names only)  | `dir /b`           | `ls \| Select-Object -ExpandProperty Name`                           |
| Recursive list            | `dir /s`           | `ls -Recurse`                                                        |
| Show folder size          | `dir /s <folder>`  | `(ls -Recurse <folder> \| Measure-Object -Property Length -Sum).Sum` |

### Common Path Shortcuts (CMD)

```cmd
%USERPROFILE%     → C:\Users\<you>
%APPDATA%         → C:\Users\<you>\AppData\Roaming
%LOCALAPPDATA%    → C:\Users\<you>\AppData\Local
%TEMP%            → Temp folder
%WINDIR%          → C:\Windows
%SYSTEMROOT%      → C:\Windows
%PROGRAMFILES%    → C:\Program Files
%PROGRAMFILES(X86)% → C:\Program Files (x86)
%HOMEDRIVE%       → C:
%HOMEPATH%        → \Users\<you>
%PUBLIC%          → C:\Users\Public
%SYSTEMDRIVE%     → C:
```

### Common Path Shortcuts (PowerShell)

```powershell
$env:USERPROFILE
$env:APPDATA
$env:LOCALAPPDATA
$env:TEMP
$env:WINDIR
$env:PROGRAMFILES
$HOME
$PSScriptRoot    # directory of the current script
$PWD             # current directory object
```

---

## 📂 Files & Directories

| Action                | CMD                             | PowerShell                                                        |
| --------------------- | ------------------------------- | ----------------------------------------------------------------- |
| Create directory      | `mkdir <name>`                  | `mkdir <name>` / `New-Item -ItemType Directory`                   |
| Create nested dirs    | `mkdir a\b\c`                   | `mkdir a\b\c -Force`                                              |
| Remove empty dir      | `rmdir <name>`                  | `rmdir <name>`                                                    |
| Remove dir + contents | `rmdir /s /q <name>`            | `rm -Recurse -Force <name>`                                       |
| Create empty file     | `type nul > file.txt`           | `New-Item file.txt -ItemType File`                                |
| Copy file             | `copy src dst`                  | `cp src dst` / `Copy-Item src dst`                                |
| Copy folder           | `xcopy src dst /e /i /h`        | `cp src dst -Recurse`                                             |
| Mirror copy           | `robocopy src dst /mir`         | `robocopy src dst /mir`                                           |
| Move / rename         | `move src dst`                  | `mv src dst` / `Move-Item src dst`                                |
| Rename                | `ren old new`                   | `Rename-Item old new`                                             |
| Delete file           | `del file.txt`                  | `rm file.txt` / `Remove-Item file.txt`                            |
| Delete wildcards      | `del *.log`                     | `rm *.log`                                                        |
| Delete read-only      | `del /f file.txt`               | `rm -Force file.txt`                                              |
| Delete silently       | `del /q file.txt`               | `rm -Force file.txt`                                              |
| Delete all in dir     | `del /q /f /s *.*`              | `rm -Recurse -Force .\*`                                          |
| Create symlink (file) | `mklink link.txt target.txt`    | `New-Item -ItemType SymbolicLink -Name link -Target target`       |
| Create symlink (dir)  | `mklink /d linkdir targetdir`   | `New-Item -ItemType SymbolicLink -Name linkdir -Target targetdir` |
| Create hardlink       | `mklink /h link.txt target.txt` | —                                                                 |
| Create junction       | `mklink /j junction target`     | `New-Item -ItemType Junction ...`                                 |
| Show file attributes  | `attrib file.txt`               | `Get-Item file.txt \| Select-Object Attributes`                   |
| Set file attribute    | `attrib +r file.txt`            | `Set-ItemProperty file.txt -Name Attributes -Value ReadOnly`      |
| Remove read-only attr | `attrib -r file.txt`            | —                                                                 |
| Hide file             | `attrib +h file.txt`            | —                                                                 |
| Show file path        | `where file.txt`                | `(Get-Item file.txt).FullName`                                    |
| Compare two files     | `fc file1.txt file2.txt`        | `Compare-Object (gc file1) (gc file2)`                            |
| Encrypt file (EFS)    | `cipher /e file.txt`            | —                                                                 |
| Decrypt file          | `cipher /d file.txt`            | —                                                                 |
| Compact file          | `compact /c file.txt`           | —                                                                 |
| Print file to printer | `print file.txt`                | —                                                                 |

### ROBOCOPY (Advanced Copy)

```cmd
robocopy src dst                  :: Basic copy
robocopy src dst /mir             :: Mirror (delete extra files in dst)
robocopy src dst /e               :: Include all subdirectories
robocopy src dst /z               :: Restartable mode
robocopy src dst /r:3 /w:5        :: Retry 3 times, wait 5 sec
robocopy src dst *.txt /s         :: Copy only .txt files recursively
robocopy src dst /log:copy.log    :: Save log to file
robocopy src dst /xf *.tmp        :: Exclude .tmp files
robocopy src dst /xd cache        :: Exclude "cache" directory
```

### XCOPY (Classic Copy)

```cmd
xcopy src dst /e    :: Copy all subdirs (including empty)
xcopy src dst /h    :: Include hidden/system files
xcopy src dst /y    :: Overwrite without prompt
xcopy src dst /d    :: Copy only newer files
xcopy src dst /exclude:list.txt  :: Exclude files in list
```

---

## 📄 Viewing & Editing Files

| Action                   | CMD                                  | PowerShell                                                           |
| ------------------------ | ------------------------------------ | -------------------------------------------------------------------- |
| Print file               | `type file.txt`                      | `cat file.txt` / `Get-Content file.txt`                              |
| Page through file        | `more file.txt`                      | `more file.txt`                                                      |
| First N lines            | —                                    | `Get-Content file.txt -Head 10`                                      |
| Last N lines             | —                                    | `Get-Content file.txt -Tail 10`                                      |
| Follow file live         | —                                    | `Get-Content file.txt -Wait`                                         |
| Write to file            | `echo text > file.txt`               | `"text" > file.txt` / `Set-Content file.txt "text"`                  |
| Append to file           | `echo text >> file.txt`              | `"text" >> file.txt` / `Add-Content file.txt "text"`                 |
| Count lines              | `find /c /v "" file.txt`             | `(Get-Content file.txt).Count`                                       |
| Open Notepad             | `notepad file.txt`                   | `notepad file.txt`                                                   |
| Open VS Code             | `code file.txt`                      | `code file.txt`                                                      |
| Open with default app    | `start file.txt`                     | `Invoke-Item file.txt`                                               |
| Open Explorer here       | `explorer .`                         | `explorer .`                                                         |
| Hash file (MD5)          | `certutil -hashfile file.txt MD5`    | `Get-FileHash file.txt -Algorithm MD5`                               |
| Hash file (SHA256)       | `certutil -hashfile file.txt SHA256` | `Get-FileHash file.txt`                                              |
| Base64 encode            | `certutil -encode src.txt out.txt`   | `[Convert]::ToBase64String([IO.File]::ReadAllBytes("file"))`         |
| Base64 decode            | `certutil -decode src.txt out.txt`   | `[IO.File]::WriteAllBytes("out", [Convert]::FromBase64String($b64))` |
| Sort file contents       | `sort file.txt`                      | `Get-Content file.txt \| Sort-Object`                                |
| Remove duplicates        | —                                    | `Get-Content file.txt \| Select-Object -Unique`                      |
| Copy output to clipboard | `dir \| clip`                        | `dir \| Set-Clipboard`                                               |
| Paste from clipboard     | —                                    | `Get-Clipboard`                                                      |
| Word count               | —                                    | `(Get-Content file.txt -Raw).Split().Count`                          |

---

## 🔍 Search & Find

| Action                    | CMD                                             | PowerShell                                                                  |
| ------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------- |
| Find text in file         | `findstr "text" file.txt`                       | `Select-String "text" file.txt`                                             |
| Case-insensitive          | `findstr /i "text" file.txt`                    | `Select-String -NoCase "text" file.txt`                                     |
| Regex search              | `findstr /r "pat" file.txt`                     | `Select-String -Pattern "regex" file.txt`                                   |
| Whole word search         | `findstr /w "word" file.txt`                    | `Select-String -SimpleMatch "word" file.txt`                                |
| Recursive search          | `findstr /s "text" *.*`                         | `Get-ChildItem -Recurse \| Select-String "text"`                            |
| Find in multiple files    | `findstr "text" *.txt`                          | `Select-String "text" *.txt`                                                |
| Show file names only      | `findstr /l /m "text" *`                        | `Select-String "text" * \| Select-Object Filename -Unique`                  |
| Find file by name         | `where file.txt`                                | `Get-ChildItem -Recurse -Filter "file.txt"`                                 |
| Find by extension         | `dir /s /b *.log`                               | `Get-ChildItem -Recurse -Filter "*.log"`                                    |
| Find files modified today | —                                               | `Get-ChildItem -Recurse \| Where-Object LastWriteTime -gt (Get-Date).Date`  |
| Find files over 100MB     | —                                               | `Get-ChildItem -Recurse \| Where-Object Length -gt 100MB`                   |
| Find empty files          | —                                               | `Get-ChildItem -Recurse \| Where-Object Length -eq 0`                       |
| Find empty folders        | —                                               | `Get-ChildItem -Directory -Recurse \| Where-Object { !(Get-ChildItem $_) }` |
| FORFILES by date          | `forfiles /m *.log /d -7 /c "cmd /c del @path"` | —                                                                           |

### FINDSTR Flags

```cmd
findstr /b "text" file    :: Match at beginning of line
findstr /e "text" file    :: Match at end of line
findstr /x "text" file    :: Exact match of whole line
findstr /v "text" file    :: Print lines NOT containing text
findstr /n "text" file    :: Print line numbers
findstr /c:"phrase" file  :: Literal string (multi-word)
findstr /g:list.txt file  :: Search strings from a file
```

---

## 💾 Disk & Drive Management

| Action                  | CMD                                           | PowerShell                                                        |
| ----------------------- | --------------------------------------------- | ----------------------------------------------------------------- |
| List drives             | `wmic logicaldisk get caption,description`    | `Get-PSDrive -PSProvider FileSystem`                              |
| Drive info              | `vol C:`                                      | `Get-Volume C`                                                    |
| Disk usage              | `wmic logicaldisk get size,freespace,caption` | `Get-Volume`                                                      |
| Check disk              | `chkdsk C:`                                   | `Repair-Volume -DriveLetter C -Scan`                              |
| Fix disk errors         | `chkdsk C: /f`                                | `Repair-Volume -DriveLetter C`                                    |
| Fix bad sectors         | `chkdsk C: /r`                                | `Repair-Volume -DriveLetter C -OfflineScanAndFix`                 |
| Schedule chkdsk on boot | `chkdsk C: /f /r /x`                          | —                                                                 |
| Disk status             | `chkntfs C:`                                  | `Get-Disk`                                                        |
| Format drive            | `format D: /fs:NTFS /q`                       | `Format-Volume -DriveLetter D -FileSystem NTFS`                   |
| Label drive             | `label C: MyDrive`                            | `Set-Volume -DriveLetter C -NewFileSystemLabel "MyDrive"`         |
| Map network drive       | `net use Z: \\server\share`                   | `New-PSDrive -Name Z -PSProvider FileSystem -Root \\server\share` |
| Unmap network drive     | `net use Z: /delete`                          | `Remove-PSDrive Z`                                                |
| Substitute path         | `subst Z: C:\long\path\here`                  | —                                                                 |
| Remove substitution     | `subst Z: /d`                                 | —                                                                 |
| Defragment drive        | `defrag C: /u /v`                             | `Optimize-Volume -DriveLetter C -Defrag`                          |
| Optimize SSD (TRIM)     | `defrag C: /l`                                | `Optimize-Volume -DriveLetter C -ReTrim`                          |
| Compact OS              | `compact /compactOS:always`                   | —                                                                 |

### DISKPART (Interactive)

```cmd
diskpart
  list disk              :: List all physical disks
  select disk 1          :: Select disk 1
  list partition         :: List partitions on selected disk
  select partition 1     :: Select partition 1
  list volume            :: List all volumes
  select volume 2        :: Select volume 2
  active                 :: Mark partition as active
  format fs=ntfs quick   :: Quick format
  assign letter=E        :: Assign drive letter E
  delete partition       :: Delete selected partition
  clean                  :: Wipe entire disk
  exit
```

---

## ⚙️ System Information

| Action                | CMD                                        | PowerShell                                                                                                                        |
| --------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| Computer name         | `hostname`                                 | `$env:COMPUTERNAME`                                                                                                               |
| Current user          | `whoami`                                   | `[System.Security.Principal.WindowsIdentity]::GetCurrent().Name`                                                                  |
| User groups           | `whoami /groups`                           | `(New-Object Security.Principal.WindowsPrincipal([Security.Principal.WindowsIdentity]::GetCurrent())).IsInRole("Administrators")` |
| Windows version       | `ver`                                      | `[System.Environment]::OSVersion`                                                                                                 |
| Detailed system info  | `systeminfo`                               | `Get-ComputerInfo`                                                                                                                |
| BIOS info             | `wmic bios get smbiosbiosversion`          | `Get-WmiObject Win32_BIOS`                                                                                                        |
| CPU info              | `wmic cpu get name,numberofcores`          | `Get-WmiObject Win32_Processor`                                                                                                   |
| RAM total             | `wmic memorychip get capacity`             | `(Get-WmiObject Win32_PhysicalMemory \| Measure-Object Capacity -Sum).Sum / 1GB`                                                  |
| Available RAM         | `wmic OS get FreePhysicalMemory`           | `(Get-WmiObject Win32_OperatingSystem).FreePhysicalMemory / 1MB`                                                                  |
| GPU info              | `wmic path win32_VideoController get name` | `Get-WmiObject Win32_VideoController \| Select Name`                                                                              |
| Monitor info          | `wmic desktopmonitor get name`             | `Get-WmiObject Win32_DesktopMonitor`                                                                                              |
| Motherboard info      | `wmic baseboard get manufacturer,product`  | `Get-WmiObject Win32_BaseBoard`                                                                                                   |
| Serial number         | `wmic bios get serialnumber`               | `(Get-WmiObject Win32_BIOS).SerialNumber`                                                                                         |
| System boot time      | `net statistics workstation`               | `(Get-CimInstance Win32_OperatingSystem).LastBootUpTime`                                                                          |
| Uptime                | —                                          | `(Get-Date) - (gcim Win32_OperatingSystem).LastBootUpTime`                                                                        |
| Environment variables | `set`                                      | `Get-ChildItem Env:`                                                                                                              |
| Installed software    | `wmic product get name,version`            | `Get-WmiObject Win32_Product \| Select Name,Version`                                                                              |
| Windows license key   | —                                          | `(Get-WmiObject -query 'select * from SoftwareLicensingService').OA3xOriginalProductKey`                                          |
| Windows activation    | `slmgr /xpr`                               | `slmgr /xpr`                                                                                                                      |

---

## 🔄 Processes & Tasks

| Action                    | CMD                             | PowerShell                                                       |
| ------------------------- | ------------------------------- | ---------------------------------------------------------------- |
| List all processes        | `tasklist`                      | `Get-Process`                                                    |
| Find process by name      | `tasklist \| findstr "chrome"`  | `Get-Process -Name chrome`                                       |
| Find process by PID       | `tasklist \| findstr "1234"`    | `Get-Process -Id 1234`                                           |
| List with memory usage    | `tasklist /v`                   | `Get-Process \| Sort-Object WS -Descending`                      |
| Kill by name              | `taskkill /IM chrome.exe /F`    | `Stop-Process -Name chrome -Force`                               |
| Kill by PID               | `taskkill /PID 1234 /F`         | `Stop-Process -Id 1234`                                          |
| Kill all instances        | `taskkill /IM chrome.exe /F /T` | `Get-Process chrome \| Stop-Process`                             |
| Start application         | `start notepad.exe`             | `Start-Process notepad`                                          |
| Start as admin            | —                               | `Start-Process notepad -Verb runAs`                              |
| Start minimized           | `start /min notepad.exe`        | `Start-Process notepad -WindowStyle Minimized`                   |
| Start with priority       | `start /high cmd.exe`           | `(Start-Process notepad -PassThru).PriorityClass = "High"`       |
| List startup items        | `wmic startup list brief`       | `Get-CimInstance Win32_StartupCommand`                           |
| Run command in background | `start /b command`              | `Start-Job { command }`                                          |
| Wait for process          | —                               | `Wait-Process -Name notepad`                                     |
| Check if running          | —                               | `Get-Process notepad -ErrorAction SilentlyContinue`              |
| CPU usage of process      | —                               | `Get-Process \| Sort CPU -Descending \| Select -First 10`        |
| Memory of process         | —                               | `Get-Process \| Sort WS -Descending \| Select Name,WS -First 10` |
| Full process details      | —                               | `Get-Process -Name chrome \| Format-List *`                      |

---

## 🌐 Networking

| Action                    | CMD                                                                                        | PowerShell                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| Show all adapters         | `ipconfig`                                                                                 | `Get-NetAdapter`                                                                                |
| Full IP config            | `ipconfig /all`                                                                            | `Get-NetIPConfiguration`                                                                        |
| Show IP addresses         | —                                                                                          | `Get-NetIPAddress`                                                                              |
| Show default gateway      | —                                                                                          | `Get-NetRoute -DestinationPrefix "0.0.0.0/0"`                                                   |
| Release DHCP lease        | `ipconfig /release`                                                                        | —                                                                                               |
| Renew DHCP lease          | `ipconfig /renew`                                                                          | —                                                                                               |
| Flush DNS cache           | `ipconfig /flushdns`                                                                       | `Clear-DnsClientCache`                                                                          |
| Show DNS cache            | `ipconfig /displaydns`                                                                     | `Get-DnsClientCache`                                                                            |
| Show hostname             | `hostname`                                                                                 | `hostname`                                                                                      |
| Ping host                 | `ping google.com`                                                                          | `Test-Connection google.com`                                                                    |
| Ping with count           | `ping -n 5 google.com`                                                                     | `Test-Connection google.com -Count 5`                                                           |
| Continuous ping           | `ping -t google.com`                                                                       | `Test-Connection google.com -Repeat`                                                            |
| Trace route               | `tracert google.com`                                                                       | `Test-NetConnection google.com -TraceRoute`                                                     |
| Path ping (statistics)    | `pathping google.com`                                                                      | —                                                                                               |
| DNS lookup                | `nslookup google.com`                                                                      | `Resolve-DnsName google.com`                                                                    |
| DNS reverse lookup        | `nslookup 8.8.8.8`                                                                         | `Resolve-DnsName 8.8.8.8`                                                                       |
| Show routing table        | `route print`                                                                              | `Get-NetRoute`                                                                                  |
| Add static route          | `route add 192.168.1.0 mask 255.255.255.0 192.168.0.1`                                     | `New-NetRoute -DestinationPrefix "192.168.1.0/24" -NextHop 192.168.0.1`                         |
| Delete route              | `route delete 192.168.1.0`                                                                 | `Remove-NetRoute -DestinationPrefix "192.168.1.0/24"`                                           |
| Show ARP table            | `arp -a`                                                                                   | `Get-NetNeighbor`                                                                               |
| Clear ARP cache           | `arp -d *`                                                                                 | `Remove-NetNeighbor -Confirm:$false`                                                            |
| Show all connections      | `netstat -an`                                                                              | `Get-NetTCPConnection`                                                                          |
| Show listening ports      | `netstat -an \| findstr LISTENING`                                                         | `Get-NetTCPConnection -State Listen`                                                            |
| Show connections with PID | `netstat -ano`                                                                             | `Get-NetTCPConnection \| Select Local*,Remote*,State,OwningProcess`                             |
| Show network stats        | `netstat -s`                                                                               | —                                                                                               |
| Test port connection      | `telnet host 80`                                                                           | `Test-NetConnection host -Port 80`                                                              |
| Show open shares          | `net share`                                                                                | `Get-SmbShare`                                                                                  |
| Connect to share          | `net use \\server\share`                                                                   | `New-SmbMapping -RemotePath \\server\share`                                                     |
| Disconnect share          | `net use \\server\share /delete`                                                           | `Remove-SmbMapping \\server\share`                                                              |
| Download file             | —                                                                                          | `Invoke-WebRequest -Uri <url> -OutFile file`                                                    |
| HTTP GET                  | —                                                                                          | `Invoke-RestMethod -Uri <url>`                                                                  |
| HTTP POST                 | —                                                                                          | `Invoke-RestMethod -Uri <url> -Method Post -Body $data`                                         |
| FTP session               | `ftp ftp.example.com`                                                                      | —                                                                                               |
| Check firewall            | `netsh advfirewall show allprofiles`                                                       | `Get-NetFirewallProfile`                                                                        |
| Add firewall rule         | `netsh advfirewall firewall add rule name="Test" dir=in action=allow port=80 protocol=tcp` | `New-NetFirewallRule -Name "Test" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 80` |
| Remove firewall rule      | `netsh advfirewall firewall delete rule name="Test"`                                       | `Remove-NetFirewallRule -Name "Test"`                                                           |
| Reset TCP/IP stack        | `netsh int ip reset`                                                                       | —                                                                                               |
| Reset Winsock             | `netsh winsock reset`                                                                      | —                                                                                               |
| Wi-Fi profiles            | `netsh wlan show profiles`                                                                 | `Get-NetConnectionProfile`                                                                      |
| Wi-Fi password            | `netsh wlan show profile name="SSID" key=clear`                                            | —                                                                                               |
| Enable/Disable adapter    | `netsh interface set interface "Ethernet" disable`                                         | `Disable-NetAdapter -Name "Ethernet"` / `Enable-NetAdapter`                                     |

---

## 👤 Users & Groups

| Action             | CMD                                     | PowerShell                                                                                 |
| ------------------ | --------------------------------------- | ------------------------------------------------------------------------------------------ |
| List local users   | `net user`                              | `Get-LocalUser`                                                                            |
| User details       | `net user <name>`                       | `Get-LocalUser <name>`                                                                     |
| Add user           | `net user <name> <pass> /add`           | `New-LocalUser -Name <name> -Password (ConvertTo-SecureString "pass" -AsPlainText -Force)` |
| Delete user        | `net user <name> /delete`               | `Remove-LocalUser -Name <name>`                                                            |
| Change password    | `net user <name> <newpass>`             | `Set-LocalUser -Name <name> -Password (...)`                                               |
| Enable user        | `net user <name> /active:yes`           | `Enable-LocalUser -Name <name>`                                                            |
| Disable user       | `net user <name> /active:no`            | `Disable-LocalUser -Name <name>`                                                           |
| List local groups  | `net localgroup`                        | `Get-LocalGroup`                                                                           |
| Group members      | `net localgroup <group>`                | `Get-LocalGroupMember <group>`                                                             |
| Add to group       | `net localgroup <group> <user> /add`    | `Add-LocalGroupMember -Group <group> -Member <user>`                                       |
| Remove from group  | `net localgroup <group> <user> /delete` | `Remove-LocalGroupMember -Group <group> -Member <user>`                                    |
| Create group       | `net localgroup <group> /add`           | `New-LocalGroup -Name <group>`                                                             |
| Delete group       | `net localgroup <group> /delete`        | `Remove-LocalGroup -Name <group>`                                                          |
| Whoami (full)      | `whoami /all`                           | `whoami /all`                                                                              |
| Whoami groups only | `whoami /groups`                        | —                                                                                          |
| Whoami privileges  | `whoami /priv`                          | —                                                                                          |

---

## 🔐 Permissions & Security

| Action                   | CMD                                                                                     | PowerShell                                                                                                                                                   |
| ------------------------ | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| View permissions         | `icacls file.txt`                                                                       | `Get-Acl file.txt \| Format-List`                                                                                                                            |
| Grant permission         | `icacls file.txt /grant User:F`                                                         | `$acl = Get-Acl file; $acl.SetAccessRule(...); Set-Acl file $acl`                                                                                            |
| Deny permission          | `icacls file.txt /deny User:F`                                                          | —                                                                                                                                                            |
| Remove permission        | `icacls file.txt /remove User`                                                          | —                                                                                                                                                            |
| Take ownership           | `takeown /f file.txt`                                                                   | —                                                                                                                                                            |
| Take ownership recursive | `takeown /f folder /r /d y`                                                             | —                                                                                                                                                            |
| Reset permissions        | `icacls folder /reset /t /c`                                                            | —                                                                                                                                                            |
| Inherit permissions      | `icacls file.txt /inheritance:e`                                                        | —                                                                                                                                                            |
| Remove inheritance       | `icacls file.txt /inheritance:d`                                                        | —                                                                                                                                                            |
| File audit               | `auditpol /get /category:*`                                                             | —                                                                                                                                                            |
| View group policy        | `gpresult /r`                                                                           | `Get-GPResultantSetOfPolicy -ReportType HTML -Path gp.html`                                                                                                  |
| Apply group policy       | `gpupdate /force`                                                                       | `Invoke-GPUpdate -Force`                                                                                                                                     |
| Check UAC status         | `reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v EnableLUA` | —                                                                                                                                                            |
| Run as admin check       | —                                                                                       | `([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)` |
| Cipher (EFS)             | `cipher /e /s:folder`                                                                   | —                                                                                                                                                            |
| SFC (system file check)  | `sfc /scannow`                                                                          | —                                                                                                                                                            |
| DISM restore health      | `dism /Online /Cleanup-Image /RestoreHealth`                                            | —                                                                                                                                                            |
| BitLocker status         | `manage-bde -status`                                                                    | `Get-BitLockerVolume`                                                                                                                                        |
| Enable BitLocker         | `manage-bde -on C: -RecoveryPassword`                                                   | `Enable-BitLocker -MountPoint C:`                                                                                                                            |
| Disable BitLocker        | `manage-bde -off C:`                                                                    | `Disable-BitLocker -MountPoint C:`                                                                                                                           |

---

## 🗝️ Registry

| Action             | CMD                                                  | PowerShell                                                                                           |
| ------------------ | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Query key          | `reg query HKLM\SOFTWARE\MyApp`                      | `Get-ItemProperty HKLM:\SOFTWARE\MyApp`                                                              |
| Query value        | `reg query HKLM\...\MyApp /v Version`                | `Get-ItemPropertyValue HKLM:\...\MyApp -Name Version`                                                |
| Add/Set value      | `reg add HKLM\...\MyApp /v Key /t REG_SZ /d "value"` | `Set-ItemProperty HKLM:\...\MyApp -Name Key -Value "value"`                                          |
| Delete value       | `reg delete HKLM\...\MyApp /v Key /f`                | `Remove-ItemProperty HKLM:\...\MyApp -Name Key`                                                      |
| Delete key         | `reg delete HKLM\...\MyApp /f`                       | `Remove-Item HKLM:\...\MyApp -Recurse`                                                               |
| Create key         | `reg add HKLM\...\NewKey`                            | `New-Item HKLM:\...\NewKey`                                                                          |
| Export to file     | `reg export HKLM\...\MyApp backup.reg`               | `Export-Registry ...`                                                                                |
| Import from file   | `reg import backup.reg`                              | `reg import backup.reg`                                                                              |
| Compare registries | `reg compare HKLM\App1 HKLM\App2`                    | —                                                                                                    |
| Copy key           | `reg copy HKLM\App1 HKLM\App2 /s`                    | `cp HKLM:\App1 HKLM:\App2 -Recurse`                                                                  |
| Search in registry | —                                                    | `Get-ChildItem HKLM:\ -Recurse -ErrorAction SilentlyContinue \| Where-Object { $_ -match "search" }` |

### Registry Hives

```
HKLM  = HKEY_LOCAL_MACHINE   (system-wide settings)
HKCU  = HKEY_CURRENT_USER    (current user settings)
HKCR  = HKEY_CLASSES_ROOT    (file associations)
HKU   = HKEY_USERS           (all users profiles)
HKCC  = HKEY_CURRENT_CONFIG  (hardware profile)
```

### Registry Value Types

```
REG_SZ        = String
REG_EXPAND_SZ = Expandable string (%VAR%)
REG_DWORD     = 32-bit number
REG_QWORD     = 64-bit number
REG_BINARY    = Binary data
REG_MULTI_SZ  = Multi-string
```

---

## ⚙️ Services

| Action                  | CMD                                                    | PowerShell                                              |
| ----------------------- | ------------------------------------------------------ | ------------------------------------------------------- |
| List all services       | `sc query`                                             | `Get-Service`                                           |
| List running only       | `sc query state= running`                              | `Get-Service \| Where-Object Status -eq Running`        |
| List stopped only       | `sc query state= stopped`                              | `Get-Service \| Where-Object Status -eq Stopped`        |
| Service details         | `sc qc <service>`                                      | `Get-Service <service> \| Format-List *`                |
| Start service           | `sc start <service>`                                   | `Start-Service <service>`                               |
| Stop service            | `sc stop <service>`                                    | `Stop-Service <service>`                                |
| Restart service         | `net stop <svc> && net start <svc>`                    | `Restart-Service <service>`                             |
| Pause service           | `sc pause <service>`                                   | `Suspend-Service <service>`                             |
| Resume service          | `sc continue <service>`                                | `Resume-Service <service>`                              |
| Set startup type        | `sc config <svc> start= auto`                          | `Set-Service <svc> -StartupType Automatic`              |
| Startup types           | `boot\|system\|auto\|demand\|disabled`                 | `Boot\|System\|Automatic\|Manual\|Disabled`             |
| Create service          | `sc create <name> binpath= "C:\app.exe"`               | `New-Service -Name <name> -BinaryPathName "C:\app.exe"` |
| Delete service          | `sc delete <name>`                                     | `Remove-Service <name>`                                 |
| Show dependencies       | `sc enumdepend <service>`                              | `(Get-Service <svc>).DependentServices`                 |
| Service failure actions | `sc failure <svc> reset= 86400 actions= restart/60000` | —                                                       |

---

## 📅 Scheduled Tasks

| Action                   | CMD                                                                   | PowerShell                                                    |
| ------------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------- |
| List all tasks           | `schtasks /query`                                                     | `Get-ScheduledTask`                                           |
| Task details             | `schtasks /query /tn "\TaskName" /v /fo list`                         | `Get-ScheduledTask -TaskName "Name" \| Get-ScheduledTaskInfo` |
| Create task (daily)      | `schtasks /create /tn "Name" /tr "C:\script.bat" /sc daily /st 09:00` | `Register-ScheduledTask ...`                                  |
| Create task (at startup) | `schtasks /create /tn "Name" /tr "C:\app.exe" /sc onstart /ru SYSTEM` | —                                                             |
| Create task (on logon)   | `schtasks /create /tn "Name" /tr "C:\app.exe" /sc onlogon`            | —                                                             |
| Run task now             | `schtasks /run /tn "Name"`                                            | `Start-ScheduledTask -TaskName "Name"`                        |
| End task                 | `schtasks /end /tn "Name"`                                            | `Stop-ScheduledTask -TaskName "Name"`                         |
| Enable task              | `schtasks /change /tn "Name" /enable`                                 | `Enable-ScheduledTask -TaskName "Name"`                       |
| Disable task             | `schtasks /change /tn "Name" /disable`                                | `Disable-ScheduledTask -TaskName "Name"`                      |
| Delete task              | `schtasks /delete /tn "Name" /f`                                      | `Unregister-ScheduledTask -TaskName "Name" -Confirm:$false`   |

### Create Task via PowerShell

```powershell
$action  = New-ScheduledTaskAction -Execute "C:\script.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 9am
$settings = New-ScheduledTaskSettingsSet -RunOnlyIfNetworkAvailable
Register-ScheduledTask -TaskName "MyTask" -Action $action -Trigger $trigger -Settings $settings -RunLevel Highest
```

---

## 🧩 Environment Variables

| Action                   | CMD                      | PowerShell                                                     |
| ------------------------ | ------------------------ | -------------------------------------------------------------- |
| Print all variables      | `set`                    | `Get-ChildItem Env:`                                           |
| Print one variable       | `echo %PATH%`            | `$env:PATH`                                                    |
| Print formatted          | `set VAR`                | `$env:VAR`                                                     |
| Set (session only)       | `set VAR=value`          | `$env:VAR = "value"`                                           |
| Append to PATH           | `set PATH=%PATH%;C:\new` | `$env:PATH += ";C:\new"`                                       |
| Set permanently (user)   | `setx VAR "value"`       | `[Environment]::SetEnvironmentVariable("VAR","val","User")`    |
| Set permanently (system) | `setx VAR "value" /m`    | `[Environment]::SetEnvironmentVariable("VAR","val","Machine")` |
| Delete (session)         | `set VAR=`               | `Remove-Item Env:VAR`                                          |
| Delete permanently       | `setx VAR ""`            | `[Environment]::SetEnvironmentVariable("VAR",$null,"User")`    |
| Get from .NET            | —                        | `[System.Environment]::GetEnvironmentVariable("VAR")`          |

---

## 📦 Package Management (winget)

```powershell
winget search <query>               # Search available packages
winget install <id/name>            # Install a package
winget install <id> --silent        # Silent install
winget install <id> --version 1.0   # Install specific version
winget uninstall <id/name>          # Uninstall a package
winget upgrade                      # List upgradeable packages
winget upgrade <id>                 # Upgrade specific package
winget upgrade --all                # Upgrade all packages
winget list                         # List installed packages
winget list <query>                 # Filter installed packages
winget show <id>                    # Show package details
winget source list                  # List package sources
winget source add --name <n> --arg <url>  # Add source
winget import -i packages.json      # Bulk install from file
winget export -o packages.json      # Export installed list
winget settings                     # Open settings file
winget features                     # List experimental features
```

---

## 🔌 Startup & Shutdown

| Action                  | CMD                                                    | PowerShell                |
| ----------------------- | ------------------------------------------------------ | ------------------------- |
| Shutdown immediately    | `shutdown /s /t 0`                                     | `Stop-Computer -Force`    |
| Shutdown with delay     | `shutdown /s /t 60`                                    | `Stop-Computer`           |
| Restart                 | `shutdown /r /t 0`                                     | `Restart-Computer -Force` |
| Restart with delay      | `shutdown /r /t 60`                                    | —                         |
| Log off                 | `shutdown /l`                                          | `logoff`                  |
| Hibernate               | `shutdown /h`                                          | —                         |
| Sleep                   | `rundll32.exe powrprof.dll,SetSuspendState 0,1,0`      | —                         |
| Cancel shutdown         | `shutdown /a`                                          | —                         |
| BIOS restart (firmware) | `shutdown /r /fw /t 0`                                 | —                         |
| Safe mode restart       | `bcdedit /set {current} safeboot minimal` then restart | —                         |
| Cancel safe mode        | `bcdedit /deletevalue {current} safeboot`              | —                         |
| Lock screen             | `rundll32.exe user32.dll,LockWorkStation`              | —                         |

---

## 💾 Backup & Recovery

| Action               | CMD                                                                                           | PowerShell                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| System restore point | `wmic /namespace:\\root\default Path SystemRestore Call CreateRestorePoint "MyPoint", 100, 7` | `Checkpoint-Computer -Description "Backup" -RestorePointType MODIFY_SETTINGS` |
| List restore points  | —                                                                                             | `Get-ComputerRestorePoint`                                                    |
| Restore from point   | —                                                                                             | `Restore-Computer -RestorePoint 5`                                            |
| Shadow copy list     | `vssadmin list shadows`                                                                       | `Get-WmiObject Win32_ShadowCopy`                                              |
| Create shadow copy   | `wmic shadowcopy call create volume=C:\`                                                      | —                                                                             |
| Windows backup       | `wbadmin start backup -backupTarget:D: -include:C: -allCritical`                              | —                                                                             |
| Backup status        | `wbadmin get status`                                                                          | —                                                                             |
| Recover files        | `wbadmin start recovery ...`                                                                  | —                                                                             |
| Repair boot          | `bootrec /fixmbr`                                                                             | —                                                                             |
| Repair BCD           | `bootrec /rebuildbcd`                                                                         | —                                                                             |
| Fix boot sector      | `bootrec /fixboot`                                                                            | —                                                                             |
| SFC full scan        | `sfc /scannow`                                                                                | —                                                                             |
| DISM health check    | `dism /Online /Cleanup-Image /CheckHealth`                                                    | —                                                                             |
| DISM repair          | `dism /Online /Cleanup-Image /RestoreHealth`                                                  | —                                                                             |
| DISM from ISO        | `dism /Online /Cleanup-Image /RestoreHealth /Source:D:\sources\install.wim`                   | —                                                                             |

---

## 📋 Event Logs

| Action             | CMD                  | PowerShell                                                                                      |
| ------------------ | -------------------- | ----------------------------------------------------------------------------------------------- |
| View system log    | `eventvwr`           | `Get-EventLog -LogName System -Newest 20`                                                       |
| View app log       | —                    | `Get-EventLog -LogName Application -Newest 20`                                                  |
| Filter by event ID | —                    | `Get-EventLog -LogName System -InstanceId 6006`                                                 |
| Filter by source   | —                    | `Get-EventLog -LogName Application -Source "MSSQLSERVER"`                                       |
| Filter by level    | —                    | `Get-EventLog -LogName System -EntryType Error`                                                 |
| Levels             | —                    | `Error`, `Warning`, `Information`, `FailureAudit`, `SuccessAudit`                               |
| Filter by time     | —                    | `Get-EventLog -LogName System -After (Get-Date).AddDays(-1)`                                    |
| Export to CSV      | —                    | `Get-EventLog -LogName System -Newest 100 \| Export-Csv events.csv`                             |
| Clear log          | `wevtutil cl System` | `Clear-EventLog -LogName System`                                                                |
| List all log names | `wevtutil el`        | `Get-EventLog -List`                                                                            |
| Advanced log query | —                    | `Get-WinEvent -FilterHashtable @{LogName='System'; Level=2; StartTime=(Get-Date).AddHours(-1)}` |

---

## 🖥️ Hardware & Drivers

| Action              | CMD                                                         | PowerShell                                       |
| ------------------- | ----------------------------------------------------------- | ------------------------------------------------ |
| List all devices    | `devmgmt.msc`                                               | `Get-PnpDevice`                                  |
| Devices with errors | —                                                           | `Get-PnpDevice \| Where-Object Status -ne OK`    |
| Disable device      | —                                                           | `Disable-PnpDevice -InstanceId <id>`             |
| Enable device       | —                                                           | `Enable-PnpDevice -InstanceId <id>`              |
| Driver list         | `driverquery`                                               | `Get-WmiObject Win32_PnPSignedDriver`            |
| Signed driver list  | `driverquery /si`                                           | —                                                |
| Driver details      | `driverquery /v`                                            | —                                                |
| Export drivers      | `pnputil /export-driver * C:\drivers`                       | —                                                |
| Add driver          | `pnputil /add-driver driver.inf`                            | —                                                |
| Printer list        | `wmic printer list brief`                                   | `Get-Printer`                                    |
| Add printer         | `rundll32 printui.dll,PrintUIEntry /ia /m "DriverName" ...` | `Add-Printer -Name "MyPrinter" -DriverName "HP"` |
| Default printer     | —                                                           | `(Get-Printer \| Where-Object Default).Name`     |
| USB devices         | `wmic path Win32_USBHub get DeviceID`                       | `Get-PnpDevice -Class USB`                       |

---

## 🔋 Power Management

| Action                  | CMD                                               | PowerShell       |
| ----------------------- | ------------------------------------------------- | ---------------- |
| Show power plan         | `powercfg /list`                                  | `powercfg /list` |
| Active power plan       | `powercfg /getactivescheme`                       | —                |
| Set balanced plan       | `powercfg /setactive SCHEME_BALANCED`             | —                |
| Set high performance    | `powercfg /setactive SCHEME_MIN`                  | —                |
| Power efficiency report | `powercfg /energy`                                | —                |
| Battery report          | `powercfg /batteryreport /output C:\battery.html` | —                |
| Sleep report            | `powercfg /sleepstudy`                            | —                |
| Last wake reason        | `powercfg /lastwake`                              | —                |
| Wake timers             | `powercfg /waketimers`                            | —                |
| Set sleep timeout (AC)  | `powercfg /change standby-timeout-ac 30`          | —                |
| Disable sleep           | `powercfg /change standby-timeout-ac 0`           | —                |
| Set hibernate timeout   | `powercfg /change hibernate-timeout-ac 60`        | —                |
| Disable hibernate       | `powercfg /h off`                                 | —                |
| Enable hibernate        | `powercfg /h on`                                  | —                |

---

## 🔁 Redirects, Pipes & Chaining

| Symbol | Meaning                        | Example                          |
| ------ | ------------------------------ | -------------------------------- |
| `>`    | Redirect stdout (overwrite)    | `dir > out.txt`                  |
| `>>`   | Redirect stdout (append)       | `echo hi >> log.txt`             |
| `<`    | Redirect stdin                 | `sort < list.txt`                |
| `\|`   | Pipe output to command         | `tasklist \| findstr chrome`     |
| `2>`   | Redirect stderr                | `cmd 2> err.txt`                 |
| `2>&1` | Merge stderr into stdout       | `cmd > all.txt 2>&1`             |
| `&&`   | Run next if previous succeeded | `mkdir dir && cd dir`            |
| `\|\|` | Run next if previous failed    | `cd dir \|\| mkdir dir`          |
| `&`    | Run sequentially regardless    | `echo a & echo b`                |
| `\`    | Line continuation (PS)         | `Get-Process \`<br> \| Sort CPU` |

### Piping Examples

```cmd
:: CMD
dir /b | sort                          :: Sort file list alphabetically
tasklist | findstr /i "chrome"         :: Filter process list
netstat -an | findstr "LISTENING"      :: Show only listening ports
systeminfo | findstr /c:"OS" /c:"RAM"  :: Extract specific lines
dir /s /b *.log | find /c /v ""       :: Count .log files
```

```powershell
# PowerShell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-Service | Where-Object Status -eq "Stopped" | Select-Object Name
Get-ChildItem -Recurse *.txt | ForEach-Object { Write-Host $_.FullName }
Get-Content log.txt | Select-String "ERROR" | Export-Csv errors.csv
Get-EventLog -LogName System -Newest 50 | Where-Object EntryType -eq Error | Format-Table
```

---

## 📝 Scripting & Automation

### Batch Script (.bat) Fundamentals

```bat
@echo off                             :: Suppress command echo
setlocal                              :: Localize variable changes
set VAR=Hello                         :: Set variable
echo %VAR%                            :: Print variable
set /p INPUT=Enter value:             :: Read user input
set /a RESULT=5+3                     :: Arithmetic

:: Conditionals
if "%VAR%"=="Hello" echo Matched
if not exist file.txt echo Not found
if %ERRORLEVEL% neq 0 exit /b 1

:: Loops
for %%i in (1 2 3) do echo %%i
for /l %%i in (1,1,10) do echo %%i   :: 1 to 10
for /f "tokens=*" %%a in (file.txt) do echo %%a   :: Read file
for /r C:\folder %%f in (*.txt) do echo %%f        :: Recursive

:: Functions (labels)
call :myFunction
goto :eof

:myFunction
echo Inside function
goto :eof

:: Error handling
command || (echo Failed & exit /b 1)

:: Pause and wait
pause                                 :: Press any key
timeout /t 5                          :: Wait 5 seconds
timeout /t 5 /nobreak                 :: Wait silently
```

### PowerShell Script (.ps1) Fundamentals

```powershell
# Variables
$name = "Alice"
$num  = 42
$arr  = @(1, 2, 3)
$hash = @{ Key = "Value"; Num = 10 }

# String interpolation
Write-Host "Hello, $name! You are $($num) years old."

# User input
$input = Read-Host "Enter your name"

# Conditionals
if ($num -gt 10) { "Greater" }
elseif ($num -eq 10) { "Equal" }
else { "Less" }

# Comparison operators
# -eq  -ne  -gt  -lt  -ge  -le  (numbers)
# -like  -match  -contains  -in  (strings/arrays)
# -and  -or  -not  (logical)

# Loops
foreach ($item in $arr) { Write-Host $item }
for ($i = 0; $i -lt 5; $i++) { Write-Host $i }
while ($num -gt 0) { $num--; Write-Host $num }
1..10 | ForEach-Object { Write-Host $_ }

# Functions
function Greet {
    param ([string]$Name = "World")
    Write-Host "Hello, $Name!"
}
Greet -Name "Alice"

# Error handling
try {
    Get-Item "C:\nonexistent" -ErrorAction Stop
} catch {
    Write-Host "Error: $_"
} finally {
    Write-Host "Always runs"
}

# Pipeline
Get-Process | Where-Object CPU -gt 5 | Sort-Object CPU -Descending | Select-Object Name, CPU -First 5

# Working with files
$lines = Get-Content "file.txt"
$lines | Where-Object { $_ -match "error" } | Set-Content "errors.txt"

# Modules
Import-Module ActiveDirectory
Get-Module -ListAvailable | Where-Object Name -like "*Net*"

# Execution policy
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### PowerShell — Common One-Liners

```powershell
# Find large files
Get-ChildItem -Recurse | Sort-Object Length -Descending | Select-Object FullName, @{n='Size(MB)';e={[math]::Round($_.Length/1MB,2)}} -First 20

# Get IP addresses
(Get-NetIPAddress -AddressFamily IPv4).IPAddress

# Kill process using a port
(Get-NetTCPConnection -LocalPort 8080).OwningProcess | ForEach-Object { Stop-Process -Id $_ }

# Uninstall software silently
Get-WmiObject Win32_Product | Where-Object Name -like "*Java*" | Invoke-WmiMethod -Name Uninstall

# Bulk rename files
Get-ChildItem *.txt | Rename-Item -NewName { $_.Name -replace ".txt",".bak" }

# Monitor a log file live
Get-Content C:\app.log -Wait -Tail 20

# Generate random password
-join ((33..126) | Get-Random -Count 16 | ForEach-Object { [char]$_ })

# Check if running as admin
([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)

# Get disk space summary
Get-PSDrive -PSProvider FileSystem | Select-Object Name, @{n='Free(GB)';e={[math]::Round($_.Free/1GB,1)}}, @{n='Used(GB)';e={[math]::Round(($_.Used)/1GB,1)}}

# Count files by extension
Get-ChildItem -Recurse | Group-Object Extension | Sort-Object Count -Descending

# Find and delete temp files
Get-ChildItem $env:TEMP -Recurse -ErrorAction SilentlyContinue | Remove-Item -Recurse -Force -ErrorAction SilentlyContinue
```

---

## ⌨️ Keyboard Shortcuts

### CMD Shortcuts

| Shortcut      | Action                              |
| ------------- | ----------------------------------- |
| `Tab`         | Autocomplete path/command           |
| `Shift + Tab` | Cycle autocomplete backwards        |
| `↑` / `↓`     | Navigate command history            |
| `F1`          | Paste previous command char by char |
| `F3`          | Paste entire previous command       |
| `F7`          | Show popup history list             |
| `F8`          | Search history (type prefix first)  |
| `F9`          | Select command by history number    |
| `Alt + F7`    | Clear history                       |
| `Ctrl + C`    | Cancel running command              |
| `Ctrl + Z`    | End-of-file / Ctrl+Z marker         |
| `Ctrl + V`    | Paste                               |
| `Ctrl + A`    | Select all text                     |
| `Ctrl + Home` | Scroll to top                       |
| `Ctrl + End`  | Scroll to bottom                    |
| `cls`         | Clear screen                        |
| `exit`        | Close window                        |

### PowerShell Shortcuts

| Shortcut                | Action                           |
| ----------------------- | -------------------------------- |
| `Tab`                   | Autocomplete                     |
| `Ctrl + Space`          | Show IntelliSense / completions  |
| `↑` / `↓`               | Command history                  |
| `Ctrl + R`              | Reverse history search           |
| `F8`                    | Search history by current prefix |
| `Ctrl + C`              | Cancel running command           |
| `Ctrl + L`              | Clear screen                     |
| `Ctrl + A`              | Go to beginning of line          |
| `Ctrl + E`              | Go to end of line                |
| `Ctrl + ←` / `Ctrl + →` | Jump word left/right             |
| `Ctrl + Backspace`      | Delete word backwards            |
| `Ctrl + Delete`         | Delete word forwards             |
| `Alt + F7`              | Clear history                    |
| `Get-History`           | Print history list               |
| `Invoke-History 5`      | Re-run command #5                |
| `Clear-History`         | Clear history                    |

### Windows Terminal App Shortcuts

| Shortcut                | Action                  |
| ----------------------- | ----------------------- |
| `Ctrl + Shift + T`      | New tab                 |
| `Ctrl + Shift + W`      | Close tab               |
| `Ctrl + Tab`            | Next tab                |
| `Ctrl + Shift + Tab`    | Previous tab            |
| `Ctrl + Shift + P`      | Command palette         |
| `Ctrl + ,`              | Open settings           |
| `Ctrl + +` / `Ctrl + -` | Zoom in/out             |
| `Ctrl + Shift + F`      | Find                    |
| `Alt + Shift + D`       | Split pane (horizontal) |
| `Alt + Shift + +`       | Split pane (vertical)   |
| `Alt + ←/→/↑/↓`         | Move between panes      |

---

## 📖 Complete CMD Command A–Z

| Command          | Description                                       |
| ---------------- | ------------------------------------------------- |
| `append`         | Set data file search path                         |
| `arp`            | Display/modify ARP cache                          |
| `assoc`          | Display/modify file extension associations        |
| `at`             | Schedule commands (deprecated; use schtasks)      |
| `attrib`         | Display/modify file attributes                    |
| `bcdedit`        | Boot Configuration Data editor                    |
| `break`          | Enable/disable extended CTRL+C checking           |
| `cacls`          | Display/modify file ACLs (deprecated; use icacls) |
| `call`           | Call a batch script as a subroutine               |
| `cd` / `chdir`   | Change directory                                  |
| `chcp`           | Display/set active code page                      |
| `chkdsk`         | Check disk and display status report              |
| `chkntfs`        | Display/modify disk checking at startup           |
| `cipher`         | Encrypt/decrypt files and folders (EFS)           |
| `clip`           | Copy command output to clipboard                  |
| `cls`            | Clear the screen                                  |
| `cmd`            | Start a new CMD instance                          |
| `color`          | Set console foreground/background colors          |
| `comp`           | Compare two files                                 |
| `compact`        | Display/alter compression on NTFS                 |
| `convert`        | Convert FAT volume to NTFS                        |
| `copy`           | Copy files                                        |
| `date`           | Display/set date                                  |
| `del` / `erase`  | Delete files                                      |
| `dir`            | List directory contents                           |
| `diskpart`       | Interactive disk partitioning                     |
| `doskey`         | Command-line editor and macro recorder            |
| `driverquery`    | List installed device drivers                     |
| `echo`           | Print message / toggle command echoing            |
| `endlocal`       | End localization of environment changes           |
| `exit`           | Quit CMD or return error code                     |
| `expand`         | Expand compressed cabinet files                   |
| `fc`             | Compare two files or sets of files                |
| `find`           | Search for text string in files                   |
| `findstr`        | Search using strings or regex in files            |
| `for`            | Run command for set of files/values               |
| `forfiles`       | Select files by date for batch processing         |
| `format`         | Format a disk volume                              |
| `fsutil`         | File system utility                               |
| `ftp`            | File Transfer Protocol client                     |
| `ftype`          | Display/modify file type associations             |
| `goto`           | Jump to labeled line in batch script              |
| `gpresult`       | Display Group Policy results                      |
| `gpupdate`       | Refresh Group Policy settings                     |
| `help`           | List commands or show command help                |
| `hostname`       | Display the computer's hostname                   |
| `icacls`         | Display/modify file ACLs                          |
| `if`             | Conditional processing in batch script            |
| `ipconfig`       | Display/manage IP configuration                   |
| `label`          | Create/change/delete disk volume label            |
| `logman`         | Manage data collector sets / logs                 |
| `md` / `mkdir`   | Create directory                                  |
| `mklink`         | Create symbolic links, hard links, junctions      |
| `mode`           | Configure system devices                          |
| `more`           | Display output one screen at a time               |
| `move`           | Move/rename files                                 |
| `msconfig`       | System configuration tool                         |
| `msiexec`        | Install/configure/remove MSI packages             |
| `net`            | Network services management                       |
| `netsh`          | Network shell configuration                       |
| `netstat`        | Network statistics and connections                |
| `nltest`         | Network diagnostics                               |
| `nslookup`       | DNS lookup tool                                   |
| `openfiles`      | Display files opened by remote users              |
| `path`           | Display/set PATH environment variable             |
| `pathping`       | Trace route with statistics                       |
| `pause`          | Pause batch script and prompt user                |
| `ping`           | Test network connectivity                         |
| `popd`           | Restore previous directory from stack             |
| `powercfg`       | Power configuration utility                       |
| `print`          | Print a text file                                 |
| `prompt`         | Change the CMD prompt string                      |
| `pushd`          | Save current dir and change to new one            |
| `rd` / `rmdir`   | Remove directory                                  |
| `recover`        | Recover readable data from bad sectors            |
| `reg`            | Registry command-line operations                  |
| `ren` / `rename` | Rename files or directories                       |
| `replace`        | Replace files                                     |
| `robocopy`       | Robust file copy utility                          |
| `route`          | Display/modify routing table                      |
| `runas`          | Run a program as a different user                 |
| `sc`             | Service Control — manage services                 |
| `schtasks`       | Create/manage scheduled tasks                     |
| `set`            | Display/set/remove environment variables          |
| `setlocal`       | Begin localization of environment changes         |
| `setx`           | Set environment variables permanently             |
| `sfc`            | System file checker                               |
| `shutdown`       | Shut down or restart computer                     |
| `sort`           | Sort input                                        |
| `start`          | Start a program or command in new window          |
| `subst`          | Associate a path with a drive letter              |
| `systeminfo`     | Display detailed system configuration             |
| `takeown`        | Take ownership of a file or folder                |
| `taskkill`       | Kill running processes                            |
| `tasklist`       | List currently running processes                  |
| `time`           | Display/set the system time                       |
| `timeout`        | Pause processing for N seconds                    |
| `title`          | Set the CMD window title                          |
| `tracert`        | Trace route to a host                             |
| `tree`           | Display directory structure as a tree             |
| `type`           | Display text file contents                        |
| `ver`            | Display Windows version                           |
| `verify`         | Verify files are written correctly                |
| `vol`            | Display disk volume label and serial number       |
| `wbadmin`        | Windows Backup administrator                      |
| `where`          | Find location of files in PATH                    |
| `whoami`         | Display current user info                         |
| `wmic`           | WMI command-line interface                        |
| `xcopy`          | Copy files and directory trees                    |

---

## 📖 Complete PowerShell Cmdlet A–Z

### By Category

#### Aliases

```powershell
Get-Alias              # List all aliases
Set-Alias ll Get-ChildItem  # Create alias
New-Alias touch New-Item    # Create new alias
Remove-Alias ll             # Remove alias
Export-Alias aliases.csv    # Export aliases
Import-Alias aliases.csv    # Import aliases
```

#### Archives & Compression

```powershell
Compress-Archive -Path C:\folder -DestinationPath archive.zip
Compress-Archive -Path * -DestinationPath out.zip -Update
Expand-Archive -Path archive.zip -DestinationPath C:\out
Expand-Archive archive.zip -Force   # Overwrite existing
```

#### CSV / JSON / XML

```powershell
# CSV
Import-Csv data.csv
Export-Csv -Path out.csv -NoTypeInformation
ConvertFrom-Csv $rawData

# JSON
Get-Content data.json | ConvertFrom-Json
$obj | ConvertTo-Json | Set-Content out.json
$obj | ConvertTo-Json -Depth 5 | Out-File out.json

# XML
[xml]$xml = Get-Content data.xml
$xml.Save("out.xml")
$obj | Export-Clixml backup.xml
Import-Clixml backup.xml
```

#### Dates & Time

```powershell
Get-Date                          # Current date/time
Get-Date -Format "yyyy-MM-dd"     # Formatted date
(Get-Date).AddDays(7)             # 7 days from now
(Get-Date).AddHours(-3)           # 3 hours ago
New-TimeSpan -Start $d1 -End $d2  # Difference between dates
Measure-Command { command }       # Time a command
```

#### Error Handling

```powershell
$ErrorActionPreference = "Stop"        # Stop on all errors
Get-Item x -ErrorAction SilentlyContinue  # Ignore error
$error[0]                              # Last error
$error.Clear()                         # Clear error list
Write-Error "Custom error message"
throw "Fatal error"
```

#### Formatting Output

```powershell
Format-Table               # Table view
Format-List                # List view
Format-Wide                # Wide view
Format-Custom              # Custom view
Out-File output.txt        # Write to file
Out-GridView               # GUI grid popup
Out-Null                   # Discard output
Out-String                 # Convert to string
Out-Host                   # Force console output
Write-Host "text"          # Print to console
Write-Output "text"        # Send down pipeline
Write-Verbose "debug"      # Verbose output
Write-Warning "warn"       # Warning output
Write-Error "error"        # Error output
Write-Debug "debug"        # Debug output
```

#### Jobs (Background)

```powershell
Start-Job { Get-Process }          # Start background job
Get-Job                            # List jobs
Receive-Job -Id 1                  # Get job output
Wait-Job -Id 1                     # Wait for job
Stop-Job -Id 1                     # Stop job
Remove-Job -Id 1                   # Remove job
Invoke-Command -ComputerName srv1 -ScriptBlock { Get-Process }  # Remote job
```

#### Math & Numbers

```powershell
[math]::Round(3.14159, 2)     # Round to 2 decimals
[math]::Floor(3.9)            # Floor
[math]::Ceiling(3.1)          # Ceiling
[math]::Abs(-5)               # Absolute value
[math]::Sqrt(16)              # Square root
[math]::Pow(2,10)             # Power
[math]::PI                    # Pi constant
Get-Random                    # Random number
Get-Random -Minimum 1 -Maximum 100  # Random in range
```

#### Modules

```powershell
Get-Module                           # Loaded modules
Get-Module -ListAvailable            # All available modules
Import-Module ActiveDirectory        # Load module
Remove-Module ActiveDirectory        # Unload module
Install-Module -Name PSReadLine      # Install from gallery
Update-Module PSReadLine             # Update module
Uninstall-Module PSReadLine          # Remove module
Find-Module -Name *network*          # Search gallery
Get-Command -Module ActiveDirectory  # Commands in module
New-ModuleManifest -Path my.psd1     # Create module manifest
```

#### Objects & Pipeline

```powershell
Select-Object Name,CPU              # Select properties
Select-Object -First 10             # First N items
Select-Object -Last 5               # Last N items
Select-Object -Unique               # Remove duplicates
Select-Object -ExpandProperty Name  # Get value of property
Where-Object { $_.CPU -gt 5 }       # Filter objects
ForEach-Object { $_ * 2 }           # Transform each
Sort-Object Name                    # Sort ascending
Sort-Object CPU -Descending         # Sort descending
Group-Object Extension              # Group by property
Measure-Object -Sum Length          # Sum/avg/count
Compare-Object $a $b                # Diff two sets
Tee-Object -FilePath out.txt        # Fork pipeline to file
```

#### Processes (Extended)

```powershell
Get-Process                             # All processes
Get-Process -Name chrome                # By name
Get-Process -Id 1234                    # By PID
Start-Process notepad -Wait             # Wait for exit
Start-Process notepad -PassThru         # Return object
(Start-Process cmd -PassThru).Id        # Get PID
Stop-Process -Name chrome -Force
Stop-Process -Id 1234
Wait-Process -Id 1234 -Timeout 30
Debug-Process -Name notepad
Get-Process | Measure-Object WS -Sum   # Total RAM usage
```

#### Remote Management

```powershell
Enter-PSSession -ComputerName server1          # Interactive remote session
Exit-PSSession                                 # Leave session
Invoke-Command -ComputerName srv1 { command }  # Run command remotely
New-PSSession -ComputerName srv1               # Persistent session
Get-PSSession                                  # List sessions
Remove-PSSession -Id 1                         # Remove session
Copy-Item file.txt -Destination \\srv1\C$\     # Copy to remote
Enable-PSRemoting -Force                       # Enable WinRM
Test-WsMan -ComputerName srv1                  # Test WinRM
```

#### Strings

```powershell
"Hello".ToUpper()
"Hello".ToLower()
"Hello".Length
"Hello World".Split(" ")
"Hello".Replace("H","J")
"Hello World".Substring(6)
"Hello World".Contains("World")
"Hello World".StartsWith("Hello")
"Hello World".Trim()
"  spaces  ".TrimStart().TrimEnd()
[string]::Join(",", @("a","b","c"))
"text" -match "regex"          # Regex test
"text" -replace "old","new"    # Regex replace
-join ("a","b","c")            # Concatenate array
```

#### Security & Credentials

```powershell
Get-Credential                                       # GUI credential prompt
$cred = Get-Credential -UserName "admin"
ConvertTo-SecureString "pass" -AsPlainText -Force    # To secure string
ConvertFrom-SecureString $secureStr                  # To encrypted string
Get-Acl C:\folder                                    # Get ACL
Set-Acl C:\folder $acl                               # Set ACL
Test-Path Cert:\CurrentUser\My                       # Certificate store
Get-ChildItem Cert:\CurrentUser\My                   # List certificates
```

#### Variables & Types

```powershell
$var = "value"                # String
[int]$num = 42                # Typed variable
[bool]$flag = $true           # Boolean
[array]$arr = @(1,2,3)        # Array
[hashtable]$h = @{}           # Hashtable
$null                         # Null value
$true / $false                # Boolean literals
$_                            # Current pipeline object
$?                            # Success of last command
$LASTEXITCODE                 # Exit code of last native cmd
$PSVersionTable               # PowerShell version info
$Host                         # Current host info
$args                         # Script arguments array
```

---

## 🔧 WMIC Quick Reference

```cmd
wmic cpu get name,numberofcores,maxclockspeed
wmic memorychip get capacity,speed
wmic diskdrive get model,size,status
wmic logicaldisk get caption,size,freespace,filesystem
wmic bios get smbiosbiosversion,serialnumber
wmic baseboard get manufacturer,product
wmic os get caption,version,buildnumber,osarchitecture
wmic process get name,processid,commandline
wmic process where name="chrome.exe" get processid
wmic process where processid=1234 delete
wmic product get name,version,vendor
wmic product where name="AppName" call uninstall
wmic startup list full
wmic service get name,state,startmode
wmic service where name="Spooler" call startservice
wmic useraccount list brief
wmic nicconfig get ipaddress,defaultipgateway,macaddress
wmic path win32_networkadapter get name,macaddress
```

---

## 🧪 NETSH Quick Reference

```cmd
netsh int ip reset                     :: Reset TCP/IP
netsh winsock reset                    :: Reset Winsock
netsh advfirewall show allprofiles     :: Show firewall rules
netsh advfirewall set allprofiles state off  :: Disable firewall
netsh advfirewall set allprofiles state on   :: Enable firewall
netsh advfirewall firewall show rule name=all
netsh advfirewall firewall add rule name="MyRule" dir=in action=allow protocol=tcp localport=8080
netsh advfirewall firewall delete rule name="MyRule"
netsh wlan show profiles               :: Wi-Fi profiles
netsh wlan show profile name="SSID" key=clear  :: Wi-Fi password
netsh wlan connect name="SSID"        :: Connect to Wi-Fi
netsh wlan disconnect                  :: Disconnect Wi-Fi
netsh interface show interface         :: All adapters
netsh interface set interface "Ethernet" disable
netsh interface set interface "Ethernet" enable
netsh interface ip set address "Ethernet" static 192.168.1.10 255.255.255.0 192.168.1.1
netsh interface ip set address "Ethernet" dhcp
netsh interface ip set dns "Ethernet" static 8.8.8.8
```

---

_Last updated: May 2026 | Windows CMD & PowerShell — Complete Reference_
