# ESLint Reference

ESLint is a static analysis tool for JavaScript/TypeScript that finds and fixes problems in your code.

---

## Installation

```bash
# Install locally (recommended)
npm install --save-dev eslint

# Initialize config
npx eslint --init

# Or with a specific config package
npm init @eslint/config
```

---

## Config Files

### Flat Config (v9+, current default) — `eslint.config.js`

```js
import js from "@eslint/js";

export default [
	js.configs.recommended,
	{
		files: ["**/*.js"],
		rules: {
			"no-unused-vars": "warn",
			"no-console": "off",
			semi: ["error", "always"],
		},
	},
];
```

### Legacy Config (v8 and below) — `.eslintrc.json`

```json
{
	"env": {
		"browser": true,
		"es2021": true,
		"node": true
	},
	"extends": ["eslint:recommended"],
	"rules": {
		"no-unused-vars": "warn",
		"semi": ["error", "always"]
	}
}
```

---

## CLI Commands

```bash
# Lint a file or directory
npx eslint src/

# Lint and auto-fix fixable issues
npx eslint src/ --fix

# Lint specific file types
npx eslint src/ --ext .js,.ts,.jsx,.tsx

# Print config for a file (debugging)
npx eslint --print-config src/index.js

# Lint with a custom config file
npx eslint --config my-config.js src/

# Quiet mode (only errors, no warnings)
npx eslint src/ --quiet

# Output as JSON
npx eslint src/ --format json

# Cache results for faster re-runs
npx eslint src/ --cache
```

---

## Rule Severity Levels

| Value           | Meaning                |
| --------------- | ---------------------- |
| `0` / `"off"`   | Disable the rule       |
| `1` / `"warn"`  | Warning (non-breaking) |
| `2` / `"error"` | Error (exit code 1)    |

```json
{
	"rules": {
		"no-console": "off",
		"eqeqeq": "warn",
		"semi": ["error", "always"]
	}
}
```

---

## Common Rules

```json
{
	"rules": {
		"no-unused-vars": "warn",
		"no-undef": "error",
		"no-console": "warn",
		"eqeqeq": ["error", "always"],
		"semi": ["error", "always"],
		"quotes": ["error", "single"],
		"indent": ["error", 2],
		"comma-dangle": ["error", "always-multiline"],
		"no-var": "error",
		"prefer-const": "error",
		"arrow-body-style": ["error", "as-needed"],
		"object-shorthand": ["error", "always"]
	}
}
```

---

## Soft Rules (warn — non-breaking)

These rules flag code quality and style concerns without blocking CI. Good starting point when adding lint to an existing project.

### Code Quality

```json
{
	"rules": {
		"no-unused-vars": "warn",
		"no-console": "warn",
		"no-debugger": "warn",
		"no-alert": "warn",
		"no-todo-comments": "off",
		"no-empty": "warn",
		"no-empty-function": "warn",
		"no-lonely-if": "warn",
		"no-negated-condition": "warn",
		"no-nested-ternary": "warn",
		"no-unneeded-ternary": "warn",
		"no-useless-return": "warn",
		"no-useless-concat": "warn",
		"no-useless-rename": "warn",
		"no-shadow": "warn",
		"no-param-reassign": "warn",
		"no-else-return": "warn",
		"consistent-return": "warn",
		"default-case": "warn"
	}
}
```

### Modern JavaScript Suggestions

```json
{
	"rules": {
		"prefer-const": "warn",
		"prefer-arrow-callback": "warn",
		"prefer-template": "warn",
		"prefer-destructuring": ["warn", { "array": false, "object": true }],
		"prefer-rest-params": "warn",
		"prefer-spread": "warn",
		"prefer-object-spread": "warn",
		"prefer-numeric-literals": "warn",
		"prefer-exponentiation-operator": "warn",
		"object-shorthand": ["warn", "always"],
		"arrow-body-style": ["warn", "as-needed"],
		"no-var": "warn",
		"require-await": "warn",
		"no-return-await": "warn"
	}
}
```

