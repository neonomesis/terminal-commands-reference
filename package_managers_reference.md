# Package Managers Reference

A comprehensive guide to package managers across macOS, Windows, and Linux.

---

## macOS

### Homebrew

The most popular package manager for macOS.

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Common commands
brew install <package>          # Install a package
brew uninstall <package>        # Remove a package
brew update                     # Update Homebrew itself
brew upgrade                    # Upgrade all packages
brew upgrade <package>          # Upgrade a specific package
brew list                       # List installed packages
brew search <package>           # Search for a package
brew info <package>             # Show package info
brew doctor                     # Check for issues
brew cleanup                    # Remove old versions
brew tap <user/repo>            # Add a third-party repository
brew untap <user/repo>          # Remove a repository
brew services list              # List background services
brew services start <service>   # Start a service
brew services stop <service>    # Stop a service
brew services restart <service> # Restart a service
```

### Homebrew Cask (GUI Apps)

Extension of Homebrew for macOS GUI applications.

```bash
brew install --cask <app>       # Install a GUI app
brew uninstall --cask <app>     # Remove a GUI app
brew list --cask                # List installed cask apps
brew upgrade --cask             # Upgrade all cask apps
brew search --cask <app>        # Search for cask apps
```

### MacPorts

Alternative to Homebrew, uses a different approach.

```bash
# Install from: https://www.macports.org/install.php

sudo port install <package>     # Install a package
sudo port uninstall <package>   # Remove a package
sudo port selfupdate            # Update MacPorts itself
sudo port upgrade outdated      # Upgrade all packages
sudo port list installed        # List installed packages
sudo port search <package>      # Search for a package
sudo port info <package>        # Show package info
sudo port clean --all installed # Clean build files
```

### pip (Python)

```bash
pip install <package>           # Install a package
pip uninstall <package>         # Remove a package
pip install --upgrade <package> # Upgrade a package
pip list                        # List installed packages
pip show <package>              # Show package info
pip freeze > requirements.txt   # Export installed packages
pip install -r requirements.txt # Install from requirements file
pip search <package>            # Search (deprecated in newer pip)
```

### npm / npx (Node.js)

```bash
npm install <package>           # Install locally
npm install -g <package>        # Install globally
npm uninstall <package>         # Remove a package
npm update                      # Update all packages
npm list                        # List installed packages
npm list -g                     # List global packages
npm outdated                    # Show outdated packages
npm init                        # Create package.json
npm run <script>                # Run a script from package.json
npx <package>                   # Run a package without installing
```

### yarn

```bash
yarn add <package>              # Install a package
yarn remove <package>           # Remove a package
yarn upgrade                    # Upgrade all packages
yarn global add <package>       # Install globally
yarn list                       # List installed packages
yarn init                       # Create package.json
yarn install                    # Install from yarn.lock
```

---

## Windows

### Winget (Windows Package Manager)

Built-in package manager starting from Windows 10 (build 1709+).

```powershell
# Install Winget — comes pre-installed on Windows 11
# On Windows 10: install via Microsoft Store (App Installer)

winget install <package>        # Install a package
winget uninstall <package>      # Remove a package
winget upgrade <package>        # Upgrade a specific package
winget upgrade --all            # Upgrade all packages
winget list                     # List installed packages
winget search <package>         # Search for a package
winget show <package>           # Show package info
winget source list              # List package sources
winget source add <name> <url>  # Add a package source
winget export -o packages.json  # Export installed packages
winget import -i packages.json  # Import and install packages
```

### Chocolatey

Popular community-driven package manager for Windows.

```powershell
# Install Chocolatey (run as Administrator)
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Common commands (run as Administrator)
choco install <package>         # Install a package
choco uninstall <package>       # Remove a package
choco upgrade <package>         # Upgrade a package
choco upgrade all               # Upgrade all packages
choco list --local-only         # List installed packages
choco search <package>          # Search for a package
choco info <package>            # Show package info
choco outdated                  # Show outdated packages
choco pin add -n <package>      # Pin a package version
choco pin remove -n <package>   # Unpin a package
```

### Scoop

Command-line installer focused on dev tools, no admin required.

```powershell
# Install Scoop
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex

