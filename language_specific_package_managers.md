# Language-Specific Package Managers — Deep Reference

Comprehensive command reference for package managers across every major programming language.
Covers install, remove, update, publish, workspaces, virtual environments, and more.

---

## Table of Contents

- [Python](#python)
  - [pip / pip3](#pip--pip3)
  - [pipenv](#pipenv)
  - [poetry](#poetry)
  - [conda / mamba](#conda--mamba)
  - [uv](#uv)
  - [venv / virtualenv](#venv--virtualenv)
  - [pyenv](#pyenv)
- [Rust — cargo](#rust--cargo)
- [Go — go modules](#go--go-modules)
- [Ruby](#ruby)
  - [gem](#gem)
  - [bundler](#bundler)
  - [rbenv](#rbenv)
  - [rvm](#rvm)
- [PHP — composer](#php--composer)
- [Java / JVM](#java--jvm)
  - [Maven (mvn)](#maven-mvn)
  - [Gradle](#gradle)
- [.NET / C# — dotnet CLI & NuGet](#net--c--dotnet-cli--nuget)
- [Swift — Swift Package Manager](#swift--swift-package-manager)
- [Dart / Flutter](#dart--flutter)
- [Haskell](#haskell)
  - [cabal](#cabal)
  - [stack](#stack)
- [Elixir — mix & hex](#elixir--mix--hex)
- [Julia — Pkg](#julia--pkg)
- [R](#r)
- [Lua — LuaRocks](#lua--luarocks)
- [C / C++](#c--c)
  - [Conan](#conan)
  - [vcpkg](#vcpkg)
- [Perl — cpan & cpanm](#perl--cpan--cpanm)
- [Erlang — rebar3](#erlang--rebar3)
- [Nim — nimble](#nim--nimble)
- [Zig — zig build](#zig--zig-build)
- [Cross-Language Quick Reference Table](#cross-language-quick-reference-table)

---

## Python

### pip / pip3
The standard Python package installer. `pip3` is the same tool for Python 3.

```bash
# --- Version & Help ---
pip --version                           # Show pip version
pip3 --version
pip help                                # Show all commands
pip help install                        # Help for a subcommand

# --- Installing ---
pip install <package>                   # Install latest version
pip install <package>==1.2.3            # Exact version
pip install "<package>>=1.2,<2.0"       # Version range
pip install <package> --pre             # Include pre-releases
pip install <package> --upgrade         # Upgrade existing package
pip install -U <package>                # Short form of --upgrade
pip install <package> --user            # Install for current user only (no sudo)
pip install <package> --target ./vendor # Install into a custom directory
pip install <package> --no-deps         # Skip dependency resolution
pip install <package> --quiet           # Suppress output
pip install --index-url <url> <pkg>     # Use a custom index
pip install --extra-index-url <url> <pkg>
pip install <local-dir>                 # Install from local directory
pip install <tarball.tar.gz>            # Install from tarball
pip install git+https://github.com/user/repo.git  # Install from Git
pip install git+https://github.com/user/repo.git@main  # Specific branch/tag

# --- Requirements Files ---
pip install -r requirements.txt         # Install from requirements file
pip install -r requirements.txt --no-cache-dir
pip install -c constraints.txt <pkg>    # Install with version constraints
pip freeze > requirements.txt           # Export installed packages
pip freeze --local > requirements.txt   # Only local (not global) packages

# --- Removing ---
pip uninstall <package>                 # Remove a package (prompts)
pip uninstall <package> -y             # Remove without prompt
pip uninstall -r requirements.txt -y   # Remove all listed packages

# --- Listing & Info ---
pip list                                # List installed packages
pip list --outdated                     # List outdated packages
pip list --uptodate                     # List up-to-date packages
pip list --format=json                  # JSON output
pip list --format=freeze                # requirements.txt format
pip show <package>                      # Show package metadata
pip show -f <package>                   # Include installed files
pip check                               # Verify all dependencies are satisfied

# --- Searching ---
pip search <query>                      # Search PyPI (deprecated in newer pip)
# Use https://pypi.org or: pip index versions <package>
pip index versions <package>            # List all available versions

# --- Cache ---
pip cache list                          # List cached packages
pip cache info                          # Show cache info
pip cache purge                         # Clear the cache
pip cache remove <package>             # Remove specific package from cache

# --- Config ---
pip config list                         # Show all config values
pip config get global.index-url         # Get a config value
pip config set global.index-url <url>   # Set PyPI mirror
pip config unset global.index-url       # Remove a config value
pip config edit                         # Open config file in editor

# --- Download without Installing ---
pip download <package> -d ./packages    # Download wheel/sdist to a directory
pip download -r requirements.txt -d ./packages

# --- Wheels & Building ---
pip wheel <package>                     # Build a wheel
pip wheel -r requirements.txt -w ./wheels
pip install --no-index --find-links ./wheels <pkg>  # Install from local wheels

# --- Hash Checking (security) ---
pip hash <file>.whl                     # Get hash of a downloaded file
pip install --require-hashes -r requirements.txt  # Enforce hash checking
```

---

### pipenv
Combines virtualenv + pip into one workflow. Creates a `Pipfile` and `Pipfile.lock`.

```bash
# --- Install & Version ---
pip install pipenv
pipenv --version

# --- Project Setup ---
pipenv install                          # Create venv and install from Pipfile
pipenv install --python 3.11            # Specify Python version
pipenv install --dev                    # Install dev dependencies too
pipenv --where                          # Show project home
pipenv --venv                           # Show virtualenv path
pipenv --py                             # Show Python interpreter path

# --- Adding Packages ---
pipenv install <package>                # Add to [packages]
pipenv install <package>==1.2.3         # Specific version
pipenv install "<package>>=1.0"         # Version range
pipenv install <package> --dev          # Add to [dev-packages]
pipenv install -r requirements.txt      # Import from requirements.txt

# --- Removing Packages ---
pipenv uninstall <package>              # Remove from Pipfile
pipenv uninstall --all                  # Remove all packages
pipenv uninstall --all-dev              # Remove all dev packages

# --- Updating ---
pipenv update                           # Update all packages
pipenv update <package>                 # Update a specific package
pipenv upgrade <package>                # Upgrade + update lock
pipenv outdated                         # List outdated packages

# --- Lock File ---
pipenv lock                             # Generate Pipfile.lock
pipenv lock -r                          # Print requirements.txt format
pipenv lock -r --dev                    # Include dev deps
pipenv sync                             # Install from Pipfile.lock (no updates)

# --- Running & Shell ---
pipenv run python script.py             # Run script in venv
pipenv run pytest                       # Run any command in venv
pipenv shell                            # Activate venv shell
exit                                    # Deactivate (inside pipenv shell)

# --- Checking & Graphs ---
pipenv check                            # Check for security vulnerabilities
pipenv graph                            # Show dependency graph
pipenv graph --reverse                  # Show reverse dependency graph

# --- Environment ---
pipenv --rm                             # Remove the virtualenv
PIPENV_VENV_IN_PROJECT=1 pipenv install # Store .venv in project dir
```

---

### poetry
Modern dependency management and packaging. Uses `pyproject.toml`.

```bash
# --- Install ---
curl -sSL https://install.python-poetry.org | python3 -
poetry --version
poetry self update                      # Update poetry itself
poetry self update --preview            # Update to preview version

# --- New Project ---
poetry new <project-name>               # Scaffold a new project
poetry new --src <project>              # Use src/ layout
poetry init                             # Interactively create pyproject.toml

# --- Installing Dependencies ---
poetry install                          # Install all deps from lock file
poetry install --no-dev                 # Skip dev deps (prod deploy)
poetry install --only main              # Install only main group (poetry 1.2+)
poetry install --only dev               # Install only dev group
poetry install --sync                   # Remove unlisted packages too
poetry install --no-root                # Don't install the package itself
poetry install -E <extra>               # Install with an extra

# --- Adding Packages ---
poetry add <package>                    # Add to [tool.poetry.dependencies]
poetry add <package>@^1.2.3             # With version constraint
poetry add <package>@latest             # Latest version
poetry add <package> --group dev        # Add to dev dependency group
poetry add -D <package>                 # Short form: add to dev group
poetry add <package> --optional         # Mark as optional
poetry add <package> --python ">=3.10"  # Python version constraint
poetry add git+https://github.com/u/r  # From Git
poetry add ./path/to/local-pkg         # From local path
poetry add <package> --extras "crypto" # Include extras

# --- Removing Packages ---
poetry remove <package>                 # Remove from dependencies
poetry remove <package> --group dev     # Remove from dev group
poetry remove -D <package>              # Short form

# --- Updating ---
poetry update                           # Update all packages + lock file
poetry update <package>                 # Update specific package
poetry show --outdated                  # List packages with newer versions
poetry show --latest                    # Show latest available versions

# --- Lock File ---
poetry lock                             # Regenerate lock file without installing
poetry lock --no-update                 # Refresh lock without upgrading
poetry check                            # Validate pyproject.toml and lock

# --- Running ---
poetry run python script.py             # Run in venv
poetry run pytest                       # Run command in venv
poetry shell                            # Activate venv shell
exit                                    # Deactivate

# --- Virtual Environment ---
poetry env info                         # Show venv info
poetry env list                         # List all envs for this project
poetry env use python3.11               # Switch Python version
poetry env use /path/to/python          # Use specific interpreter
poetry env remove <env-name>            # Delete an env
poetry config virtualenvs.in-project true  # Store .venv inside project

# --- Listing & Info ---
poetry show                             # List installed packages
poetry show <package>                   # Show package details
poetry show --tree                      # Dependency tree
poetry show --no-dev                    # Exclude dev deps

# --- Publishing ---
poetry config pypi-token.pypi <token>   # Set PyPI API token
poetry build                            # Build sdist and wheel
poetry publish                          # Upload to PyPI
poetry publish --build                  # Build then publish
poetry publish -r testpypi              # Publish to TestPyPI
poetry publish --dry-run                # Simulate publish

# --- Version Bumping ---
poetry version patch                    # Bump patch (1.0.0 → 1.0.1)
poetry version minor                    # Bump minor (1.0.0 → 1.1.0)
poetry version major                    # Bump major (1.0.0 → 2.0.0)
poetry version prerelease               # Bump to next prerelease
poetry version 2.1.0                    # Set exact version

# --- Dependency Groups (poetry 1.2+) ---
# pyproject.toml: [tool.poetry.group.test.dependencies]
poetry install --with test,lint         # Install named groups
poetry install --without docs           # Exclude a group

# --- Config ---
poetry config --list                    # Show all config
poetry config virtualenvs.create false  # Disable auto venv creation
poetry config cache-dir                 # Show cache location
```

---

### conda / mamba
Environment and package manager for data science. Handles non-Python packages too.

```bash
# --- Install ---
# Download Miniconda: https://docs.conda.io/en/latest/miniconda.html
# or Miniforge (recommended): https://github.com/conda-forge/miniforge
conda --version
conda update conda                      # Update conda itself
mamba --version                         # mamba = drop-in faster conda

# --- Environment Management ---
conda create -n myenv python=3.11       # Create a new environment
conda create -n myenv python=3.11 numpy pandas  # With packages
conda create -p ./venv python=3.11      # Create in local path
conda activate myenv                    # Activate environment
conda deactivate                        # Deactivate current environment
conda env list                          # List all environments
conda env remove -n myenv               # Delete an environment
conda env remove -p ./venv

# --- Cloning Environments ---
conda create -n myenv_copy --clone myenv       # Clone an environment
conda env export > environment.yml             # Export environment
conda env export --no-builds > env.yml         # Without build strings
conda env export --from-history > env.yml      # Only explicitly installed
conda env create -f environment.yml            # Create from file
conda env update -f environment.yml            # Update from file
conda env update -f environment.yml --prune    # Also remove unlisted packages

# --- Installing Packages ---
conda install <package>                 # Install in active env
conda install <package>=1.2.3          # Specific version
conda install <package> -c conda-forge # From conda-forge channel
conda install -n myenv <package>        # Install in specific env
conda install --file requirements.txt  # Install from file
mamba install <package>                 # Faster with mamba

# --- Removing Packages ---
conda remove <package>                  # Remove from active env
conda remove -n myenv <package>         # Remove from specific env
conda remove --all -n myenv             # Remove entire environment

# --- Updating Packages ---
conda update <package>                  # Update a package
conda update --all                      # Update all packages in env
conda update -n myenv --all             # Update all in specific env

# --- Listing & Searching ---
conda list                              # List installed packages
conda list -n myenv                     # List in specific env
conda list <package>                    # Show if/how package is installed
conda search <package>                  # Search available packages
conda search <package> -c conda-forge   # Search specific channel
conda info                              # Show system and conda info
conda info --envs                       # Same as env list

# --- Channels ---
conda config --show channels            # Show configured channels
conda config --add channels conda-forge # Add a channel (prepend)
conda config --append channels <ch>    # Add channel at end (lower priority)
conda config --remove channels <ch>    # Remove a channel
conda config --set channel_priority strict  # Strict channel priority

# --- Cleaning ---
conda clean --all                       # Remove all cached data
conda clean --packages                  # Remove unused packages
conda clean --index-cache               # Clear index cache
conda clean --tarballs                  # Remove downloaded archives

# --- Running Without Activating ---
conda run -n myenv python script.py     # Run in env without activating

# --- pip inside conda ---
conda activate myenv
pip install <package>                   # Use pip within active conda env
# Always activate first; never use pip with --user in conda envs
```

---

### uv
Extremely fast Python package installer and resolver (written in Rust). Drop-in pip replacement.

```bash
# --- Install ---
curl -LsSf https://astral.sh/uv/install.sh | sh   # macOS/Linux
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"  # Windows
pip install uv                           # Via pip
uv --version
uv self update                          # Update uv itself

# --- Project Management (uv projects, pyproject.toml) ---
uv init <project-name>                  # Create new project
uv init --lib <name>                    # Create library project
uv init --script script.py             # Create standalone script
uv add <package>                        # Add dependency to project
uv add "<package>>=1.0,<2.0"            # With version constraint
uv add <package> --dev                  # Add to dev dependencies
uv add <package> --optional <group>     # Add to optional group
uv remove <package>                     # Remove dependency
uv sync                                 # Sync environment with pyproject.toml
uv sync --frozen                        # Sync without updating lock file
uv sync --no-dev                        # Exclude dev dependencies
uv lock                                 # Update uv.lock without syncing
uv lock --check                         # Verify lock is up-to-date
uv tree                                 # Show dependency tree

# --- pip Interface (drop-in replacement) ---
uv pip install <package>                # Install a package
uv pip install -r requirements.txt     # Install from requirements
uv pip install -e .                     # Install current package editable
uv pip uninstall <package>              # Uninstall
uv pip list                             # List installed packages
uv pip freeze                           # Output requirements.txt format
uv pip show <package>                   # Show package info
uv pip check                            # Verify dependencies
uv pip compile requirements.in          # Compile to requirements.txt
uv pip sync requirements.txt            # Sync env exactly (removes extras)

# --- Virtual Environments ---
uv venv                                 # Create .venv in current directory
uv venv --python 3.11                   # Specify Python version
uv venv ./my-venv                       # Custom path
uv venv --python cpython-3.12           # Specific implementation

# --- Python Version Management ---
uv python install 3.12                  # Install a Python version
uv python install 3.10 3.11 3.12        # Install multiple versions
uv python list                          # List available Python versions
uv python list --only-installed         # List installed versions
uv python find 3.11                     # Find Python 3.11 interpreter path
uv python pin 3.11                      # Pin project Python version (.python-version)
uv python uninstall 3.10                # Remove a Python version

# --- Running Scripts & Tools ---
uv run python script.py                 # Run in project environment
uv run pytest                           # Run tool in project env
uvx ruff check .                        # Run tool without installing (like pipx)
uv tool install ruff                    # Install tool globally
uv tool run ruff                        # Run installed tool
uv tool list                            # List installed tools
uv tool uninstall ruff                  # Uninstall tool
uv tool upgrade --all                   # Upgrade all tools

# --- Caching ---
uv cache dir                            # Show cache directory
uv cache clean                          # Clear entire cache
uv cache prune                          # Remove stale entries
```

---

### venv / virtualenv
Built-in Python virtual environment tools.

```bash
# --- venv (built into Python 3.3+) ---
python3 -m venv .venv                   # Create venv in .venv/
python3 -m venv .venv --python 3.11     # Specific version
python3 -m venv .venv --clear           # Recreate if exists
python3 -m venv .venv --upgrade-deps    # Upgrade pip/setuptools in venv

source .venv/bin/activate               # Activate (macOS/Linux)
.venv\Scripts\activate                  # Activate (Windows cmd)
.venv\Scripts\Activate.ps1             # Activate (PowerShell)
deactivate                              # Deactivate

# --- virtualenv (third-party, more features) ---
pip install virtualenv
virtualenv .venv                        # Create virtualenv
virtualenv .venv --python=python3.11    # Specific Python
virtualenv .venv --system-site-packages # Access system packages
virtualenv .venv --copies               # Copy instead of symlink
virtualenv --version
```

---

### pyenv
Python version manager — install and switch between Python versions.

```bash
# --- Install ---
# macOS:  brew install pyenv
# Linux:  curl https://pyenv.run | bash
# Windows: pyenv-win via scoop/chocolatey

pyenv --version
pyenv update                            # Update pyenv

# --- Installing Python Versions ---
pyenv install --list                    # List all installable versions
pyenv install 3.12.0                    # Install a version
pyenv install 3.11.8 3.10.14           # Install multiple
pyenv uninstall 3.10.14                # Remove a version
pyenv versions                          # List installed versions
pyenv version                           # Show current active version

# --- Setting Versions ---
pyenv global 3.12.0                     # Set system-wide default
pyenv local 3.11.8                      # Set for current dir (.python-version)
pyenv shell 3.10.14                     # Set for current shell session
pyenv which python                      # Show path of active python

# --- Virtualenv Integration ---
# Install pyenv-virtualenv plugin first
pyenv virtualenv 3.12.0 my-project      # Create named venv
pyenv activate my-project               # Activate
pyenv deactivate                        # Deactivate
pyenv virtualenvs                       # List all virtualenvs
pyenv uninstall my-project             # Delete virtualenv
```

---

## Rust — cargo

The official Rust package manager and build tool.

```bash
# --- Install Rust + cargo ---
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo --version
rustup update                           # Update Rust + cargo

# --- New Project ---
cargo new <project-name>                # Binary project (src/main.rs)
cargo new <project-name> --lib          # Library project (src/lib.rs)
cargo new <project-name> --edition 2021 # With specific edition
cargo init                              # Initialize in current directory
cargo init --lib                        # Library in current directory

# --- Building ---
cargo build                             # Debug build → target/debug/
cargo build --release                   # Release build → target/release/
cargo build --target x86_64-unknown-linux-musl  # Cross-compile
cargo check                             # Type-check without building binary
cargo clippy                            # Run linter
cargo clippy -- -D warnings            # Treat warnings as errors
cargo fmt                               # Format code
cargo fmt --check                       # Check formatting without changing

# --- Running ---
cargo run                               # Build and run (debug)
cargo run --release                     # Build and run (release)
cargo run --bin <name>                  # Run specific binary in workspace
cargo run -- arg1 arg2                  # Pass args to the program

# --- Testing ---
cargo test                              # Run all tests
cargo test <name>                       # Run tests matching name
cargo test --lib                        # Only library tests
cargo test --doc                        # Only doc tests
cargo test --release                    # Test in release mode
cargo test -- --nocapture               # Show stdout from tests
cargo test -- --test-threads=1          # Run tests single-threaded
cargo bench                             # Run benchmarks

# --- Adding Dependencies (Cargo.toml) ---
cargo add <package>                     # Add latest version to Cargo.toml
cargo add <package>@1.2.3              # Specific version
cargo add <package> --features "feat1,feat2"  # With features
cargo add <package> --dev               # Add to [dev-dependencies]
cargo add <package> --build             # Add to [build-dependencies]
cargo add <package> --optional          # Mark as optional feature
cargo add <package> --git <url>         # From Git repository
cargo add <package> --git <url> --branch main
cargo add <package> --path ./local-crate # From local path
cargo remove <package>                  # Remove dependency from Cargo.toml

# --- Updating ---
cargo update                            # Update Cargo.lock (minor/patch)
cargo update <package>                  # Update specific package
cargo update <package> --precise 1.2.3 # Pin to exact version

# --- Workspace ---
# Cargo.toml: [workspace] members = ["crate-a", "crate-b"]
cargo build --workspace                 # Build all workspace members
cargo test --workspace                  # Test all members
cargo build -p <crate>                  # Build specific crate
cargo run -p <crate>                    # Run specific crate

# --- Publishing to crates.io ---
cargo login                             # Authenticate with API token
cargo login <token>                     # Provide token directly
cargo search <query>                    # Search crates.io
cargo info <package>                    # Show crate info
cargo publish                           # Publish to crates.io
cargo publish --dry-run                 # Simulate publish
cargo publish --allow-dirty             # Publish with uncommitted changes
cargo yank --vers 1.2.3                 # Yank a version (prevent installs)
cargo yank --vers 1.2.3 --undo          # Un-yank
cargo owner --add <user>               # Add owner to a crate
cargo owner --remove <user>            # Remove owner

# --- Installing Binaries ---
cargo install <package>                 # Install binary from crates.io
cargo install <package> --version 1.2.3
cargo install <package> --features "feat"
cargo install --git <url>               # Install from Git
cargo install --path .                  # Install from local crate
cargo install --list                    # List installed binaries
cargo uninstall <package>               # Remove installed binary

# --- Cache & Cleaning ---
cargo clean                             # Remove target/ directory
cargo clean -p <crate>                  # Clean specific crate
~/.cargo/                               # Global cargo home
cargo cache --autoclean                 # (via cargo-cache plugin)

# --- Docs ---
cargo doc                               # Build documentation
cargo doc --open                        # Build and open in browser
cargo doc --no-deps                     # Only document this crate

# --- Useful cargo subcommands (install via cargo install) ---
cargo expand                            # Expand macros
cargo watch -x run                      # Rerun on file changes
cargo audit                             # Check for security vulnerabilities
cargo outdated                          # Show outdated dependencies
cargo tree                              # Display dependency tree
cargo tree -d                           # Show duplicates only
cargo flamegraph                        # Generate performance flamegraph
cargo tarpaulin                         # Code coverage
```

---

## Go — go modules

Go's built-in dependency management system.

```bash
# --- Install & Version ---
go version
go env GOPATH                           # Show GOPATH
go env GOMODCACHE                       # Show module cache path
go env                                  # Show all Go environment variables

# --- Module Initialization ---
go mod init <module-path>               # Initialize a new module
# e.g.: go mod init github.com/username/myapp

# --- Adding Dependencies ---
go get <package>                        # Add + install latest
go get <package>@v1.2.3                 # Specific version
go get <package>@latest                 # Latest released version
go get <package>@main                   # Latest commit on main branch
go get <package>@<commit-hash>          # Specific commit
go get -u <package>                     # Upgrade to latest minor/patch
go get -u=patch <package>               # Upgrade patch only
go get ./...                            # Update all packages in module

# --- Removing Dependencies ---
# Remove import from code, then:
go mod tidy                             # Remove unused deps, add missing

# --- Building & Running ---
go build .                              # Build current package
go build ./...                          # Build all packages in module
go build -o myapp .                     # Build with output name
go run .                                # Run current package
go run main.go                          # Run specific file
go run ./cmd/server                     # Run specific subdirectory

# --- Testing ---
go test ./...                           # Test all packages
go test ./pkg/...                       # Test specific subtree
go test -v ./...                        # Verbose output
go test -run TestName ./...             # Run tests matching name
go test -bench=. ./...                  # Run benchmarks
go test -bench=. -benchmem ./...        # With memory stats
go test -cover ./...                    # Show coverage
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out        # View coverage in browser
go test -race ./...                     # Detect data races
go test -count=1 ./...                  # Disable test caching

# --- Module Files ---
go mod tidy                             # Sync go.mod and go.sum
go mod tidy -e                          # Continue despite errors
go mod verify                           # Verify module integrity
go mod graph                            # Print module dependency graph
go mod download                         # Download all dependencies
go mod download <module>                # Download specific module
go mod edit -replace old=new            # Replace a module
go mod edit -dropreplace old            # Remove a replace directive
go mod why <package>                    # Explain why package is needed
go mod vendor                           # Copy deps to vendor/
go build -mod=vendor ./...              # Build using vendor/

# --- Listing ---
go list -m all                          # List all modules (deps)
go list -m -u all                       # With available updates
go list -m -json all                    # JSON output
go list ./...                           # List all packages in module

# --- Installing Tools ---
go install <package>@latest             # Install binary tool
go install <package>@v1.2.3            # Specific version
# Binaries go to $GOPATH/bin (usually ~/go/bin)

# --- Workspaces (go 1.18+) ---
go work init ./module-a ./module-b      # Create go.work
go work use ./module-c                  # Add module to workspace
go work sync                            # Sync workspace
go work edit -replace old=new           # Add replace directive

# --- Formatting & Linting ---
go fmt ./...                            # Format all Go files
gofmt -w .                              # Format in-place
go vet ./...                            # Report likely errors
golangci-lint run                       # Comprehensive linter (install separately)

# --- Documentation ---
go doc <package>                        # Show package docs
go doc <package>.<Symbol>               # Show specific symbol docs
godoc -http=:6060                       # Start local doc server

# --- Cross-Compilation ---
GOOS=linux GOARCH=amd64 go build -o myapp-linux .
GOOS=windows GOARCH=amd64 go build -o myapp.exe .
GOOS=darwin GOARCH=arm64 go build -o myapp-mac .
go tool dist list                       # List all GOOS/GOARCH combos

# --- Cache ---
go clean -cache                         # Clear build cache
go clean -modcache                      # Clear module cache
go clean -testcache                     # Clear test cache
go clean -fuzzcache                     # Clear fuzz cache
```

---

## Ruby

### gem
RubyGems — the standard Ruby package manager.

```bash
# --- Version & Update ---
gem --version
gem update --system                     # Update RubyGems itself

# --- Installing Gems ---
gem install <gem>                       # Install latest version
gem install <gem> -v 1.2.3             # Specific version
gem install <gem> --pre                 # Include pre-release versions
gem install <gem> --no-document        # Skip docs (faster)
gem install <gem> --user-install        # Install in user's home (~/.gem)
gem install <gem> --install-dir ./gems  # Custom directory
gem install --local <gem>.gem           # Install from local file
gem install --source <url> <gem>        # Use custom gem server

# --- Removing Gems ---
gem uninstall <gem>                     # Remove latest version
gem uninstall <gem> -v 1.2.3           # Specific version
gem uninstall <gem> --all               # All versions
gem uninstall <gem> -ax                 # All versions + executables

# --- Updating Gems ---
gem update                              # Update all gems
gem update <gem>                        # Update specific gem
gem outdated                            # List outdated gems
gem update --system                     # Update RubyGems itself

# --- Listing & Info ---
gem list                                # List installed gems
gem list <gem>                          # Show versions of specific gem
gem contents <gem>                      # List files in gem
gem info <gem>                          # Show gem info
gem search <query>                      # Search rubygems.org
gem search <query> --remote             # Explicit remote search
gem dependency <gem>                    # Show gem's dependencies
gem environment                         # Show RubyGems environment

# --- Cleanup ---
gem cleanup                             # Remove old versions of all gems
gem cleanup <gem>                       # Remove old versions of specific gem

# --- Sources ---
gem sources --list                      # List gem sources
gem sources --add <url>                 # Add source
gem sources --remove <url>              # Remove source
gem sources --clear-all                 # Remove all sources

# --- Creating & Publishing Gems ---
bundle gem <gem-name>                   # Scaffold new gem (uses bundler)
gem build <name>.gemspec               # Build .gem file
gem push <name>-1.0.0.gem              # Publish to rubygems.org
gem owner --add <email> <gem>          # Add owner
gem yank <gem> -v 1.0.0                # Yank a version
gem signin                              # Log in to rubygems.org
```

---

### bundler
Manages gem dependencies for a project. Uses `Gemfile` and `Gemfile.lock`.

```bash
# --- Install & Version ---
gem install bundler
bundle version
bundle help

# --- Setup ---
bundle init                             # Create a Gemfile
bundle install                          # Install all Gemfile dependencies
bundle install --without development test  # Skip groups
bundle install --deployment             # Frozen install for production
bundle install --path vendor/bundle     # Install into project-local dir
bundle install --jobs 4                 # Parallel install

# --- Adding Packages ---
bundle add <gem>                        # Add to Gemfile + install
bundle add <gem> --version "~> 1.2"    # With version constraint
bundle add <gem> --group development    # In specific group
bundle add <gem> --require false        # Don't auto-require

# --- Removing Packages ---
bundle remove <gem>                     # Remove from Gemfile

# --- Updating ---
bundle update                           # Update all gems (update lock file)
bundle update <gem>                     # Update specific gem
bundle update --conservative            # Only patch/minor updates
bundle outdated                         # Show outdated gems

# --- Running in Context ---
bundle exec <command>                   # Run command using Gemfile gems
bundle exec rspec                       # Run rspec with bundled gems
bundle exec ruby script.rb

# --- Lock File ---
bundle lock                             # Generate Gemfile.lock without installing
bundle lock --update                    # Update lock file
bundle lock --add-platform x86_64-linux # Add a platform to lock file

# --- Checking & Cleaning ---
bundle check                            # Check if all gems are installed
bundle list                             # List gems in bundle
bundle show <gem>                       # Show path to gem
bundle info <gem>                       # Show gem info
bundle viz                              # Generate dependency graph (graphviz)
bundle clean                            # Remove gems not in Gemfile.lock
bundle clean --force                    # Force remove all other gems

# --- Configuration ---
bundle config list                      # Show all config
bundle config set --local path vendor/bundle
bundle config set --global without development
bundle config unset <key>
```

---

### rbenv
Ruby version manager (lightweight, shell-based).

```bash
# --- Install ---
# macOS:  brew install rbenv
# Linux:  git clone https://github.com/rbenv/rbenv.git ~/.rbenv

rbenv --version
rbenv init                              # Setup shell integration
rbenv doctor                            # Check installation

# --- Installing Ruby Versions ---
rbenv install --list                    # List stable versions
rbenv install --list-all                # All available versions
rbenv install 3.3.0                     # Install a version
rbenv install 3.2.2 3.1.4              # Multiple versions
rbenv uninstall 3.1.4                   # Remove a version
rbenv versions                          # List installed versions
rbenv version                           # Show current version

# --- Setting Versions ---
rbenv global 3.3.0                      # Set system default
rbenv local 3.2.2                       # Set for current dir (.ruby-version)
rbenv shell 3.1.4                       # Set for current shell
rbenv which ruby                        # Show path to ruby
rbenv whence bundle                     # Show versions with this command

# --- Rehashing (after installing gems with executables) ---
rbenv rehash                            # Rebuild shim executables
# (runs automatically with rbenv-gem-rehash plugin)
```

---

### rvm
Ruby Version Manager (full-featured, manages gemsets too).

```bash
# --- Install ---
\curl -sSL https://get.rvm.io | bash -s stable
rvm --version

# --- Installing Ruby ---
rvm list known                          # List available versions
rvm install 3.3.0                       # Install a version
rvm install ruby-head                   # Install latest dev build
rvm uninstall 3.1.0                     # Remove a version
rvm list                                # List installed versions
rvm current                             # Show current version

# --- Switching Versions ---
rvm use 3.3.0                           # Use a version
rvm use 3.3.0 --default                 # Set as default
rvm use system                          # Use system Ruby
rvm use ruby-3.3.0@myapp                # Use version + gemset

# --- Gemsets (isolated gem environments) ---
rvm gemset create myapp                 # Create a gemset
rvm gemset use myapp                    # Switch to gemset
rvm gemset list                         # List gemsets for current Ruby
rvm gemset list_all                     # List all gemsets
rvm gemset delete myapp                 # Delete a gemset
rvm gemset empty myapp                  # Remove gems from gemset
rvm gemset export gemlist.txt           # Export gemset contents
rvm gemset import gemlist.txt           # Import gems from file
rvm use 3.3.0@myapp --create            # Create and use gemset

# --- .rvmrc / .ruby-version + .ruby-gemset ---
echo "ruby-3.3.0" > .ruby-version
echo "myapp" > .ruby-gemset
# rvm auto-switches when you cd into the directory
```

---

## PHP — composer

Dependency manager for PHP. Uses `composer.json` and `composer.lock`.

```bash
# --- Install ---
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
sudo mv composer.phar /usr/local/bin/composer
composer --version
composer self-update                    # Update composer itself
composer self-update --rollback         # Rollback to previous version

# --- Project Initialization ---
composer init                           # Interactive setup
composer create-project <vendor>/<pkg> <dir>  # Scaffold from package
composer create-project laravel/laravel myapp  # Laravel example

# --- Installing Dependencies ---
composer install                        # Install from composer.lock
composer install --no-dev               # Skip dev dependencies
composer install --optimize-autoloader # Optimize for production
composer install --no-scripts           # Skip scripts
composer install --ignore-platform-reqs # Ignore PHP version constraints

# --- Adding Packages ---
composer require <vendor>/<package>     # Add + install
composer require <vendor>/<package>:^1.2.3   # With version constraint
composer require <vendor>/<package>:dev-main  # From git main branch
composer require <vendor>/<package> --dev     # Add to require-dev
composer require <vendor>/<package> --no-update  # Add to composer.json only
composer require <vendor>/<package> --with-all-dependencies

# --- Removing Packages ---
composer remove <vendor>/<package>      # Remove from project
composer remove <vendor>/<package> --dev

# --- Updating ---
composer update                         # Update all packages + lock file
composer update <vendor>/<package>      # Update specific package
composer update --with-all-dependencies # Update + all transitive deps
composer update --lock                  # Only update lock file hash
composer outdated                       # List outdated packages
composer outdated --direct              # Only direct deps
composer outdated --minor-only          # Only minor version bumps

# --- Listing & Info ---
composer show                           # List installed packages
composer show <vendor>/<package>        # Show package details
composer show --tree                    # Dependency tree
composer show --latest                  # Show latest available versions
composer info <vendor>/<package>        # Show package info

# --- Autoloading ---
composer dump-autoload                  # Regenerate autoloader
composer dump-autoload --optimize       # Optimize class map
composer dump-autoload --classmap-authoritative  # Only class map (fastest)
composer dump-autoload --no-dev         # Exclude dev

# --- Scripts ---
composer run-script <script>            # Run a composer script
composer run <script>                   # Short alias
composer run test                       # Example
# Scripts are defined in composer.json "scripts" section

# --- Checking & Validation ---
composer validate                       # Validate composer.json
composer check-platform-reqs            # Check PHP + extension requirements
composer audit                          # Check for security vulnerabilities

# --- Search ---
composer search <query>                 # Search Packagist
composer search <query> --only-name     # Search by package name only

# --- Configuration ---
composer config --list                  # Show all config
composer config --global home           # Show config home
composer config repositories.local vcs ./local-pkg  # Add VCS repo
composer config repositories.packagist composer https://packagist.org
composer config --global process-timeout 600
composer global require <package>       # Install global tool
composer global update                  # Update global packages
composer global show                    # List global packages

# --- Lock File ---
composer lock --no-update               # Update lock file hash only
composer update nothing                 # Same as above

# --- Cache ---
composer clear-cache                    # Clear composer cache
composer cache-clear                    # Same
```

---

## Java / JVM

### Maven (mvn)

Build automation and dependency management for Java projects.

```bash
# --- Install ---
# macOS:  brew install maven
# Linux:  sudo apt install maven  OR  sudo dnf install maven
# Windows: scoop install maven  OR  choco install maven
mvn --version

# --- Project Setup ---
mvn archetype:generate \
  -DgroupId=com.example \
  -DartifactId=my-app \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DarchetypeVersion=1.4 \
  -DinteractiveMode=false
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-webapp  # Web app

# --- Lifecycle Phases (run in order) ---
mvn validate                            # Validate project structure
mvn compile                             # Compile source code
mvn test                                # Run unit tests
mvn package                             # Build JAR/WAR
mvn verify                              # Run integration tests
mvn install                             # Install to local ~/.m2 repo
mvn deploy                              # Upload to remote repository
mvn clean                               # Delete target/ directory
mvn clean install                       # Clean build + install
mvn clean package -DskipTests           # Build without running tests

# --- Running ---
mvn exec:java -Dexec.mainClass="com.example.App"
mvn spring-boot:run                     # Run Spring Boot app

# --- Dependencies ---
mvn dependency:resolve                  # Resolve all dependencies
mvn dependency:tree                     # Print dependency tree
mvn dependency:tree -Dincludes=<group>  # Filter dependency tree
mvn dependency:list                     # List dependencies
mvn dependency:analyze                  # Analyze unused/undeclared deps
mvn dependency:purge-local-repository   # Delete cached deps, re-download
mvn versions:display-dependency-updates # Show available updates
mvn versions:use-latest-releases        # Update to latest releases
mvn versions:use-latest-versions        # Update including snapshots

# --- Plugins ---
mvn help:describe -Dplugin=compiler     # Describe a plugin
mvn help:effective-pom                  # Show effective (merged) POM
mvn help:active-profiles                # Show active profiles
mvn site                                # Generate project site/docs
mvn javadoc:javadoc                     # Generate Javadoc

# --- Profiles ---
mvn package -Pproduction                # Activate profile
mvn package -Pdevelopment,testing       # Multiple profiles

# --- Skipping ---
mvn install -DskipTests                 # Skip test execution
mvn install -Dmaven.test.skip=true      # Skip test compilation + execution
mvn package -q                          # Quiet output

# --- Wrapper ---
./mvnw clean install                    # Use project's Maven wrapper (Linux/Mac)
.\mvnw.cmd clean install                # Windows
```

---

### Gradle

Flexible build tool for Java, Kotlin, Groovy, Android, and more.

```bash
# --- Install ---
# macOS:  brew install gradle
# Linux:  sdk install gradle  (via SDKMAN)
# Windows: scoop install gradle  OR  choco install gradle
gradle --version

# --- Project Setup ---
gradle init                             # Interactive project scaffold
gradle init --type java-application     # Java app
gradle init --type java-library         # Java library
gradle init --type kotlin-application   # Kotlin app
gradle init --dsl kotlin                # Use Kotlin DSL (build.gradle.kts)

# --- Building ---
gradle build                            # Compile + test + jar
gradle assemble                         # Build without tests
gradle compileJava                      # Compile only
gradle classes                          # Compile + process resources
gradle jar                              # Create JAR
gradle war                              # Create WAR
gradle clean                            # Delete build/ directory
gradle clean build                      # Clean then build
gradle build -x test                    # Build, skip tests

# --- Testing ---
gradle test                             # Run all tests
gradle test --tests "*.MyTest"          # Run matching tests
gradle test --tests "com.example.MyTest.myMethod"
gradle test --info                      # Verbose test output

# --- Running ---
gradle run                              # Run main application (application plugin)
gradle bootRun                          # Run Spring Boot app

# --- Tasks ---
gradle tasks                            # List all tasks
gradle tasks --all                      # List all tasks with descriptions
gradle help --task <taskName>           # Describe a task
gradle <taskName>                       # Run any task
gradle <task1> <task2>                  # Run multiple tasks

# --- Dependencies ---
gradle dependencies                     # Print dependency tree (all configs)
gradle dependencies --configuration runtimeClasspath
gradle dependencyInsight --dependency <pkg>  # Explain why dep is included
gradle dependencyUpdates               # Check for updates (requires plugin)

# --- Daemon ---
gradle --daemon                         # Use (start if needed) Gradle daemon
gradle --no-daemon                      # Don't use daemon
gradle --stop                           # Stop all daemons
gradle status                           # Show daemon status

# --- Performance ---
gradle build --parallel                 # Build subprojects in parallel
gradle build --build-cache              # Use build cache
gradle build --configuration-cache      # Use configuration cache
gradle build --scan                     # Upload build scan to Gradle Enterprise
gradle build -p <project> --no-daemon

# --- Wrapper ---
gradle wrapper                          # Generate Gradle wrapper files
gradle wrapper --gradle-version 8.6     # Specific version
./gradlew build                         # Use wrapper (Linux/macOS)
.\gradlew.bat build                     # Use wrapper (Windows)
./gradlew --refresh-dependencies build  # Force re-download deps

# --- Kotlin DSL (build.gradle.kts) examples ---
# dependencies { implementation("com.google.guava:guava:32.1.3-jre") }
# repositories { mavenCentral() }

# --- Multi-Project Build ---
gradle :subproject:build                # Build specific subproject
gradle -p subproject build              # Same
gradle build --project-dir subproject   # Another form
```

---

## .NET / C# — dotnet CLI & NuGet

```bash
# --- Install ---
# Download from https://dot.net
dotnet --version
dotnet --list-sdks                      # List installed SDKs
dotnet --list-runtimes                  # List installed runtimes
dotnet tool update --global dotnet-outdated  # Update global tool

# --- New Project ---
dotnet new list                         # List all templates
dotnet new console -n MyApp             # Console application
dotnet new webapi -n MyApi              # ASP.NET Web API
dotnet new blazorwasm -n MyBlazor       # Blazor WebAssembly
dotnet new classlib -n MyLib            # Class library
dotnet new sln -n MySolution            # Solution file
dotnet new gitignore                    # .gitignore for .NET
dotnet new --install <template>         # Install template package

# --- Solution & Project Management ---
dotnet sln add MyProject/MyProject.csproj    # Add project to solution
dotnet sln remove MyProject/MyProject.csproj
dotnet sln list                              # List projects in solution
dotnet add reference ../MyLib/MyLib.csproj   # Add project reference

# --- NuGet Package Management ---
dotnet add package <PackageName>             # Add NuGet package
dotnet add package <PackageName> --version 1.2.3
dotnet add package <PackageName> --prerelease
dotnet add package <PackageName> --source <url>  # Custom feed
dotnet remove package <PackageName>          # Remove package
dotnet list package                          # List packages in project
dotnet list package --outdated               # Show outdated packages
dotnet list package --vulnerable             # Show vulnerable packages
dotnet list package --include-transitive     # Include indirect deps
dotnet restore                               # Restore all packages
dotnet restore --no-cache                    # Skip cache
dotnet restore --locked-mode                # Fail if packages.lock.json would change

# --- Building ---
dotnet build                                 # Build project
dotnet build -c Release                      # Release build
dotnet build --no-restore                    # Skip restore
dotnet build -p:Version=1.2.3               # Set version property
dotnet build /warnaserror                    # Treat warnings as errors
dotnet msbuild                               # Direct MSBuild access

# --- Running ---
dotnet run                                   # Run project
dotnet run --project ./src/MyApp             # Specify project
dotnet run -c Release                        # Release mode
dotnet run -- --port 5000                    # Pass args to app
dotnet watch run                             # Run with hot reload

# --- Testing ---
dotnet test                                  # Run all tests
dotnet test ./tests/MyTests.csproj           # Specific test project
dotnet test --filter "TestCategory=Unit"     # Filter tests
dotnet test --filter "FullyQualifiedName~MyTest"
dotnet test -v detailed                      # Verbose output
dotnet test --collect:"XPlat Code Coverage"  # Code coverage
dotnet test --logger "trx;LogFileName=results.trx"

# --- Publishing ---
dotnet publish                               # Publish app
dotnet publish -c Release -o ./publish       # Release to dir
dotnet publish -c Release -r linux-x64       # Linux self-contained
dotnet publish -c Release -r win-x64 --self-contained
dotnet publish -c Release -p:PublishSingleFile=true  # Single exe
dotnet publish -c Release -p:PublishTrimmed=true     # Trim unused code

# --- Global Tools ---
dotnet tool install -g <tool>               # Install global tool
dotnet tool install --local <tool>          # Install local tool
dotnet tool update -g <tool>                # Update global tool
dotnet tool uninstall -g <tool>             # Remove global tool
dotnet tool list -g                         # List global tools
dotnet tool list                            # List local tools
dotnet tool restore                         # Restore local tools from manifest
dotnet new tool-manifest                    # Create tools manifest file

# --- NuGet CLI (nuget.exe / dotnet nuget) ---
dotnet nuget list source                    # List NuGet sources
dotnet nuget add source <url> -n <name>     # Add source
dotnet nuget remove source <name>           # Remove source
dotnet nuget push <package>.nupkg -k <key> -s https://api.nuget.org/v3/index.json
dotnet nuget delete <pkg> <ver> -k <key> -s <source>  # Remove from feed
dotnet pack                                 # Create NuGet package (.nupkg)
dotnet pack -c Release -o ./nupkgs          # Release package to dir
dotnet pack -p:PackageVersion=1.2.3

# --- Format & Analyze ---
dotnet format                               # Format code
dotnet format --verify-no-changes           # CI check
dotnet format style                         # Style fixes only
dotnet format analyzers                     # Analyzer fixes only
```

---

## Swift — Swift Package Manager

```bash
# --- Comes with Xcode / Swift toolchain ---
swift package --version
swift --version

# --- Creating a Package ---
mkdir MyPackage && cd MyPackage
swift package init                          # Library package
swift package init --type executable        # Executable
swift package init --type library           # Explicit library
swift package init --name MyTool            # With name

# --- Building ---
swift build                                 # Debug build
swift build -c release                      # Release build
swift build --target <Target>               # Specific target
swift build --show-bin-path                 # Show output directory

# --- Running ---
swift run                                   # Build + run executable
swift run <Target>                          # Run specific target
swift run -c release                        # Release mode
swift run -- arg1 arg2                      # Pass arguments

# --- Testing ---
swift test                                  # Run all tests
swift test --filter <TestCase>              # Run matching tests
swift test --filter <TestCase>/<testMethod>
swift test -c release                       # Release mode
swift test --parallel                       # Parallel testing
swift test --enable-code-coverage           # Generate coverage data
swift test --show-bin-path                  # Show build output path

# --- Package Resolution ---
swift package resolve                       # Resolve dependencies (update Package.resolved)
swift package update                        # Update all dependencies
swift package update <PackageName>          # Update specific package

# --- Showing Info ---
swift package show-dependencies             # List resolved dependencies
swift package show-dependencies --format json
swift package describe                      # Describe the package
swift package dump-package                  # Print Package.swift as JSON

# --- Xcode Integration ---
swift package generate-xcodeproj            # Generate .xcodeproj (legacy)
# Modern approach: use .swiftpackage directly in Xcode

# --- Reset ---
swift package clean                         # Remove .build/
swift package reset                         # Remove all caches + .build/

# --- Plugin Commands ---
swift package plugin --list                 # List available plugins
swift package <plugin-command>              # Run a plugin

# --- Package.swift structure (for reference) ---
# dependencies: [
#   .package(url: "https://github.com/...", from: "1.0.0"),
#   .package(url: "https://github.com/...", .upToNextMinor(from: "2.1.0")),
#   .package(url: "https://github.com/...", branch: "main"),
#   .package(url: "https://github.com/...", revision: "abc123"),
#   .package(path: "../local-package"),
# ]
```

---

## Dart / Flutter

### dart pub

```bash
# --- Version ---
dart --version
dart pub --version

# --- Project Setup ---
dart create <project>                   # Create new Dart app
dart create -t console <project>        # Console app
dart create -t package <project>        # Dart package
dart create -t server-shelf <project>   # Server app

# --- Installing Dependencies ---
dart pub get                            # Install from pubspec.yaml
dart pub get --offline                  # Install from local cache
dart pub upgrade                        # Upgrade all to latest allowed versions
dart pub upgrade <package>              # Upgrade specific package
dart pub upgrade --major-versions       # Upgrade including major version bumps
dart pub downgrade                      # Downgrade to earliest allowed versions

# --- Adding / Removing ---
dart pub add <package>                  # Add dependency
dart pub add <package>:^1.2.3           # With version constraint
dart pub add dev:<package>              # Add dev dependency
dart pub remove <package>               # Remove dependency

# --- Listing & Info ---
dart pub deps                           # Show dependency tree
dart pub deps --style=compact           # Compact tree
dart pub deps --json                    # JSON output
dart pub outdated                       # Show outdated packages
dart pub outdated --mode=null-safety    # Check null safety status

# --- Publishing ---
dart pub login                          # Authenticate with pub.dev
dart pub publish                        # Publish to pub.dev
dart pub publish --dry-run              # Validate without publishing

# --- Cache ---
dart pub cache list                     # List cached packages
dart pub cache add <package>            # Add package to cache
dart pub cache clean                    # Clear the cache
dart pub cache repair                   # Re-download cached packages

# --- Global Packages (tools) ---
dart pub global activate <package>      # Install globally
dart pub global activate <pkg> --source path ./local
dart pub global deactivate <package>    # Remove global package
dart pub global list                    # List global packages
dart pub global run <package> <command> # Run global package
```

### flutter pub

```bash
# Flutter wraps dart pub — most dart pub commands work with flutter pub
flutter --version
flutter pub get                         # Install dependencies
flutter pub upgrade                     # Upgrade packages
flutter pub upgrade --major-versions    # Include major bumps
flutter pub add <package>               # Add dependency
flutter pub remove <package>            # Remove dependency
flutter pub deps                        # Dependency tree
flutter pub outdated                    # Outdated packages
flutter pub publish                     # Publish Flutter package
flutter pub run <package>:<command>     # Run package executable

# --- Flutter-Specific ---
flutter create <project>                # Create new Flutter app
flutter create --template=plugin <pkg>  # Create Flutter plugin
flutter create --template=package <pkg> # Create Dart-only package
flutter build apk                       # Build Android APK
flutter build ios                       # Build iOS
flutter build web                       # Build web
flutter run                             # Run on connected device
flutter clean                           # Remove build artifacts
flutter doctor                          # Check environment setup
```

---

## Haskell

### cabal
The Haskell package and build tool.

```bash
# --- Install (via GHCup) ---
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh
cabal --version
cabal update                            # Update package list from Hackage

# --- Project Setup ---
cabal init                              # Interactive project setup
cabal init --lib                        # Library
cabal init --exe                        # Executable
cabal init --libandexe                  # Both

# --- Building ---
cabal build                             # Build project
cabal build all                         # Build all components
cabal build <target>                    # Build specific component
cabal clean                             # Remove dist-newstyle/

# --- Running & Testing ---
cabal run                               # Build and run executable
cabal run <exe-name>                    # Run specific executable
cabal run -- arg1 arg2                  # With arguments
cabal test                              # Run tests
cabal test <test-suite>                 # Specific suite
cabal bench                             # Run benchmarks

# --- Dependencies (cabal.project) ---
cabal install <package>                 # Install to global store
cabal install <package> --lib           # Install as library
cabal install <package>-1.2.3          # Specific version
cabal install --package-env .           # Install to project env

# --- Freeze & Solver ---
cabal freeze                            # Write cabal.project.freeze
cabal freeze --dry-run                  # Preview without writing
cabal outdated                          # List outdated deps

# --- REPL ---
cabal repl                              # Open GHCi with project loaded
cabal repl <target>                     # Specific target

# --- Documentation ---
cabal haddock                           # Generate Haddock docs
cabal haddock --open                    # Open in browser

# --- Publish ---
cabal sdist                             # Create source distribution
cabal upload dist-newstyle/*.tar.gz     # Upload to Hackage
cabal upload --publish dist-newstyle/*.tar.gz  # Publish (make public)
```

---

### stack
Another Haskell build tool. Uses "resolvers" (LTS Haskell snapshots) for reproducible builds.

```bash
# --- Install ---
curl -sSL https://get.haskellstack.org/ | sh
stack --version
stack upgrade                           # Update stack itself

# --- New Project ---
stack new <project>                     # Default template
stack new <project> <template>          # Specific template
stack new <project> simple              # Simple template

# --- Setup & Build ---
stack setup                             # Install GHC for this project
stack build                             # Build project
stack build --fast                      # No optimization (faster compile)
stack build --pedantic                  # -Wall -Werror
stack build --file-watch                # Watch + rebuild on changes
stack clean                             # Clean build artifacts
stack clean --full                      # Full clean including snapshots

# --- Running & Testing ---
stack run                               # Build + run main executable
stack exec <exe>                        # Run built executable
stack exec <exe> -- arg1 arg2          # With args
stack test                              # Run test suites
stack test --coverage                   # With coverage
stack bench                             # Run benchmarks
stack ghci                              # Launch GHCi REPL
stack repl                              # Same

# --- Dependencies ---
stack install <package>                 # Install binary tool
stack install --resolver lts-22.0       # Use specific resolver
stack list-dependencies                 # List all dependencies
stack ls dependencies                   # Same

# --- Resolvers & Snapshots ---
stack solver                            # Suggest resolver for deps
stack update                            # Update snapshot database
# stack.yaml: resolver: lts-22.0

# --- Docker ---
stack build --docker                    # Build inside Docker
stack test --docker
```

---

## Elixir — mix & hex

```bash
# --- Install (via asdf or official installer) ---
mix --version
elixir --version

# --- New Project ---
mix new <project>                       # New project
mix new <project> --module MyApp        # Custom module name
mix new <project> --sup                 # With OTP supervisor
mix phx.new <project>                   # Phoenix web app (install first)
mix phx.new <project> --no-ecto         # Phoenix without database
mix phx.new <project> --live            # With LiveView

# --- Fetching Dependencies ---
mix deps.get                            # Fetch all dependencies
mix deps.get --no-archives-check        # Skip archive checks
mix deps.update <dep>                   # Update specific dep
mix deps.update --all                   # Update all deps
mix deps.unlock <dep>                   # Unlock specific dep
mix deps.unlock --all                   # Unlock all deps
mix deps.clean <dep>                    # Remove built dep files
mix deps.clean --all                    # Clean all
mix deps.clean --unused                 # Clean only unused

# --- Building & Compiling ---
mix compile                             # Compile project
mix compile --warnings-as-errors        # Strict mode
mix deps.compile                        # Compile dependencies

# --- Running ---
mix run                                 # Run scripts/main entry
mix run -e "IO.puts 'hello'"            # Eval expression
iex -S mix                              # Start IEx with project loaded
mix phx.server                          # Start Phoenix server

# --- Testing ---
mix test                                # Run all tests
mix test test/my_test.exs               # Specific file
mix test test/my_test.exs:42            # Specific line
mix test --only tag:integration         # Filter by tag
mix test --trace                        # Verbose output
mix test --cover                        # Coverage (via ExCoveralls)

# --- Hex (Package Manager for Elixir) ---
mix hex.info                            # Show hex info
mix hex.search <query>                  # Search hex.pm
mix hex.info <package>                  # Package info
mix hex.outdated                        # List outdated deps
mix hex.audit                           # Security audit
mix hex.retire <pkg> <ver> <reason>    # Retire a version
mix hex.publish                         # Publish package to hex.pm
mix hex.publish --revert <ver>          # Unpublish a version

# --- Release ---
mix release                             # Build production release
mix release --overwrite                 # Overwrite existing release
MIX_ENV=prod mix release               # Production env

# --- Common Mix Tasks ---
mix format                              # Format code
mix format --check-formatted            # CI check
mix credo                               # Code quality analysis (install credo)
mix dialyzer                            # Type checking (install dialyxir)
mix ecto.create                         # Create database
mix ecto.migrate                        # Run migrations
mix ecto.rollback                       # Rollback last migration
mix ecto.reset                          # Drop + create + migrate
mix phx.gen.context                     # Generate context/schema
mix phx.routes                          # List routes
```

---

## Julia — Pkg

Julia has a built-in REPL-based package manager.

```julia
# Enter Pkg REPL: press ] in Julia REPL
# Exit Pkg REPL: press Backspace or Ctrl+C

# --- Adding Packages ---
add <Package>                  # Install latest
add <Package>@1.2.3            # Specific version
add <Package>@^1.2             # Compatible with 1.2
add <Package>#main             # From git main branch
add https://github.com/u/r    # From git URL
add ./local-package            # From local path
add <Package1> <Package2>     # Multiple packages

# --- Removing Packages ---
rm <Package>                   # Remove package
rm <Package1> <Package2>

# --- Updating ---
update                         # Update all packages
update <Package>               # Update specific package
up                             # Short alias

# --- Status & Info ---
status                         # Show installed packages (short: st)
status <Package>               # Show specific package
status --outdated              # Only outdated
instantiate                    # Install exact versions from Manifest.toml

# --- Project Environments ---
activate .                     # Activate current dir as project
activate ./myproject           # Activate specific project
activate --temp                # Create temp environment
activate                       # Activate global default env
resolve                        # Re-resolve project deps

# --- Developing Packages ---
develop <Package>              # Install as mutable (for dev)
develop .                      # Develop current package
develop https://github.com/u/r
free <Package>                 # Return to registry version

# --- Pin & Undo ---
pin <Package>                  # Pin to current version
free <Package>                 # Unpin package
undo                           # Undo last operation
redo                           # Redo last undone operation

# --- Building ---
build <Package>                # Rebuild package artifacts
build                          # Rebuild all packages

# --- Testing ---
test <Package>                 # Test a package
test                           # Test current project

# --- Precompiling ---
precompile                     # Precompile all packages

# --- Registry ---
registry add <url>             # Add a registry
registry remove <name>         # Remove a registry
registry status                # Show registries
registry update                # Update registries

# --- Scripting (Pkg API) ---
using Pkg
Pkg.add("Package")
Pkg.add(PackageSpec(name="Package", version="1.2.3"))
Pkg.rm("Package")
Pkg.update()
Pkg.status()
Pkg.instantiate()
Pkg.activate(".")
Pkg.test("Package")
```

---

## R

```r
# --- Base R package management ---

# Installing packages
install.packages("package")              # From CRAN
install.packages(c("pkg1", "pkg2"))      # Multiple packages
install.packages("package", repos = "https://cran.rstudio.com/")
install.packages("package", dependencies = TRUE)  # Include suggested deps
install.packages("package", lib = "~/R/custom_lib")  # Custom library path

# Removing packages
remove.packages("package")
remove.packages(c("pkg1", "pkg2"))

# Loading packages
library(package)                         # Load + attach (error if missing)
require(package)                         # Load + attach (warning if missing)
requireNamespace("package", quietly = TRUE)  # Load without attaching

# Updating packages
update.packages()                        # Update all
update.packages(ask = FALSE)             # Non-interactive update
update.packages("package")              # Update specific package
old.packages()                           # List outdated packages

# Listing & Info
installed.packages()                     # List installed (returns matrix)
rownames(installed.packages())           # Just package names
packageVersion("package")               # Show version
packageDescription("package")           # Show description
citation("package")                      # How to cite package

# GitHub / remote sources (devtools)
install.packages("devtools")
devtools::install_github("user/repo")
devtools::install_github("user/repo@v1.2.3")  # Tag
devtools::install_github("user/repo", ref = "main")  # Branch
devtools::install_gitlab("user/repo")
devtools::install_bitbucket("user/repo")
devtools::install_local("./path/to/package")
devtools::install_url("https://...")

# --- pak (modern package manager for R) ---
install.packages("pak")
pak::pkg_install("package")             # From CRAN
pak::pkg_install("user/repo")           # From GitHub
pak::pkg_install("package@1.2.3")       # Specific version
pak::pkg_install(c("pkg1", "pkg2"))     # Multiple
pak::pkg_remove("package")             # Remove
pak::pkg_update()                       # Update all
pak::pkg_update("package")             # Update specific
pak::pkg_status("package")             # Show status
pak::pkg_deps("package")               # Show dependencies
pak::pkg_deps_tree("package")           # Dependency tree
pak::cache_delete()                     # Clear pak cache

# --- renv (reproducible R environments) ---
install.packages("renv")
renv::init()                            # Initialize project environment
renv::install("package")               # Install in project env
renv::remove("package")                # Remove from project
renv::update()                          # Update packages
renv::snapshot()                        # Update renv.lock
renv::restore()                         # Restore from renv.lock
renv::status()                          # Show environment status
renv::activate()                        # Activate renv for project
renv::deactivate()                      # Deactivate renv
renv::clean()                           # Remove unused packages
renv::upgrade()                         # Upgrade renv itself
renv::dependencies()                    # List all package dependencies

# --- BiocManager (Bioconductor) ---
install.packages("BiocManager")
BiocManager::install("GenomicRanges")   # Install Bioc package
BiocManager::install()                  # Update all Bioc packages
BiocManager::version()                  # Show Bioconductor version
BiocManager::available("RNA")           # Search available packages
```

---

## Lua — LuaRocks

```bash
# --- Install ---
# macOS:  brew install luarocks
# Linux:  sudo apt install luarocks  OR  sudo dnf install luarocks
# Windows: https://luarocks.org/
luarocks --version

# --- Installing Rocks ---
luarocks install <rock>                 # Install latest
luarocks install <rock> 1.2.3          # Specific version
luarocks install <rock> --dev          # Development version
luarocks install <rock> --tree ./deps   # Local tree (project-specific)
luarocks install <rock> --local         # Install to user tree

# --- Removing Rocks ---
luarocks remove <rock>                  # Remove latest
luarocks remove <rock> 1.2.3           # Specific version

# --- Searching ---
luarocks search <query>                 # Search luarocks.org
luarocks show <rock>                    # Show rock info
luarocks list                           # List installed rocks

# --- Building from Rockspec ---
luarocks build <rockspec>               # Build from .rockspec file
luarocks build                          # Build from rockspec in current dir
luarocks make                           # Build + install from local rockspec
luarocks pack <rockspec>                # Create .rock archive

# --- Managing Trees ---
luarocks path                           # Show Lua path variables
luarocks path --bin                     # Show bin directory
eval $(luarocks path --bin)             # Add to PATH
luarocks --tree ./deps path            # Scoped to local tree

# --- Uploading ---
luarocks upload <rock>.rockspec         # Upload to luarocks.org
luarocks upload <rock>-1.0-1.src.rock
```

---

## C / C++

### Conan

Package manager for C and C++ libraries.

```bash
# --- Install ---
pip install conan
conan --version
conan config home                       # Show config home

# --- Profile Setup (required first time) ---
conan profile detect                    # Auto-detect and create default profile
conan profile list                      # List profiles
conan profile show default              # Show default profile
conan profile new myprofile --detect    # Create named profile

# --- Installing Dependencies ---
conan install .                         # Install from conanfile.txt/py in .
conan install . --build=missing         # Build missing packages from source
conan install . -s build_type=Debug     # Debug build
conan install . -s build_type=Release   # Release build
conan install . -pr myprofile           # Use specific profile
conan install . -o <package>:option=True  # Set package option
conan install --requires="<pkg>/1.2.3" # Install without conanfile

# --- Building ---
conan build .                           # Build using conanfile
conan create .                          # Create package (build + test)
conan create . --name mypkg --version 1.0
conan create . -pr:b default -pr:h myprofile

# --- Searching ---
conan search "*"                        # List all local cached packages
conan search <package>                  # Search local cache
conan search <package> -r conancenter   # Search ConanCenter remote
conan list <package>/*:* -r conancenter # Detailed search on remote

# --- Cache & Removing ---
conan remove <package>                  # Remove from local cache
conan remove "*"                        # Remove all from cache
conan cache clean                       # Clean unused packages
conan cache path <package>/<version>    # Show package cache path

# --- Remotes ---
conan remote list                       # List remotes
conan remote add <name> <url>           # Add remote
conan remote remove <name>              # Remove remote
conan remote enable/disable <name>      # Enable/disable

# --- Lockfile ---
conan lock create .                     # Create conan.lock
conan install . --lockfile conan.lock   # Install from lockfile

# --- Publishing ---
conan upload <package> -r <remote>      # Upload to remote
conan upload "*" -r myserver            # Upload all to remote
```

---

### vcpkg

Microsoft's C/C++ package manager. Integrates with CMake/MSBuild.

```bash
# --- Install ---
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh                    # macOS/Linux
.\bootstrap-vcpkg.bat                   # Windows
./vcpkg integrate install               # Integrate with Visual Studio / CMake

vcpkg --version
vcpkg upgrade --no-dry-run              # Upgrade vcpkg itself

# --- Installing Packages ---
vcpkg install <package>                 # Install for default triplet
vcpkg install <package>:x64-linux       # Specific triplet
vcpkg install <package>:x64-windows     # Windows 64-bit
vcpkg install <package>:arm64-osx       # macOS Apple Silicon
vcpkg install <pkg1> <pkg2> <pkg3>      # Multiple packages
vcpkg install <package>[feature1,feature2]  # With features

# --- Removing Packages ---
vcpkg remove <package>                  # Remove package
vcpkg remove <package>:x64-linux
vcpkg remove --outdated                 # Remove outdated packages

# --- Updating ---
vcpkg upgrade                           # Show packages that would be upgraded
vcpkg upgrade --no-dry-run              # Actually upgrade

# --- Searching & Info ---
vcpkg search <query>                    # Search available packages
vcpkg list                              # List installed packages
vcpkg show <package>                    # Show package info

# --- CMake Integration ---
# Add to CMakeLists.txt or CLI:
cmake -DCMAKE_TOOLCHAIN_FILE=/path/to/vcpkg/scripts/buildsystems/vcpkg.cmake ..
# Or set VCPKG_ROOT environment variable

# --- Manifest Mode (vcpkg.json) ---
# Create vcpkg.json in project root with dependencies
vcpkg install                           # Install from vcpkg.json
vcpkg x-update-baseline --add-initial-baseline  # Set baseline

# --- Ports (create/update packages) ---
vcpkg create <package> <url> <sha512>   # Scaffold new port
vcpkg edit <package>                    # Edit portfile
vcpkg format-manifest vcpkg.json        # Format manifest file
```

---

## Perl — cpan & cpanm

```bash
# --- cpan (built-in) ---
cpan                                    # Interactive REPL
cpan <Module>                           # Install module
cpan <Module1> <Module2>               # Multiple modules
cpan -i <Module>                        # Force install
cpan -u                                 # Upgrade all modules
cpan -l                                 # List installed modules
cpan -a                                 # Make CPAN authors file

# In cpan REPL:
# install Module::Name
# upgrade Module::Name
# uninstall Module::Name
# test Module::Name
# look Module::Name     # Enter module's build dir

# --- cpanm (recommended, much simpler) ---
# Install cpanm:
curl -L https://cpanmin.us | perl - App::cpanminus
# OR: cpan App::cpanminus

cpanm <Module>                          # Install module
cpanm <Module>@1.23                     # Specific version
cpanm <Module> --notest                 # Skip tests (faster)
cpanm <Module> --force                  # Force install
cpanm <Module> -n                       # Short for --notest
cpanm --installdeps .                   # Install deps from cpanfile
cpanm --with-develop .                  # Include develop deps
cpanm --without-feature <f> .           # Skip optional feature
cpanm -L ./local <Module>               # Install to local/ directory
cpanm --self-upgrade                    # Upgrade cpanm itself

# --- cpanfile (Perl equivalent of requirements.txt) ---
# requires 'Some::Module', '1.23';
# requires 'Other::Module', '>= 2.0, < 3.0';
# recommends 'Optional::Module';
# on 'develop' => sub { requires 'Devel::NYTProf' };

# --- local::lib (user-level installs) ---
cpanm --local-lib ~/perl5 <Module>
eval $(perl -I ~/perl5/lib/perl5 -Mlocal::lib)

# --- Carton (bundler for Perl) ---
cpanm Carton
carton install                          # Install from cpanfile.snapshot
carton install --deployment             # Production install (no updates)
carton update                           # Update all deps
carton exec perl script.pl              # Run in carton environment
```

---

## Erlang — rebar3

Build tool and package manager for Erlang.

```bash
# --- Install ---
# Download from https://github.com/erlang/rebar3/releases
# OR: brew install rebar3
rebar3 --version

# --- New Project ---
rebar3 new app <name>                   # OTP application
rebar3 new lib <name>                   # Library
rebar3 new release <name>               # Release with config
rebar3 new escript <name>               # Escript (runnable script)
rebar3 new plugin <name>                # rebar3 plugin

# --- Fetching Dependencies (rebar.config) ---
rebar3 get-deps                         # Fetch all deps
rebar3 upgrade                          # Upgrade all deps
rebar3 upgrade <dep>                    # Upgrade specific dep
rebar3 unlock --all                     # Unlock all deps
rebar3 unlock <dep>                     # Unlock specific dep

# --- Building ---
rebar3 compile                          # Compile project
rebar3 clean                            # Clean artifacts

# --- Testing ---
rebar3 eunit                            # Run EUnit tests
rebar3 ct                               # Run Common Test suites
rebar3 cover                            # Generate coverage report
rebar3 dialyzer                         # Type analysis
rebar3 xref                             # Cross-reference analysis

# --- Running ---
rebar3 shell                            # Start Erlang shell with project
rebar3 run                              # Run release (if configured)

# --- Releases ---
rebar3 release                          # Build release
rebar3 tar                              # Build tarball release

# --- Hex (Erlang packages via hex.pm) ---
rebar3 hex search <query>               # Search hex.pm
rebar3 hex info <package>               # Package info
rebar3 hex publish                      # Publish to hex.pm
rebar3 hex retire <pkg> <ver> <reason>  # Retire version
```

---

## Nim — nimble

Package manager for the Nim programming language.

```bash
# --- Install (with Nim) ---
# Install via choosenim: https://github.com/dom96/choosenim
choosenim stable
nim --version
nimble --version

# --- Installing Packages ---
nimble install <package>                # Install package
nimble install <package>@1.2.3          # Specific version
nimble install <package>@>1.0           # Version range
nimble install                          # Install from .nimble file (project deps)
nimble develop                          # Install deps + add current dir to path

# --- Removing Packages ---
nimble uninstall <package>              # Remove package
nimble uninstall <package>@1.2.3        # Specific version

# --- Searching ---
nimble search <query>                   # Search nimble package directory
nimble list                             # List all available packages
nimble list --installed                 # List installed packages

# --- Building & Running ---
nimble build                            # Build project
nimble run                              # Build and run
nimble run <task>                       # Run specific task
nimble test                             # Run tests
nimble check                            # Check .nimble file validity

# --- Publishing ---
nimble publish                          # Publish to nim packages repo (via PR)
nimble init                             # Create new .nimble project

# --- Version Management (choosenim) ---
choosenim update self                   # Update choosenim
choosenim show                          # Show current Nim version
choosenim 1.6.14                        # Switch to specific version
choosenim stable                        # Switch to latest stable
choosenim devel                         # Switch to development version
choosenim list                          # List installed versions
choosenim remove 1.6.14                 # Remove a version
```

---

## Zig — zig build

Zig's built-in build system and package manager (0.12+).

```bash
# --- Install ---
# Download from https://ziglang.org/download/
zig version

# --- Project Setup ---
zig init                                # Initialize project (zig 0.12+)
zig init-exe                            # Executable project (older)
zig init-lib                            # Library project (older)

# --- Building ---
zig build                               # Build using build.zig
zig build -Doptimize=Debug              # Debug build
zig build -Doptimize=ReleaseSafe        # Release with safety checks
zig build -Doptimize=ReleaseFast        # Maximum performance
zig build -Doptimize=ReleaseSmall       # Minimize binary size
zig build -Dtarget=x86_64-linux-gnu     # Cross-compile
zig build install                       # Build and install to zig-out/
zig build --prefix ./dist               # Custom install prefix

# --- Running & Testing ---
zig build run                           # Build and run
zig build run -- arg1 arg2             # With arguments
zig build test                          # Run tests
zig build test --summary all            # With full summary

# --- Direct Compilation (without build.zig) ---
zig run main.zig                        # Compile and run
zig test main.zig                       # Compile and run tests
zig build-exe main.zig                  # Build executable
zig build-lib lib.zig                   # Build library
zig build-obj file.zig                  # Build object file

# --- Cross-Compilation ---
zig build-exe main.zig -target x86_64-windows-gnu
zig build-exe main.zig -target aarch64-macos
zig targets                             # List all supported targets

# --- Packages (build.zig.zon, Zig 0.11+) ---
# build.zig.zon declares dependencies with .url and .hash
zig fetch --save <url>                  # Download and add to build.zig.zon
zig fetch --save git+https://github.com/user/repo.git
zig build --fetch                       # Download all deps

# --- Formatting ---
zig fmt <file>.zig                      # Format a file
zig fmt .                               # Format all .zig files
zig fmt --check .                       # Check without modifying

# --- Translation ---
zig translate-c file.h                  # Translate C header to Zig
```

---

## Cross-Language Quick Reference Table

| Language   | Tool        | Add Package               | Remove Package             | Update All       | List Installed    | Config File          |
|------------|-------------|---------------------------|----------------------------|------------------|-------------------|----------------------|
| Python     | pip         | `pip install <pkg>`       | `pip uninstall <pkg>`      | `pip install -U` | `pip list`        | requirements.txt     |
| Python     | poetry      | `poetry add <pkg>`        | `poetry remove <pkg>`      | `poetry update`  | `poetry show`     | pyproject.toml       |
| Python     | uv          | `uv add <pkg>`            | `uv remove <pkg>`          | `uv sync`        | `uv pip list`     | pyproject.toml       |
| Python     | conda       | `conda install <pkg>`     | `conda remove <pkg>`       | `conda update --all` | `conda list`  | environment.yml      |
| Rust       | cargo       | `cargo add <pkg>`         | `cargo remove <pkg>`       | `cargo update`   | `cargo tree`      | Cargo.toml           |
| Go         | go          | `go get <pkg>`            | `go mod tidy`              | `go get -u ./..` | `go list -m all`  | go.mod               |
| Ruby       | gem         | `gem install <gem>`       | `gem uninstall <gem>`      | `gem update`     | `gem list`        | Gemfile              |
| Ruby       | bundler     | `bundle add <gem>`        | `bundle remove <gem>`      | `bundle update`  | `bundle list`     | Gemfile.lock         |
| PHP        | composer    | `composer require <pkg>`  | `composer remove <pkg>`    | `composer update`| `composer show`   | composer.json        |
| Java       | maven       | edit pom.xml              | edit pom.xml               | `mvn versions:use-latest-releases` | `mvn dependency:list` | pom.xml |
| Java       | gradle      | edit build.gradle         | edit build.gradle          | `gradle dependencyUpdates` | `gradle dependencies` | build.gradle |
| .NET/C#    | dotnet      | `dotnet add package <pkg>`| `dotnet remove package`    | —                | `dotnet list pkg` | .csproj              |
| Swift      | spm         | edit Package.swift        | edit Package.swift         | `swift package update` | `swift package show-dependencies` | Package.swift |
| Dart       | pub         | `dart pub add <pkg>`      | `dart pub remove <pkg>`    | `dart pub upgrade`| `dart pub deps`  | pubspec.yaml         |
| Haskell    | cabal       | edit .cabal               | edit .cabal                | `cabal update`   | `cabal list`      | *.cabal              |
| Haskell    | stack       | edit package.yaml         | edit package.yaml          | `stack update`   | `stack ls deps`   | stack.yaml           |
| Elixir     | mix/hex     | edit mix.exs              | edit mix.exs               | `mix deps.update --all` | `mix deps` | mix.exs         |
| Julia      | Pkg         | `add <pkg>`               | `rm <pkg>`                 | `update`         | `status`          | Project.toml         |
| R          | pak         | `pak::pkg_install("pkg")` | `remove.packages("pkg")`   | `pak::pkg_update()` | `installed.packages()` | renv.lock    |
| Lua        | luarocks    | `luarocks install <rock>` | `luarocks remove <rock>`   | `luarocks upgrade`| `luarocks list`  | rockspec             |
| Perl       | cpanm       | `cpanm <Module>`          | —                          | `cpanm --self-upgrade` | `cpan -l`   | cpanfile             |
| Erlang     | rebar3      | edit rebar.config         | edit rebar.config          | `rebar3 upgrade` | `rebar3 pkgs`     | rebar.config         |
| Nim        | nimble      | `nimble install <pkg>`    | `nimble uninstall <pkg>`   | `nimble refresh` | `nimble list --installed` | *.nimble    |
| Zig        | zig build   | `zig fetch --save <url>`  | edit build.zig.zon         | —                | —                 | build.zig.zon        |