### Readability & Style

```json
{
	"rules": {
		"spaced-comment": ["warn", "always"],
		"capitalized-comments": [
			"warn",
			"always",
			{ "ignoreInlineComments": true }
		],
		"multiline-comment-style": ["warn", "starred-block"],
		"yoda": ["warn", "never"],
		"curly": ["warn", "multi-line"],
		"dot-notation": "warn",
		"eqeqeq": ["warn", "always"],
		"no-implicit-coercion": "warn",
		"operator-assignment": ["warn", "always"],
		"sort-imports": ["warn", { "ignoreDeclarationSort": true }],
		"no-magic-numbers": [
			"warn",
			{ "ignore": [0, 1, -1], "ignoreArrayIndexes": true }
		]
	}
}
```

### Complexity Limits

```json
{
	"rules": {
		"complexity": ["warn", 10],
		"max-depth": ["warn", 4],
		"max-lines": ["warn", 300],
		"max-lines-per-function": ["warn", 60],
		"max-params": ["warn", 4],
		"max-statements": ["warn", 20]
	}
}
```

### TypeScript Soft Rules (`@typescript-eslint`)

```json
{
	"rules": {
		"@typescript-eslint/no-explicit-any": "warn",
		"@typescript-eslint/no-unused-vars": "warn",
		"@typescript-eslint/no-inferrable-types": "warn",
		"@typescript-eslint/prefer-optional-chain": "warn",
		"@typescript-eslint/prefer-nullish-coalescing": "warn",
		"@typescript-eslint/no-non-null-assertion": "warn",
		"@typescript-eslint/consistent-type-imports": [
			"warn",
			{ "prefer": "type-imports" }
		],
		"@typescript-eslint/no-empty-interface": "warn",
		"@typescript-eslint/ban-ts-comment": "warn"
	}
}
```

### React Soft Rules (`eslint-plugin-react`, `eslint-plugin-react-hooks`)

```json
{
	"rules": {
		"react/prop-types": "warn",
		"react/no-unused-prop-types": "warn",
		"react/self-closing-comp": "warn",
		"react/jsx-no-useless-fragment": "warn",
		"react/jsx-curly-brace-presence": ["warn", "never"],
		"react/no-array-index-key": "warn",
		"react/prefer-stateless-function": "warn",
		"react-hooks/exhaustive-deps": "warn"
	}
}
```

---

## All-Warn Starter Config

Drop-in config that sets every rule to `warn` — useful for onboarding lint into a legacy codebase without breaking the build:

```js
// eslint.config.js
import js from "@eslint/js";

function allWarn(rules) {
	return Object.fromEntries(
		Object.entries(rules).map(([key, val]) => {
			const severity = Array.isArray(val) ? val[0] : val;
			if (severity === "error" || severity === 2) {
				return [key, Array.isArray(val) ? ["warn", ...val.slice(1)] : "warn"];
			}
			return [key, val];
		}),
	);
}

export default [
	{
		rules: allWarn(js.configs.recommended.rules),
	},
];
```

---

## Ignoring Files

### Flat config (`eslint.config.js`)

```js
export default [{ ignores: ["dist/", "node_modules/", "*.min.js"] }];
```

### Legacy (`.eslintignore`)

```
node_modules/
dist/
build/
*.min.js
```

### Inline ignoring

```js
// eslint-disable-next-line no-console
console.log("debug");

/* eslint-disable no-unused-vars */
const unused = 1;
/* eslint-enable no-unused-vars */

// eslint-disable-file -- disable for entire file
```

---

## TypeScript Support

```bash
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

```js
// eslint.config.js (flat)
import tsPlugin from "@typescript-eslint/eslint-plugin";
import tsParser from "@typescript-eslint/parser";

