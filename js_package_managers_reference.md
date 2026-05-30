# JavaScript / Node.js Package Managers Reference

Comprehensive command reference for npm, yarn, pnpm, bun, and more.

---

## npm (Node Package Manager)
Comes bundled with Node.js. The default and most widely used.

### Installation
```bash
# Comes with Node.js — check version
npm --version
node --version

# Update npm itself
npm install -g npm@latest
```

### Init / Setup
```bash
npm init                        # Interactive project setup
npm init -y                     # Skip prompts, use defaults
npm init --scope=@myorg         # Scoped package setup
```

### Installing Packages
```bash
npm install                     # Install all from package.json
npm install <package>           # Install and save to dependencies
npm install <package>@1.2.3     # Install specific version
npm install <package>@latest    # Install latest version
npm install <package>@^1.0.0    # Install with version range
npm install -D <package>        # Save to devDependencies
npm install -g <package>        # Install globally
npm install --save-optional <pkg> # Save to optionalDependencies
npm install --save-peer <pkg>   # Save to peerDependencies
npm install <folder>            # Install from local folder
npm install <tarball>           # Install from tarball file
npm install <git-url>           # Install from git repo
npm ci                          # Clean install (from lock file only)
```

### Removing Packages
```bash
npm uninstall <package>         # Remove from dependencies
npm uninstall -D <package>      # Remove from devDependencies
npm uninstall -g <package>      # Remove global package
npm prune                       # Remove packages not in package.json
npm prune --production          # Remove devDependencies
```

### Updating Packages
```bash
npm update                      # Update all packages
npm update <package>            # Update specific package
npm outdated                    # Show outdated packages
npm install <package>@latest    # Force update to latest
```

### Running Scripts
```bash
npm run <script>                # Run a script from package.json
npm start                       # Run the "start" script
npm test                        # Run the "test" script
npm run build                   # Run the "build" script
npm run dev                     # Run the "dev" script
npm run --if-present <script>   # Run only if script exists
```

### Listing & Info
```bash
npm list                        # List installed packages (local)
npm list -g                     # List global packages
npm list --depth=0              # List top-level packages only
npm show <package>              # Show package metadata
npm show <package> versions     # Show all available versions
npm view <package> version      # Show latest version
npm ls <package>                # Check if package is installed
```

### Publishing
```bash
npm login                       # Log in to npm registry
npm logout                      # Log out
npm whoami                      # Show logged-in user
npm publish                     # Publish package
npm publish --access public     # Publish as public scoped package
npm version patch               # Bump patch version (1.0.0 → 1.0.1)
npm version minor               # Bump minor version (1.0.0 → 1.1.0)
npm version major               # Bump major version (1.0.0 → 2.0.0)
npm deprecate <pkg>@<ver> "msg" # Deprecate a version
npm unpublish <package>@<ver>   # Unpublish a version (72h limit)
```

### Cache & Misc
```bash
npm cache clean --force         # Clear the cache
npm cache verify                # Verify cache integrity
npm audit                       # Check for vulnerabilities
npm audit fix                   # Auto-fix vulnerabilities
npm audit fix --force           # Force fix (may break things)
npm dedupe                      # Reduce duplication in node_modules
npm pack                        # Create a tarball of the package
npm link                        # Symlink local package globally
npm link <package>              # Link a global package locally
npm exec <command>              # Run a command from a package
npx <package>                   # Run package without installing
npm config list                 # Show npm config
npm config set <key> <value>    # Set a config value
npm config get <key>            # Get a config value
npm config delete <key>         # Delete a config value
```

---

## yarn (v1 Classic)
Facebook's alternative to npm with deterministic installs.

### Installation
```bash
npm install -g yarn
yarn --version
```

### Init / Setup
```bash
yarn init                       # Interactive setup
yarn init -y                    # Skip prompts
```