# Common commands
scoop install <package>         # Install a package
scoop uninstall <package>       # Remove a package
scoop update *                  # Update all packages
scoop update <package>          # Update a specific package
scoop list                      # List installed packages
scoop search <package>          # Search for a package
scoop info <package>            # Show package info
scoop bucket list               # List buckets (repos)
scoop bucket add <bucket>       # Add a bucket
scoop cleanup *                 # Remove old versions
scoop status                    # Show outdated packages
```

### pip (Python) — same as macOS

```powershell
pip install <package>
pip uninstall <package>
pip list
pip freeze > requirements.txt
pip install -r requirements.txt
```

### npm / yarn — same as macOS

```powershell
npm install <package>
npm install -g <package>
yarn add <package>
```

### NuGet (.NET)

```powershell
nuget install <package>         # Install a package
nuget update <package>          # Update a package
nuget list                      # List packages
nuget push <package>.nupkg      # Publish a package
dotnet add package <package>    # Add to a .NET project
dotnet remove package <package> # Remove from a .NET project
dotnet list package             # List project packages
dotnet restore                  # Restore packages
```

---

## Linux

### apt / apt-get (Debian, Ubuntu, Mint)

```bash
sudo apt update                         # Refresh package list
sudo apt upgrade                        # Upgrade all packages
sudo apt install <package>              # Install a package
sudo apt remove <package>               # Remove a package (keep config)
sudo apt purge <package>                # Remove package + config files
sudo apt autoremove                     # Remove unused dependencies
sudo apt search <package>               # Search for a package
apt show <package>                      # Show package info
sudo apt list --installed               # List installed packages
sudo apt-cache depends <package>        # Show dependencies
sudo add-apt-repository <ppa>           # Add a PPA repository
sudo apt-get install --reinstall <pkg>  # Reinstall a package
sudo apt clean                          # Clear package cache
sudo apt autoclean                      # Remove old cached packages
```

### dnf / yum (Fedora, RHEL, CentOS)

```bash
sudo dnf install <package>      # Install a package
sudo dnf remove <package>       # Remove a package
sudo dnf update                 # Update all packages
sudo dnf upgrade <package>      # Upgrade a specific package
sudo dnf search <package>       # Search for a package
sudo dnf info <package>         # Show package info
sudo dnf list installed         # List installed packages
sudo dnf autoremove             # Remove unused dependencies
sudo dnf clean all              # Clear cache
sudo dnf repolist               # List repositories
sudo dnf group list             # List package groups
sudo dnf group install "<group>"# Install a package group
sudo dnf history                # Show transaction history
sudo dnf history undo <id>      # Undo a transaction
```

### pacman (Arch Linux, Manjaro)

```bash
sudo pacman -S <package>        # Install a package
sudo pacman -R <package>        # Remove a package
sudo pacman -Rs <package>       # Remove package + unused deps
sudo pacman -Syu                # Update system (sync + upgrade)
sudo pacman -Sy                 # Sync package database
sudo pacman -Su                 # Upgrade installed packages
sudo pacman -Ss <package>       # Search for a package
sudo pacman -Si <package>       # Show remote package info
sudo pacman -Qi <package>       # Show local package info
sudo pacman -Ql <package>       # List package files
sudo pacman -Qe                 # List explicitly installed packages
sudo pacman -Qdt                # List orphan packages
sudo pacman -Sc                 # Clear package cache
sudo pacman -U <file.pkg.tar>   # Install from local file
```

### yay / paru (AUR helpers for Arch)

```bash
yay -S <package>                # Install from AUR
yay -R <package>                # Remove a package
yay -Syu                        # Update system including AUR
yay -Ss <package>               # Search AUR and repos
yay -Yc                         # Remove unneeded dependencies