export default [
	{
		files: ["**/*.ts", "**/*.tsx"],
		languageOptions: { parser: tsParser },
		plugins: { "@typescript-eslint": tsPlugin },
		rules: {
			...tsPlugin.configs.recommended.rules,
			"@typescript-eslint/no-explicit-any": "warn",
		},
	},
];
```

---

## Popular Plugins & Configs

| Package                     | Purpose                                         |
| --------------------------- | ----------------------------------------------- |
| `eslint-plugin-react`       | React-specific rules                            |
| `eslint-plugin-react-hooks` | Enforce hooks rules                             |
| `eslint-plugin-import`      | Import/export linting                           |
| `eslint-plugin-jsx-a11y`    | Accessibility rules                             |
| `eslint-plugin-n`           | Node.js rules                                   |
| `@typescript-eslint`        | TypeScript rules                                |
| `eslint-config-prettier`    | Disable style rules that conflict with Prettier |
| `eslint-plugin-prettier`    | Run Prettier as an ESLint rule                  |

---

## Prettier Integration

```bash
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
```

```js
// eslint.config.js
import prettier from "eslint-config-prettier";
import prettierPlugin from "eslint-plugin-prettier/recommended";

export default [prettierPlugin, prettier];
```

---

## package.json Scripts

```json
{
	"scripts": {
		"lint": "eslint src/",
		"lint:fix": "eslint src/ --fix",
		"lint:ci": "eslint src/ --max-warnings 0"
	}
}
```

---

## VS Code Integration

Install the **ESLint** extension (`dbaeumer.vscode-eslint`), then add to `settings.json`:

```json
{
	"editor.codeActionsOnSave": {
		"source.fixAll.eslint": "explicit"
	},
	"eslint.validate": ["javascript", "typescript", "jsx", "tsx"]
}
```

---

## Debugging

```bash
# See what config applies to a file
npx eslint --print-config src/index.ts

# Run with debug output
DEBUG=eslint:* npx eslint src/

# List all loaded rules
npx eslint --print-config src/index.js | grep '"rules"' -A 9999
```

---

## Version History Highlights

| Version | Key Change                                                          |
| ------- | ------------------------------------------------------------------- |
| v6      | Sharable configs                                                    |
| v8      | Stable flat config preview                                          |
| v9      | Flat config (`eslint.config.js`) is default, `.eslintrc` deprecated |

---

## Quick Reference

```bash
npx eslint .                  # Lint everything
npx eslint . --fix            # Auto-fix
npx eslint . --quiet          # Errors only
npx eslint . --cache          # Cache for speed
npx eslint --init             # Setup wizard
npx eslint --print-config .   # Debug config
```

---

---

# Other Types of Linters

Linting is not limited to JavaScript. Every language and file format has dedicated tools.

---

## JavaScript / TypeScript Alternatives

| Tool           | Description                                                                 | Install                   |
| -------------- | --------------------------------------------------------------------------- | ------------------------- |
| **Biome**      | All-in-one linter + formatter (replaces ESLint + Prettier), written in Rust | `npm i -D @biomejs/biome` |
| **oxlint**     | Extremely fast ESLint-compatible linter in Rust                             | `npm i -D oxlint`         |
| **JSHint**     | Older, config-driven JS linter                                              | `npm i -D jshint`         |
| **StandardJS** | Opinionated JS style with zero config                                       | `npm i -D standard`       |
| **deno lint**  | Built-in linter for Deno projects                                           | `deno lint`               |

```bash
# Biome
npx @biomejs/biome lint src/
npx @biomejs/biome check --apply src/   # lint + format + fix

# oxlint
npx oxlint src/

# Standard
npx standard src/
npx standard --fix src/
```

---

## CSS / Styles

### Stylelint

```bash
npm install --save-dev stylelint stylelint-config-standard