### Installing Packages
```bash
yarn                            # Install all from package.json
yarn install                    # Same as above
yarn install --frozen-lockfile  # Fail if yarn.lock needs update (CI)
yarn add <package>              # Add to dependencies
yarn add <package>@1.2.3        # Add specific version
yarn add <package>@latest       # Add latest version
yarn add -D <package>           # Add to devDependencies
yarn add -P <package>           # Add to peerDependencies
yarn add -O <package>           # Add to optionalDependencies
yarn global add <package>       # Install globally
yarn add <package> --exact      # Install exact version (no ^ or ~)
yarn add file:<path>            # Install from local path
```

### Removing Packages
```bash
yarn remove <package>           # Remove a package
yarn global remove <package>    # Remove a global package
```

### Updating Packages
```bash
yarn upgrade                    # Upgrade all packages
yarn upgrade <package>          # Upgrade specific package
yarn upgrade <package>@latest   # Upgrade to latest
yarn upgrade-interactive        # Interactive upgrade UI
yarn upgrade-interactive --latest # Interactive with latest versions
yarn outdated                   # Show outdated packages
```

### Running Scripts
```bash
yarn <script>                   # Run a script (no "run" needed for custom)
yarn run <script>               # Run a script explicitly
yarn start                      # Run "start"
yarn test                       # Run "test"
yarn build                      # Run "build"
yarn dev                        # Run "dev"
```

### Listing & Info
```bash
yarn list                       # List all installed packages
yarn list --depth=0             # List top-level only
yarn global list                # List global packages
yarn info <package>             # Show package info
yarn info <package> version     # Show latest version
yarn why <package>              # Explain why package is installed
```

### Publishing
```bash
yarn login                      # Log in to npm registry
yarn logout                     # Log out
yarn whoami                     # Show logged-in user
yarn publish                    # Publish package
yarn version --patch            # Bump patch version
yarn version --minor            # Bump minor version
yarn version --major            # Bump major version
```

### Cache & Misc
```bash
yarn cache list                 # Show cached packages
yarn cache clean                # Clear cache
yarn cache dir                  # Show cache directory
yarn audit                      # Check vulnerabilities
yarn audit --groups dependencies # Audit only production deps
yarn dedupe                     # Deduplicate packages
yarn link                       # Symlink package
yarn link <package>             # Use linked package
yarn unlink <package>           # Remove link
yarn workspaces info            # Show workspace info
yarn config list                # Show config
yarn config set <key> <value>   # Set config
yarn config get <key>           # Get config
```

---

## yarn (v2/v3/v4 — Berry)
Modern rewrite of yarn with Plug'n'Play and zero-installs.

### Installation
```bash
# Enable via Corepack (Node.js 16.10+)
corepack enable
corepack prepare yarn@stable --activate

yarn --version                  # Should show 2.x / 3.x / 4.x
```

### Key Differences from v1
```bash
yarn set version stable         # Update to latest stable
yarn set version berry          # Switch to berry
yarn set version classic        # Switch back to v1

# PnP mode (default) — no node_modules folder
yarn install                    # Installs via PnP

# node_modules mode (optional)
# Add to .yarnrc.yml: nodeLinker: node-modules
```

### Init / Setup
```bash
yarn init -2                    # Init with yarn v2+
```

### Common Commands (same as v1, with additions)
```bash
yarn add <package>
yarn remove <package>
yarn up <package>               # Upgrade (replaces "upgrade")
yarn up <package>@latest        # Upgrade to latest
yarn up "*"                     # Upgrade all packages
yarn dlx <package>              # Run a package (replaces npx)
yarn exec <command>             # Run a command in project context
yarn workspaces foreach <cmd>   # Run command in all workspaces
yarn workspaces list            # List workspaces
yarn plugin list                # List installed plugins
yarn plugin import <name>       # Add a plugin
```

---

## pnpm
Fast, disk-efficient package manager using a content-addressable store.

