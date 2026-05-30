# Code Best Practices Reference

## Table of Contents
- [General Principles](#general-principles)
- [Naming Conventions](#naming-conventions)
- [Functions & Methods](#functions--methods)
- [Comments & Documentation](#comments--documentation)
- [Error Handling](#error-handling)
- [Code Structure & Organization](#code-structure--organization)
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