# .stylelintrc.json
{
  "extends": ["stylelint-config-standard"],
  "rules": {
    "color-no-invalid-hex": true,
    "unit-no-unknown": true,
    "property-no-unknown": true,
    "selector-class-pattern": "^[a-z][a-z0-9-]*$",
    "max-nesting-depth": 3,
    "no-duplicate-selectors": true
  }
}
```

```bash
npx stylelint "**/*.css"
npx stylelint "**/*.scss" --fix
npx stylelint "**/*.{css,scss,less}"
```

---

## Python

| Tool       | Role                                                             | Install              |
| ---------- | ---------------------------------------------------------------- | -------------------- |
| **Ruff**   | Fast all-in-one linter + formatter (replaces flake8/isort/black) | `pip install ruff`   |
| **Pylint** | Deep static analysis, style + logic                              | `pip install pylint` |
| **Flake8** | Style + syntax checker (PEP 8)                                   | `pip install flake8` |
| **mypy**   | Static type checker                                              | `pip install mypy`   |
| **Bandit** | Security vulnerability scanner                                   | `pip install bandit` |
| **Black**  | Opinionated code formatter                                       | `pip install black`  |

```bash
# Ruff (fastest, recommended)
ruff check src/
ruff check src/ --fix
ruff format src/

# Pylint
pylint src/mymodule.py

# Flake8
flake8 src/ --max-line-length=100

# mypy
mypy src/ --strict

# Bandit
bandit -r src/
```

```toml
# pyproject.toml — Ruff config
[tool.ruff]
line-length = 100
select = ["E", "F", "W", "I", "N", "UP", "S", "B"]
ignore = ["E501"]

[tool.ruff.lint]
extend-select = ["C90"]  # complexity
```

---

## Go

```bash
# Built-in
go vet ./...

# golangci-lint (runs many linters at once — recommended)
brew install golangci-lint
golangci-lint run ./...
golangci-lint run --fix ./...

# staticcheck
go install honnef.co/go/tools/cmd/staticcheck@latest
staticcheck ./...
```

```yaml
# .golangci.yml
linters:
  enable:
    - errcheck
    - gosimple
    - govet
    - ineffassign
    - staticcheck
    - unused
    - gofmt
    - goimports
    - revive
    - gosec
```

---

## Rust

```bash
# Clippy (official Rust linter, ships with rustup)
cargo clippy
cargo clippy -- -D warnings      # treat warnings as errors
cargo clippy --fix               # auto-fix
cargo fmt                        # formatter
cargo fmt -- --check             # CI check (no changes)
```

---

## Shell Scripts

### ShellCheck

```bash
# Install
brew install shellcheck           # macOS
apt install shellcheck            # Ubuntu

# Run
shellcheck script.sh
shellcheck **/*.sh

# Inline disable
# shellcheck disable=SC2086
echo $var
```

Common ShellCheck codes:

| Code   | Issue                                   |
| ------ | --------------------------------------- | --- | ----- |
| SC2086 | Unquoted variable (word splitting risk) |
| SC2046 | Unquoted command substitution           |
| SC2006 | Use `$()` instead of backticks          |
| SC2164 | Use `cd ...                             |     | exit` |

---

## Markdown

```bash
npm install --save-dev markdownlint-cli

# .markdownlint.json
{
  "MD013": { "line_length": 120 },
  "MD033": false,
  "MD041": false
}

npx markdownlint "**/*.md"
npx markdownlint "**/*.md" --fix
```

---

## YAML / JSON / TOML

```bash
# YAML
pip install yamllint
yamllint .
# .yamllint.yml
# extends: default
# rules:
#   line-length: { max: 120 }

# JSON — built into Node
node -e "JSON.parse(require('fs').readFileSync('file.json','utf8'))"

# jsonlint
npm install -g jsonlint
jsonlint file.json

# TOML
pip install toml-sort
toml-sort pyproject.toml --check
```

---

## HTML

```bash
npm install --save-dev htmlhint

# .htmlhintrc
{
  "tagname-lowercase": true,
  "attr-lowercase": true,
  "attr-value-double-quotes": true,
  "doctype-first": true,
  "id-unique": true,
  "src-not-empty": true,
  "alt-require": true
}