### Installation
```bash
# Via npm
npm install -g pnpm

# Via Corepack
corepack enable
corepack prepare pnpm@latest --activate

# Via standalone script (macOS/Linux)
curl -fsSL https://get.pnpm.io/install.sh | sh -

# Via PowerShell (Windows)
iwr https://get.pnpm.io/install.ps1 -useb | iex

pnpm --version
```

### Init / Setup
```bash
pnpm init                       # Create package.json
```

### Installing Packages
```bash
pnpm install                    # Install all from package.json
pnpm install --frozen-lockfile  # CI install (no lockfile changes)
pnpm add <package>              # Add to dependencies
pnpm add <package>@1.2.3        # Add specific version
pnpm add <package>@latest       # Add latest version
pnpm add -D <package>           # Add to devDependencies
pnpm add -g <package>           # Install globally
pnpm add -P <package>           # Add to peerDependencies
pnpm add -O <package>           # Add to optionalDependencies
pnpm add --save-exact <package> # Pin exact version
pnpm add <folder>               # Install from local folder
pnpm fetch                      # Fetch packages to virtual store (offline)
```

### Removing Packages
```bash
pnpm remove <package>           # Remove a package
pnpm remove -g <package>        # Remove a global package
```

### Updating Packages
```bash
pnpm update                     # Update all packages
pnpm update <package>           # Update specific package
pnpm update <package>@latest    # Update to latest (ignores ranges)
pnpm update --latest            # Update all ignoring version ranges
pnpm update -i                  # Interactive update
pnpm update -i --latest         # Interactive update to latest
pnpm outdated                   # Show outdated packages
```

### Running Scripts
```bash
pnpm <script>                   # Run a script
pnpm run <script>               # Run a script explicitly
pnpm start                      # Run "start"
pnpm test                       # Run "test"
pnpm build                      # Run "build"
pnpm dev                        # Run "dev"
pnpm run --filter <pkg> <script># Run script in specific workspace
```

### Listing & Info
```bash
pnpm list                       # List installed packages
pnpm list --depth=0             # Top-level only
pnpm list -g                    # List global packages
pnpm why <package>              # Explain why package is installed
pnpm view <package>             # Show package info
pnpm view <package> versions    # Show all versions
```

### Workspaces (Monorepo)
```bash
# pnpm-workspace.yaml required
pnpm -r <command>               # Run in all workspace packages
pnpm --filter <pkg> <command>   # Run in specific package
pnpm --filter "./packages/**" add <dep> # Add dep to all packages
pnpm -r update                  # Update all workspace packages
pnpm -r exec -- <command>       # Execute shell command in all packages
```

### Store & Cache
```bash
pnpm store status               # Show store status
pnpm store path                 # Show store location
pnpm store prune                # Remove unreferenced packages from store
pnpm cache list                 # List cached metadata
pnpm cache delete               # Delete cached metadata
```

### Publishing & Misc
```bash
pnpm publish                    # Publish package
pnpm pack                       # Create tarball
pnpm audit                      # Check vulnerabilities
pnpm audit --fix                # Fix vulnerabilities
pnpm dedupe                     # Deduplicate lockfile entries
pnpm link                       # Symlink package
pnpm link <dir>                 # Link from directory
pnpm dlx <package>              # Run package without installing (like npx)
pnpm exec <command>             # Run command in project context
pnpm config list                # Show config
pnpm config set <key> <value>   # Set config
pnpm config get <key>           # Get config
pnpm config delete <key>        # Delete config
pnpm env use --global <version> # Use a specific Node.js version
pnpm env list                   # List available Node.js versions
```

---

## bun
All-in-one JavaScript runtime + package manager. Extremely fast.

### Installation
```bash
# macOS / Linux
curl -fsSL https://bun.sh/install | bash

# Windows (PowerShell)
powershell -c "irm bun.sh/install.ps1 | iex"

# Via npm
npm install -g bun

bun --version
bun upgrade                     # Update bun itself
```

### Init / Setup
```bash
bun init                        # Initialize a project
bun init -y                     # Skip prompts
bun create <template>           # Create project from template
bun create react-app .          # Create React app
bun create next .               # Create Next.js app
```