paru -S <package>               # Install from AUR
paru -Syu                       # Update system including AUR
paru -Ss <package>              # Search AUR and repos
```

### zypper (openSUSE)

```bash
sudo zypper install <package>   # Install a package
sudo zypper remove <package>    # Remove a package
sudo zypper update              # Update all packages
sudo zypper refresh             # Refresh repositories
sudo zypper search <package>    # Search for a package
sudo zypper info <package>      # Show package info
sudo zypper repos               # List repositories
sudo zypper addrepo <url> <name># Add a repository
sudo zypper clean               # Clear cache
```

### snap (Ubuntu, many distros)

```bash
snap install <package>          # Install a snap package
snap install --classic <pkg>    # Install with classic confinement
snap remove <package>           # Remove a package
snap refresh                    # Update all snaps
snap refresh <package>          # Update a specific snap
snap list                       # List installed snaps
snap find <package>             # Search for a package
snap info <package>             # Show snap info
snap revert <package>           # Revert to previous version
snap connections <package>      # Show snap interfaces
```

### flatpak (universal Linux)

```bash
flatpak install <remote> <app>          # Install an app
flatpak install flathub <app>           # Install from Flathub
flatpak uninstall <app>                 # Remove an app
flatpak update                          # Update all apps
flatpak list                            # List installed apps
flatpak search <app>                    # Search for an app
flatpak info <app>                      # Show app info
flatpak remote-list                     # List remotes (repos)
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak run <app>                       # Run an app
flatpak override --filesystem=home <app># Grant filesystem access
```

### rpm (Red Hat, Fedora, CentOS — low level)

```bash
rpm -i <package>.rpm            # Install a package
rpm -U <package>.rpm            # Upgrade a package
rpm -e <package>                # Remove a package
rpm -q <package>                # Query if package is installed
rpm -qa                         # List all installed packages
rpm -ql <package>               # List files in package
rpm -qi <package>               # Show package info
rpm -qf <file>                  # Find which package owns a file
rpm --checksig <package>.rpm    # Verify package signature
```

---

## Language-Specific Package Managers (Cross-Platform)

| Language | Tool       | Install Command            | Config File      |
| -------- | ---------- | -------------------------- | ---------------- |
| Node.js  | npm        | `npm install <pkg>`        | package.json     |
| Node.js  | yarn       | `yarn add <pkg>`           | yarn.lock        |
| Node.js  | pnpm       | `pnpm add <pkg>`           | pnpm-lock.yaml   |
| Node.js  | bun        | `bun add <pkg>`            | bun.lockb        |
| Python   | pip        | `pip install <pkg>`        | requirements.txt |
| Python   | poetry     | `poetry add <pkg>`         | pyproject.toml   |
| Python   | conda      | `conda install <pkg>`      | environment.yml  |
| Python   | uv         | `uv add <pkg>`             | pyproject.toml   |
| Rust     | cargo      | `cargo add <pkg>`          | Cargo.toml       |
| Go       | go modules | `go get <pkg>`             | go.mod           |
| Ruby     | gem        | `gem install <pkg>`        | Gemfile          |
| Ruby     | bundler    | `bundle add <pkg>`         | Gemfile.lock     |
| PHP      | composer   | `composer require <pkg>`   | composer.json    |
| Java     | maven      | add to pom.xml             | pom.xml          |
| Java     | gradle     | add to build.gradle        | build.gradle     |
| .NET/C#  | nuget      | `dotnet add package <pkg>` | .csproj          |
| Swift    | swift pm   | add to Package.swift       | Package.swift    |
| Dart     | pub        | `dart pub add <pkg>`       | pubspec.yaml     |

---

## Quick Comparison

| Feature            | Homebrew (mac) | Winget (win) | Chocolatey (win) | apt (linux) | pacman (linux) |
| ------------------ | :------------: | :----------: | :--------------: | :---------: | :------------: |
| GUI apps           |   Yes (cask)   |     Yes      |       Yes        |   Limited   |    Limited     |
| Dev tools          |      Yes       |     Yes      |       Yes        |     Yes     |      Yes       |
| No admin required  |      Yes       |     Yes      |        No        |     No      |       No       |
| Community packages |      Yes       |     Yes      |       Yes        |     Yes     |   Yes (AUR)    |
| Rollback support   |    Partial     |      No      |       Yes        |     No      |      Yes       |
| Auto-updates       |     Manual     |     Yes      |      Manual      |   Manual    |     Manual     |
