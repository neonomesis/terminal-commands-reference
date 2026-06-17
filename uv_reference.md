# uv Reference Guide

A complete reference for `uv` — an extremely fast Python package and project manager, written in Rust (by Astral).

---

## Table of Contents

1. [Installation](#1-installation)
2. [Python Version Management](#2-python-version-management)
3. [Project Management](#3-project-management)
4. [Virtual Environments](#4-virtual-environments)
5. [Package Management](#5-package-management)
6. [Running Scripts & Tools](#6-running-scripts--tools)
7. [Tool Management (uvx)](#7-tool-management-uvx)
8. [Lock Files & Reproducibility](#8-lock-files--reproducibility)
9. [Workspaces](#9-workspaces)
10. [Build & Publish](#10-build--publish)
11. [Configuration](#11-configuration)
12. [uv vs pip / Poetry / Pipenv](#12-uv-vs-pip--poetry--pipenv)
13. [Common Recipes](#13-common-recipes)

---

## 1. Installation

```bash
# macOS / Linux (recommended)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# pip
pip install uv

# Homebrew
brew install uv

# Check version
uv --version

# Self-update
uv self update
```

---

## 2. Python Version Management

uv can install and manage multiple Python versions without pyenv.

```bash
uv python list                          # List available Python versions
uv python list --only-installed         # Show only installed versions
uv python install 3.12                  # Install Python 3.12
uv python install 3.11 3.12 3.13        # Install multiple versions
uv python install                       # Install version from .python-version / pyproject.toml
uv python pin 3.12                      # Pin project to Python 3.12 (writes .python-version)
uv python find                          # Show path of current Python interpreter
uv python find 3.11                     # Find path of Python 3.11
uv python uninstall 3.11                # Remove Python 3.11
```

---

## 3. Project Management

uv manages projects with `pyproject.toml` (like Poetry but faster).

```bash
uv init                                 # Init project in current directory
uv init my-project                      # Create new project folder
uv init --lib my-lib                    # Create a library project (src layout)
uv init --app my-app                    # Create an application project
uv init --script my-script.py          # Create a standalone script with inline deps

uv sync                                 # Install all dependencies from lockfile
uv sync --frozen                        # Sync without updating uv.lock
uv sync --no-dev                        # Skip dev dependencies
uv sync --group test                    # Sync specific dependency group

uv run python main.py                   # Run inside the project environment
uv run pytest                           # Run command inside the project environment
uv run --python 3.12 python main.py     # Run with a specific Python version
```

> `uv run` automatically creates/updates the virtual environment before executing.

---

## 4. Virtual Environments

```bash
uv venv                                 # Create .venv in current directory
uv venv myenv                           # Create venv named myenv
uv venv --python 3.11                   # Create venv with specific Python
uv venv --python python3.12             # Use system Python 3.12
uv venv --seed                          # Include pip/setuptools/wheel in venv

# Activate (same as plain venv)
source .venv/bin/activate               # macOS / Linux
.venv\Scripts\activate                  # Windows

# Deactivate
deactivate
```

---

## 5. Package Management

### Installing packages

```bash
uv add requests                         # Add dependency to pyproject.toml + install
uv add "requests>=2.28"                 # Add with version constraint
uv add requests httpx rich              # Add multiple packages
uv add --dev pytest ruff                # Add to dev dependencies
uv add --group test pytest              # Add to custom dependency group
uv add --optional extra requests        # Add to optional dependency group

uv pip install requests                 # pip-compatible install (no pyproject.toml needed)
uv pip install -r requirements.txt      # Install from requirements file
uv pip install -e .                     # Editable install
uv pip install ".[dev]"                 # Install with extras
```

### Removing packages

```bash
uv remove requests                      # Remove dependency from pyproject.toml
uv remove --dev pytest                  # Remove dev dependency
uv pip uninstall requests               # pip-compatible uninstall
```

### Listing packages

```bash
uv pip list                             # List installed packages
uv pip list --outdated                  # Show outdated packages
uv pip show requests                    # Show package info
uv tree                                 # Show dependency tree
uv pip freeze                           # Output requirements.txt format
```

### Upgrading packages

```bash
uv lock --upgrade                       # Upgrade all packages in lockfile
uv lock --upgrade-package requests      # Upgrade a single package
uv add "requests>=2.32" --upgrade       # Upgrade to a new constraint
```

---

## 6. Running Scripts & Tools

```bash
uv run script.py                        # Run script in project environment
uv run --with requests script.py        # Run with extra package (not installed permanently)
uv run --with "httpx>=0.27" script.py   # Run with version constraint

# Inline script dependencies (PEP 723)
# Add this to top of script.py:
# /// script
# requires-python = ">=3.11"
# dependencies = ["requests", "rich"]
# ///
uv run script.py                        # uv reads inline deps and runs isolated
```

---

## 7. Tool Management (uvx)

`uvx` runs tools in temporary isolated environments — like `npx` for Python.

```bash
uvx ruff check .                        # Run ruff without installing globally
uvx black .                             # Run black
uvx --from cowsay cowsay "hello"        # Run tool from a package with different name
uvx --python 3.11 ruff check .          # Run tool with specific Python
uvx --with requests my-tool             # Run tool with extra dependency

# Install tools globally (persisted)
uv tool install ruff                    # Install ruff as global tool
uv tool install black --python 3.12     # Install with specific Pyt
uv tool list                            # List installed tools
uv tool upgrade ruff                    # Upgrade a global tool
uv tool upgrade --all                   # Upgrade all global tools
uv tool uninstall ruff                  # Remove global tool
uv tool run ruff check .                # Explicit form of uvx
```

---

## 8. Lock Files & Reproducibility

```bash
uv lock                                 # Generate/update uv.lock (no install)
uv lock --check                         # Verify lockfile is up to date (CI use)
uv lock --upgrade                       # Regenerate lockfile with latest deps
uv export -o requirements.txt           # Export lockfile to requirements.txt
uv export --no-hashes -o requirements.txt  # Export without hash pins
uv export --group dev -o dev-requirements.txt
uv pip compile pyproject.toml -o requirements.txt  # pip-compile compatible workflow
```

> Always commit `uv.lock` for applications; omit it for libraries.

---

## 9. Workspaces

A workspace groups multiple related packages under one root.

```toml
# pyproject.toml (root)
[tool.uv.workspace]
members = ["packages/*"]
```

```bash
uv sync                                 # Sync all workspace members
uv run --package my-lib pytest          # Run in a specific workspace member
uv add my-lib --workspace               # Add workspace member as dependency
```

---

## 10. Build & Publish

```bash
uv build                                # Build sdist + wheel into dist/
uv build --sdist                        # Build source distribution only
uv build --wheel                        # Build wheel only
uv publish                              # Publish to PyPI
uv publish --token $PYPI_TOKEN          # Publish with API token
uv publish --index-url https://test.pypi.org/legacy/  # Publish to TestPyPI
```

---

## 11. Configuration

uv reads config from `pyproject.toml` or `uv.toml`.

```toml
# pyproject.toml
[tool.uv]
python-version = "3.12"
dev-dependencies = ["pytest>=8", "ruff"]

[[tool.uv.index]]
name = "private"
url = "https://my.registry.com/simple/"
default = true

[tool.uv.pip]
index-url = "https://pypi.org/simple"
extra-index-url = ["https://my.registry.com/simple/"]
```

### Environment variables

```bash
UV_PYTHON=3.12                          # Override Python version
UV_CACHE_DIR=~/.cache/uv               # Custom cache location
UV_INDEX_URL=https://...               # Custom index URL
UV_EXTRA_INDEX_URL=https://...         # Additional index URL
UV_NO_CACHE=1                          # Disable cache
UV_SYSTEM_PYTHON=1                     # Allow using system Python
UV_COMPILE_BYTECODE=1                  # Pre-compile .pyc files on install
UV_LINK_MODE=copy                      # copy | hardlink | symlink | clone
```

### Cache management

```bash
uv cache dir                            # Show cache directory path
uv cache clean                          # Clear entire cache
uv cache clean requests                 # Clear cache for a single package
uv cache prune                          # Remove unused cache entries
```

---

## 12. uv vs pip / Poetry / Pipenv

| Feature                | pip         | Poetry | Pipenv | **uv**             |
| ---------------------- | ----------- | ------ | ------ | ------------------ |
| Speed                  | Slow        | Slow   | Slow   | **10–100× faster** |
| Python management      | No          | No     | Yes    | **Yes**            |
| Lock file              | No (manual) | Yes    | Yes    | **Yes**            |
| Virtual env mgmt       | No          | Yes    | Yes    | **Yes**            |
| Tool runner (npx-like) | No          | No     | No     | **Yes (uvx)**      |
| pip-compatible API     | —           | No     | No     | **Yes (uv pip)**   |
| Workspaces             | No          | No     | No     | **Yes**            |
| Written in             | Python      | Python | Python | **Rust**           |
| pyproject.toml native  | No          | Yes    | No     | **Yes**            |

---

## 13. Common Recipes

```bash
# Start a new project from scratch
uv init my-app && cd my-app
uv add fastapi uvicorn
uv run uvicorn main:app --reload

# One-liner: run a tool without installing
uvx httpie GET https://httpbin.org/get

# Convert existing requirements.txt project
uv pip install -r requirements.txt

# Reproducible CI install
uv sync --frozen --no-dev

# Pin Python version for the project
uv python pin 3.12

# Export lockfile for Docker
uv export --no-hashes -o requirements.txt

# Run tests with coverage
uv run pytest --cov=src

# Format + lint with ruff (no install needed)
uvx ruff format .
uvx ruff check . --fix

# Upgrade all deps and sync
uv lock --upgrade && uv sync

# Create isolated script with inline dependencies
cat > fetch.py << 'EOF'
# /// script
# requires-python = ">=3.11"
# dependencies = ["httpx", "rich"]
# ///
import httpx
from rich import print
print(httpx.get("https://httpbin.org/get").json())
EOF
uv run fetch.py
```

---

> **Docs:** https://docs.astral.sh/uv  
> **GitHub:** https://github.com/astral-sh/uv