### Installing Packages
```bash
bun install                     # Install all from package.json
bun install --frozen-lockfile   # CI install (fail if lockfile changes)
bun add <package>               # Add to dependencies
bun add <package>@1.2.3         # Add specific version
bun add <package>@latest        # Add latest version
bun add -d <package>            # Add to devDependencies
bun add -g <package>            # Install globally
bun add --optional <package>    # Add to optionalDependencies
bun add --exact <package>       # Pin exact version
bun add <folder>                # Install from local folder
bun add <git-url>               # Install from git
```

### Removing Packages
```bash
bun remove <package>            # Remove a package
bun remove -g <package>         # Remove a global package
```

### Updating Packages
```bash
bun update                      # Update all packages
bun update <package>            # Update specific package
bun outdated                    # Show outdated packages
```

### Running Scripts
```bash
bun run <script>                # Run a script from package.json
bun run start                   # Run "start"
bun run test                    # Run "test"
bun run build                   # Run "build"
bun run dev                     # Run "dev"
bun <file>                      # Run a JS/TS file directly
bun --hot <file>                # Run with hot reload
bun --watch <file>              # Run with file watcher
```

### Running Without Installing
```bash
bunx <package>                  # Run a package (like npx)
bunx --bun <package>            # Force run with bun runtime
```

### Bun as a Runtime
```bash
bun <file>.ts                   # Run TypeScript directly (no compile)
bun <file>.js                   # Run JavaScript
bun repl                        # Start REPL
bun build <file> --outdir dist  # Bundle files
bun build --target browser      # Bundle for browser
bun build --target node         # Bundle for Node.js
bun build --minify              # Minify output
bun build --sourcemap           # Generate source maps
```

### Testing
```bash
bun test                        # Run all tests
bun test <file>                 # Run specific test file
bun test --watch                # Run tests in watch mode
bun test --coverage             # Run with coverage report
bun test -t "<pattern>"         # Run tests matching pattern
bun test --timeout 10000        # Set test timeout (ms)
```

### Workspaces
```bash
# Define in package.json: "workspaces": ["packages/*"]
bun install                     # Installs all workspaces
bun run --filter <pkg> <script> # Run script in specific workspace
```

### Misc
```bash
bun pm ls                       # List installed packages
bun pm hash                     # Hash the lockfile
bun pm cache rm                 # Clear package cache
bun pm bin                      # Show path to installed binaries
bun link                        # Link package globally
bun link <package>              # Use linked package
bun unlink                      # Remove global link
bun audit                       # Check vulnerabilities (bun 1.x+)
bun publish                     # Publish to npm registry
bun pack                        # Create a tarball
```

---

## Corepack
Node.js built-in tool to manage package manager versions per project.

```bash
# Enable Corepack (Node.js 16.10+)
corepack enable                 # Enable corepack shims

# Prepare specific versions
corepack prepare yarn@stable --activate
corepack prepare pnpm@latest --activate
corepack prepare yarn@3.6.4 --activate

# Use specific version for a project
corepack use yarn@4             # Set yarn version in package.json
corepack use pnpm@8             # Set pnpm version in package.json

# Disable
corepack disable
```

### packageManager field in package.json
```json
{
  "packageManager": "pnpm@8.15.0",
  "packageManager": "yarn@4.1.0",
  "packageManager": "bun@1.0.0"
}
```

---

## npx / bunx / pnpm dlx / yarn dlx
Run packages without installing them globally.

```bash
# npm
npx <package>                   # Run a package
npx <package>@latest            # Run latest version
npx -y <package>                # Auto-confirm install
npx --no-install <package>      # Run only if already cached
npx --package=<pkg> <command>   # Run specific command from package

# bun
bunx <package>                  # Run a package with bun

# pnpm
pnpm dlx <package>              # Run a package with pnpm

# yarn v2+
yarn dlx <package>              # Run a package with yarn
```