npx htmlhint "**/*.html"
```

---

## Docker

```bash
# Hadolint — Dockerfile linter
brew install hadolint
hadolint Dockerfile
docker run --rm -i hadolint/hadolint < Dockerfile

# Inline ignore
# hadolint ignore=DL3008
RUN apt-get install -y curl
```

Common Hadolint rules:

| Rule   | Issue                            |
| ------ | -------------------------------- |
| DL3007 | Use specific tag, not `latest`   |
| DL3008 | Pin apt package versions         |
| DL3009 | Delete apt lists after install   |
| DL4006 | Set `SHELL` option with pipefail |

---

## Infrastructure as Code

```bash
# Terraform
brew install tflint
tflint --init
tflint

# tfsec — security scanner for Terraform
brew install tfsec
tfsec .

# CloudFormation
pip install cfn-lint
cfn-lint template.yaml

# Kubernetes manifests
kubectl apply --dry-run=client -f manifest.yaml
kube-linter lint manifest.yaml          # deeper checks
```

---

## SQL

```bash
pip install sqlfluff

# .sqlfluff
# [sqlfluff]
# dialect = postgres
# templater = dbt

sqlfluff lint query.sql
sqlfluff fix query.sql
sqlfluff lint --dialect postgres query.sql
```

---

## Security-Focused Scanners

| Tool          | Language / Target          | Install                                                     |
| ------------- | -------------------------- | ----------------------------------------------------------- |
| **Semgrep**   | Any language, custom rules | `pip install semgrep`                                       |
| **Bandit**    | Python                     | `pip install bandit`                                        |
| **Brakeman**  | Ruby on Rails              | `gem install brakeman`                                      |
| **gosec**     | Go                         | `go install github.com/securecgo/gosec/v2/cmd/gosec@latest` |
| **npm audit** | Node.js deps               | built-in                                                    |
| **Snyk**      | Deps + code                | `npm i -g snyk`                                             |

```bash
semgrep --config=auto src/
semgrep --config=p/owasp-top-ten src/

npm audit
npm audit fix

snyk test
snyk code test
```

---

## Commit Message Linting

```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional

# commitlint.config.js
export default {
  extends: ["@commitlint/config-conventional"],
  rules: {
    "type-enum": [2, "always", ["feat","fix","docs","style","refactor","test","chore"]],
    "subject-max-length": [2, "always", 72],
  },
};

# With Husky
npx husky add .husky/commit-msg "npx commitlint --edit $1"
```

---

## Git Hooks (run linters automatically)

```bash
npm install --save-dev husky lint-staged

# package.json
{
  "lint-staged": {
    "*.{js,ts,jsx,tsx}": ["eslint --fix", "prettier --write"],
    "*.{css,scss}": ["stylelint --fix"],
    "*.py": ["ruff check --fix", "ruff format"],
    "*.sh": ["shellcheck"],
    "*.md": ["markdownlint --fix"]
  }
}

npx husky init
echo "npx lint-staged" > .husky/pre-commit
```

---

## Linter Comparison by Language

| Language   | Recommended                 | Also popular        |
| ---------- | --------------------------- | ------------------- |
| JavaScript | ESLint / Biome              | oxlint, StandardJS  |
| TypeScript | ESLint + @typescript-eslint | Biome               |
| CSS/SCSS   | Stylelint                   | —                   |
| Python     | Ruff                        | Pylint, Flake8      |
| Go         | golangci-lint               | staticcheck, go vet |
| Rust       | Clippy                      | —                   |
| Shell      | ShellCheck                  | —                   |
| Markdown   | markdownlint                | —                   |
| YAML       | yamllint                    | —                   |
| Dockerfile | Hadolint                    | —                   |
| Terraform  | tflint + tfsec              | —                   |
| SQL        | SQLFluff                    | —                   |
| HTML       | HTMLHint                    | —                   |
