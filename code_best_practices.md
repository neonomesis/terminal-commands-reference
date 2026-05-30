# Code Best Practices Reference

## Table of Contents
- [General Principles](#general-principles)
- [Naming Conventions](#naming-conventions)
- [Functions & Methods](#functions--methods)
- [Comments & Documentation](#comments--documentation)
- [Error Handling](#error-handling)
- [Code Structure & Organization](#code-structure--organization)
- [Filesystem Best Practices](#filesystem-best-practices)
- [Security](#security)
- [Performance](#performance)
- [Testing](#testing)
- [Version Control](#version-control)
- [Language-Specific](#language-specific)

---

## General Principles

### SOLID Principles
```
S - Single Responsibility   Each class/function does ONE thing
O - Open/Closed             Open for extension, closed for modification
L - Liskov Substitution     Subtypes must be replaceable for base types
I - Interface Segregation   Small specific interfaces over large general ones
D - Dependency Inversion    Depend on abstractions, not concrete implementations
```

### DRY, KISS, YAGNI
```
DRY  - Don't Repeat Yourself       Extract repeated logic into reusable units
KISS - Keep It Simple, Stupid      Prefer simple solutions over clever ones
YAGNI - You Ain't Gonna Need It    Don't build features for hypothetical future needs
```

---

## Naming Conventions

### Variables & Constants
```js
// Bad
const d = new Date();
const arr = [1, 2, 3];
const MAGIC = 86400;

// Good
const currentDate = new Date();
const userIds = [1, 2, 3];
const SECONDS_PER_DAY = 86400;
```

### Functions
```js
// Bad
function data() {}
function doStuff(x) {}

// Good
function fetchUserData() {}
function calculateTax(income) {}
```

### Boolean Naming
```js
// Bad
let active = true;
let check = false;

// Good
let isActive = true;
let hasPermission = false;
let canEdit = true;
```

### Language Conventions
```
JavaScript/TypeScript  camelCase vars, PascalCase classes, UPPER_SNAKE_CASE constants
Python                 snake_case vars/functions, PascalCase classes, UPPER_SNAKE_CASE constants
Go                     camelCase private, PascalCase exported
Java/C#                camelCase vars, PascalCase classes/methods
CSS                    kebab-case classes, BEM methodology
```

---

## Functions & Methods

### Single Responsibility
```js
// Bad — does too many things
function processUser(user) {
  validateEmail(user.email);
  saveToDatabase(user);
  sendWelcomeEmail(user);
  logActivity(user);
}

// Good — each function has one job
function registerUser(user) {
  validateUser(user);
  const saved = saveUser(user);
  notifyUser(saved);
  return saved;
}
```

### Argument Count
```js
// Bad — too many parameters
function createUser(name, email, age, role, isActive, country) {}

// Good — use an object for 3+ params
function createUser({ name, email, age, role, isActive, country }) {}
```

### Return Early (Guard Clauses)
```js
// Bad — deeply nested
function processOrder(order) {
  if (order) {
    if (order.items.length > 0) {
      if (order.isPaid) {
        // process...
      }
    }
  }
}

// Good — return early
function processOrder(order) {
  if (!order) return;
  if (order.items.length === 0) return;
  if (!order.isPaid) return;
  // process...
}
```

### Pure Functions
```js
// Impure — depends on external state
let tax = 0.2;
function getTotal(price) {
  return price + price * tax;
}

// Pure — same input always gives same output
function getTotal(price, taxRate) {
  return price + price * taxRate;
}
```

---

## Comments & Documentation

### When to Comment
```js
// Bad — comment explains WHAT (already obvious)
// increment i by 1
i++;

// Good — comment explains WHY (non-obvious reason)
// Offset by 1 because the API uses 1-based pagination
const page = requestedPage + 1;
```

### JSDoc / Docstrings
```js
/**
 * Calculates compound interest.
 * @param {number} principal - Initial amount
 * @param {number} rate - Annual interest rate (0.05 = 5%)
 * @param {number} years - Number of years
 * @returns {number} Final amount after compound interest
 */
function compoundInterest(principal, rate, years) {
  return principal * Math.pow(1 + rate, years);
}
```

```python
def compound_interest(principal: float, rate: float, years: int) -> float:
    """
    Calculate compound interest.

    Args:
        principal: Initial amount
        rate: Annual interest rate (0.05 = 5%)
        years: Number of years

    Returns:
        Final amount after compound interest
    """
    return principal * (1 + rate) ** years
```

### README Essentials
```markdown
# Project Name
Brief description of what it does.

## Installation
## Usage
## Configuration
## Contributing
## License
```

---

## Error Handling

### Never Swallow Errors
```js
// Bad
try {
  doSomething();
} catch (e) {}

// Good
try {
  doSomething();
} catch (error) {
  logger.error('doSomething failed:', error);
  throw error; // or handle gracefully
}
```

### Specific Error Types
```js
// Bad
throw new Error('Something went wrong');

// Good
class ValidationError extends Error {
  constructor(field, message) {
    super(message);
    this.name = 'ValidationError';
    this.field = field;
  }
}

throw new ValidationError('email', 'Invalid email format');
```

### Async Error Handling
```js
// Bad
async function fetchData() {
  const data = await api.get('/users'); // unhandled rejection
  return data;
}

// Good
async function fetchData() {
  try {
    const data = await api.get('/users');
    return data;
  } catch (error) {
    logger.error('Failed to fetch users:', error);
    throw new ServiceError('User fetch failed', { cause: error });
  }
}
```

### Fail Fast
```js
function divide(a, b) {
  if (b === 0) throw new Error('Division by zero');
  return a / b;
}
```

---

## Code Structure & Organization

### File Organization
```
src/
├── components/       UI components
├── services/         Business logic / API calls
├── utils/            Pure utility functions
├── models/           Data models / types
├── hooks/            React hooks (if applicable)
├── constants/        App-wide constants
└── index.js          Entry point
```

### Module Exports
```js
// Bad — export everything as default
export default { fetchUser, saveUser, deleteUser };

// Good — named exports for tree-shaking
export function fetchUser(id) {}
export function saveUser(user) {}
export function deleteUser(id) {}
```

### Magic Numbers & Strings
```js
// Bad
if (status === 3) { ... }
setTimeout(fn, 86400000);

// Good
const STATUS = { PENDING: 1, ACTIVE: 2, BANNED: 3 };
const ONE_DAY_MS = 24 * 60 * 60 * 1000;

if (status === STATUS.BANNED) { ... }
setTimeout(fn, ONE_DAY_MS);
```

### Max Line Length
```
Recommended: 80–120 characters per line
Configure in .editorconfig, .prettierrc, or eslint
```

---

## Filesystem Best Practices

### Directory & File Naming
```
Use lowercase with hyphens for directories and files
  good:  user-profile/avatar-upload.js
  bad:   UserProfile/AvatarUpload.js

Exception: language convention takes precedence
  Python modules:   snake_case.py
  React components: PascalCase.tsx
  Go files:         snake_case.go
```

### Project Root — Keep It Clean
```
/project-root
├── src/              All source code
├── tests/            All tests (mirrors src/ structure)
├── docs/             Documentation
├── scripts/          Build / automation scripts
├── public/           Static assets served directly
├── .github/          CI/CD workflows, issue templates
├── .env.example      Template for env vars (no real values)
├── .gitignore
├── README.md
└── package.json / pyproject.toml / go.mod
```

### Paths — Absolute vs Relative
```js
// Bad — breaks when file moves
const config = require('../../../config');

// Good — use path aliases or a root-relative helper
import config from '@/config';          // alias in tsconfig/webpack
const config = require(path.join(__dirname, 'config'));
```

```python
# Good — use pathlib, not string concatenation
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent
CONFIG_PATH = BASE_DIR / 'config' / 'settings.json'
```

### File Reads & Writes
```js
// Always handle file errors explicitly
import fs from 'fs/promises';

async function readConfig(filePath) {
  try {
    const content = await fs.readFile(filePath, 'utf-8');
    return JSON.parse(content);
  } catch (error) {
    if (error.code === 'ENOENT') throw new Error(`Config not found: ${filePath}`);
    throw error;
  }
}
```

```python
from pathlib import Path

def read_config(path: Path) -> dict:
    if not path.exists():
        raise FileNotFoundError(f"Config not found: {path}")
    return json.loads(path.read_text(encoding='utf-8'))
```

### Atomic Writes (Avoid Corrupt Files)
```js
// Bad — crash mid-write leaves corrupt file
fs.writeFileSync(targetPath, data);

// Good — write to temp, then rename (atomic on most OS)
const tmp = targetPath + '.tmp';
fs.writeFileSync(tmp, data);
fs.renameSync(tmp, targetPath);
```

### Temp Files & Cleanup
```python
import tempfile

# Good — temp file cleaned up automatically
with tempfile.NamedTemporaryFile(suffix='.json', delete=True) as tmp:
    tmp.write(data.encode())
    process(tmp.name)
```

```js
// Always clean up temp files in a finally block
const tmp = os.tmpdir() + '/upload-' + Date.now();
try {
  await processFile(tmp);
} finally {
  await fs.unlink(tmp).catch(() => {});
}
```

### File Upload Security
```js
// Validate file type by content (magic bytes), not just extension
import { fileTypeFromBuffer } from 'file-type';

const type = await fileTypeFromBuffer(buffer);
const ALLOWED = ['image/jpeg', 'image/png', 'image/webp'];

if (!type || !ALLOWED.includes(type.mime)) {
  throw new ValidationError('file', 'Unsupported file type');
}

// Sanitize filenames — never trust user-supplied names
import { basename } from 'path';
const safe = basename(userFilename).replace(/[^a-zA-Z0-9._-]/g, '_');
```

### Path Traversal Prevention
```js
// Bad — attacker can send ../../etc/passwd
const filePath = path.join(uploadDir, req.query.file);

// Good — resolve and verify it's inside the allowed dir
const filePath = path.resolve(uploadDir, req.query.file);
if (!filePath.startsWith(path.resolve(uploadDir))) {
  throw new Error('Path traversal detected');
}
```

### Environment-Specific Paths
```js
// Bad — hardcoded OS-specific path
const logDir = '/var/log/myapp';

// Good — configurable via env
const logDir = process.env.LOG_DIR ?? path.join(os.homedir(), '.myapp', 'logs');
```

```python
import os
from pathlib import Path

LOG_DIR = Path(os.getenv('LOG_DIR', Path.home() / '.myapp' / 'logs'))
LOG_DIR.mkdir(parents=True, exist_ok=True)
```

### File Size & Limits
```js
// Always enforce upload/read size limits
const MAX_FILE_SIZE = 10 * 1024 * 1024; // 10 MB

if (file.size > MAX_FILE_SIZE) {
  throw new ValidationError('file', 'File exceeds 10 MB limit');
}

// Stream large files instead of loading into memory
import { createReadStream } from 'fs';
const stream = createReadStream(largePath, { highWaterMark: 64 * 1024 });
```

### Cross-Platform Compatibility
```js
// Bad — Unix-only path separator
const filePath = dir + '/' + filename;

// Good — works on Windows too
const filePath = path.join(dir, filename);

// Bad — Unix line endings assumed
const lines = content.split('\n');

// Good — handles \r\n (Windows) and \n (Unix)
const lines = content.split(/\r?\n/);
```

### Permissions & Ownership
```bash
# Least-privilege file permissions
chmod 600 .env                  # owner read/write only
chmod 644 config.json           # owner write, others read
chmod 755 scripts/deploy.sh     # executable by all, writable by owner only
chmod 700 ~/.ssh                # SSH dir — owner only

# Never make secrets world-readable
chmod 777 .env                  # WRONG — anyone on system can read
```

### Logging File Operations
```js
// Log meaningful context, not just "file saved"
logger.info('Config written', {
  path: filePath,
  size: Buffer.byteLength(data),
  user: req.user.id,
});
```

---

## Security

### Input Validation
```js
// Always validate at system boundaries (user input, API responses)
function createUser(input) {
  if (!input.email || !isValidEmail(input.email)) {
    throw new ValidationError('email', 'Invalid email');
  }
  if (!input.password || input.password.length < 8) {
    throw new ValidationError('password', 'Password too short');
  }
}
```

### Never Trust User Input
```js
// SQL Injection — Bad
const query = `SELECT * FROM users WHERE id = ${userId}`;

// Good — parameterized queries
const query = 'SELECT * FROM users WHERE id = ?';
db.execute(query, [userId]);
```

### Secrets Management
```bash
# Bad — hardcoded secrets
API_KEY = "sk-abc123xyz"

# Good — environment variables
API_KEY = process.env.API_KEY
```

```
Never commit to git:
  .env files
  API keys / tokens
  Passwords / credentials
  Private keys / certificates
```

### Dependency Security
```bash
npm audit                    # Check for vulnerabilities
npm audit fix                # Auto-fix where possible
pip install safety && safety check
```

### XSS Prevention
```js
// Bad — raw HTML injection
element.innerHTML = userInput;

// Good — safe text insertion
element.textContent = userInput;
// Or sanitize with a library: DOMPurify
element.innerHTML = DOMPurify.sanitize(userInput);
```

---

## Performance

### Avoid Premature Optimization
```
1. Make it work
2. Make it right (correct + tested)
3. Make it fast (only if needed, profile first)
```

### Memoization
```js
// Cache expensive computations
const memoize = (fn) => {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
};

const expensiveCalc = memoize((n) => { /* ... */ });
```

### Lazy Loading
```js
// Load only when needed
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));
```

### Database
```sql
-- Index frequently queried columns
CREATE INDEX idx_users_email ON users(email);

-- Avoid SELECT *
SELECT id, name, email FROM users WHERE active = true;

-- Use LIMIT
SELECT * FROM logs ORDER BY created_at DESC LIMIT 100;
```

---

## Testing

### Test Pyramid
```
        /\
       /E2E\         Few — slow, expensive, test full flows
      /------\
     /Integr. \      Some — test module interactions
    /----------\
   /  Unit Tests \   Many — fast, isolated, test single units
  /--------------\
```

### Naming Tests
```js
// Pattern: describe WHAT and WHEN
describe('calculateTax', () => {
  it('returns 0 when income is below threshold', () => { ... });
  it('applies 20% rate for standard income', () => { ... });
  it('throws ValidationError for negative income', () => { ... });
});
```

### Arrange-Act-Assert (AAA)
```js
it('applies discount to order total', () => {
  // Arrange
  const order = { total: 100, discountCode: 'SAVE10' };

  // Act
  const result = applyDiscount(order);

  // Assert
  expect(result.total).toBe(90);
});
```

### Test Coverage
```
Aim for: 70–80% coverage on business logic
Avoid:   Testing implementation details (test behavior, not internals)
```

```bash
jest --coverage
pytest --cov=src
go test -cover ./...
```

---

## Version Control

### Commit Messages
```
Format: <type>(<scope>): <short description>

Types:
  feat      New feature
  fix       Bug fix
  docs      Documentation only
  style     Formatting, no logic change
  refactor  Code restructure, no feature/fix
  test      Adding tests
  chore     Build process, deps, tooling

Examples:
  feat(auth): add OAuth2 login with Google
  fix(cart): correct tax calculation for EU users
  docs(api): update endpoint parameters for v2
  refactor(users): extract email validation to utility
```

### Branch Strategy
```
main / master     Production-ready code
develop           Integration branch
feature/*         New features
fix/*             Bug fixes
release/*         Release preparation
hotfix/*          Critical production fixes
```

### .gitignore Essentials
```gitignore
# Dependencies
node_modules/
vendor/
__pycache__/
*.pyc

# Build output
dist/
build/
*.egg-info/

# Environment & secrets
.env
.env.local
*.pem
*.key

# Editor
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db
```

---

## Language-Specific

### JavaScript / TypeScript
```ts
// Prefer const over let, avoid var
const MAX_RETRIES = 3;
let retryCount = 0;

// Use TypeScript strict mode
// tsconfig.json
{ "compilerOptions": { "strict": true } }

// Optional chaining & nullish coalescing
const name = user?.profile?.name ?? 'Anonymous';

// Destructuring
const { id, email } = user;
const [first, ...rest] = items;

// Async/await over .then chains
const data = await fetchData();
```

### Python
```python
# Use type hints
def greet(name: str) -> str:
    return f"Hello, {name}"

# Context managers for resources
with open('file.txt') as f:
    content = f.read()

# List comprehensions over loops (when readable)
squares = [x ** 2 for x in range(10)]

# f-strings over .format()
message = f"Hello, {user.name}!"

# Use dataclasses for data containers
from dataclasses import dataclass

@dataclass
class User:
    name: str
    email: str
    age: int
```

### Go
```go
// Handle errors explicitly
result, err := doSomething()
if err != nil {
    return fmt.Errorf("doSomething failed: %w", err)
}

// Use defer for cleanup
func readFile(path string) error {
    f, err := os.Open(path)
    if err != nil { return err }
    defer f.Close()
    // ...
}

// Prefer interfaces for flexibility
type Writer interface {
    Write(data []byte) error
}
```

---

## Quick Checklist

### Before Committing
```
[ ] Code does what it's supposed to do
[ ] No hardcoded secrets or credentials
[ ] No debug logs / console.log left in
[ ] Edge cases handled
[ ] Tests written and passing
[ ] No TODO left unresolved
[ ] Dependencies updated in lock file
[ ] Lint/format passes
```

### Code Review Checklist
```
[ ] Is the logic correct?
[ ] Is it readable without explanation?
[ ] Are edge cases covered?
[ ] Is there proper error handling?
[ ] Any security concerns?
[ ] Any performance red flags?
[ ] Is it tested?
[ ] Does it follow project conventions?
```

---

*Reference guide — not exhaustive. Adapt to your team's conventions.*