---

## Lockfiles Reference

| Package Manager | Lockfile              | Should commit? |
|-----------------|-----------------------|:--------------:|
| npm             | `package-lock.json`   | Yes            |
| yarn v1         | `yarn.lock`           | Yes            |
| yarn v2+        | `yarn.lock`           | Yes            |
| pnpm            | `pnpm-lock.yaml`      | Yes            |
| bun             | `bun.lockb`           | Yes            |

---

## Version Range Syntax (shared across all)

```
1.2.3         exact version
^1.2.3        compatible (>=1.2.3 <2.0.0) — default
~1.2.3        patch only  (>=1.2.3 <1.3.0)
1.2.x         any patch   (>=1.2.0 <1.3.0)
*             any version
>=1.2.3       at least this version
1.2.3 - 2.0.0 version range
latest        the latest tag
```

---

## Speed Comparison (approximate, cold cache)

```
Benchmark: installing a typical React project (node_modules ~300 packages)

bun install          ~0.5s   ████░░░░░░░░░░░░░░░░  Fastest
pnpm install         ~3s     ████████░░░░░░░░░░░░  Fast (hard links)
yarn install (v1)    ~8s     ████████████████░░░░  Medium
npm install          ~10s    ████████████████████  Baseline

Note: pnpm uses a global content-addressable store with hard links,
saving significant disk space across projects.
```

---

## Common Workspace / Monorepo Configs

### npm workspaces (package.json)
```json
{
  "name": "my-monorepo",
  "workspaces": ["packages/*", "apps/*"]
}
```
```bash
npm install                             # Install all workspaces
npm run build --workspace=packages/ui   # Run in specific workspace
npm run build --workspaces              # Run in all workspaces
```

### yarn workspaces (package.json)
```json
{
  "private": true,
  "workspaces": ["packages/*"]
}
```

### pnpm workspaces (pnpm-workspace.yaml)
```yaml
packages:
  - 'packages/*'
  - 'apps/*'
  - '!**/test/**'
```

### bun workspaces (package.json)
```json
{
  "name": "my-monorepo",
  "workspaces": ["packages/*", "apps/*"]
}
```

---

## Quick Command Cheat Sheet

| Action                  | npm                      | yarn                   | pnpm                   | bun                  |
|-------------------------|--------------------------|------------------------|------------------------|----------------------|
| Install all             | `npm install`            | `yarn`                 | `pnpm install`         | `bun install`        |
| Add package             | `npm install <pkg>`      | `yarn add <pkg>`       | `pnpm add <pkg>`       | `bun add <pkg>`      |
| Add dev dep             | `npm install -D <pkg>`   | `yarn add -D <pkg>`    | `pnpm add -D <pkg>`    | `bun add -d <pkg>`   |
| Add global              | `npm install -g <pkg>`   | `yarn global add <pkg>`| `pnpm add -g <pkg>`    | `bun add -g <pkg>`   |
| Remove package          | `npm uninstall <pkg>`    | `yarn remove <pkg>`    | `pnpm remove <pkg>`    | `bun remove <pkg>`   |
| Update all              | `npm update`             | `yarn upgrade`         | `pnpm update`          | `bun update`         |
| Run script              | `npm run <script>`       | `yarn <script>`        | `pnpm <script>`        | `bun run <script>`   |
| Run without install     | `npx <pkg>`              | `yarn dlx <pkg>`       | `pnpm dlx <pkg>`       | `bunx <pkg>`         |
| List packages           | `npm list`               | `yarn list`            | `pnpm list`            | `bun pm ls`          |
| Audit                   | `npm audit`              | `yarn audit`           | `pnpm audit`           | `bun audit`          |
| Clean install (CI)      | `npm ci`                 | `yarn --frozen-lockfile`| `pnpm install --frozen-lockfile` | `bun install --frozen-lockfile` |
| Publish                 | `npm publish`            | `yarn publish`         | `pnpm publish`         | `bun publish`        |
