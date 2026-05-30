# Testing Reference Guide

A practical reference for writing and running tests across popular languages and frameworks.

---

## Table of Contents

- [JavaScript / TypeScript](#javascript--typescript)
  - [Jest](#jest)
  - [Vitest](#vitest)
  - [Mocha](#mocha)
  - [Playwright (E2E)](#playwright-e2e)
  - [Cypress (E2E)](#cypress-e2e)
- [Python](#python)
  - [pytest](#pytest)
  - [unittest](#unittest)
- [Go](#go)
- [Rust](#rust)
- [General Concepts](#general-concepts)

---

## JavaScript / TypeScript

### Jest

#### Install
```bash
npm install --save-dev jest
# TypeScript support
npm install --save-dev ts-jest @types/jest
```

#### Config (`jest.config.js`)
```js
module.exports = {
  preset: 'ts-jest',        // remove if not using TypeScript
  testEnvironment: 'node',  // or 'jsdom' for browser-like env
  coverageDirectory: 'coverage',
  collectCoverageFrom: ['src/**/*.{ts,js}'],
};
```

#### Writing Tests
```js
// math.test.js
const { add } = require('./math');

describe('add()', () => {
  it('returns the sum of two numbers', () => {
    expect(add(2, 3)).toBe(5);
  });

  it('handles negative numbers', () => {
    expect(add(-1, 1)).toBe(0);
  });
});
```

#### Running Tests
```bash
npx jest                        # run all tests
npx jest --watch                # watch mode
npx jest --coverage             # with coverage report
npx jest path/to/file.test.js   # single file
npx jest -t "test name"         # run tests matching name
npx jest --verbose              # detailed output
npx jest --bail                 # stop after first failure
npx jest --runInBand            # run serially (no parallelism)
```

#### Matchers Cheat Sheet
```js
expect(value).toBe(x)              // strict equality (===)
expect(value).toEqual(x)           // deep equality
expect(value).toBeTruthy()
expect(value).toBeFalsy()
expect(value).toBeNull()
expect(value).toBeUndefined()
expect(value).toContain(item)      // array or string
expect(value).toHaveLength(n)
expect(fn).toThrow()               // function throws
expect(fn).toThrow('message')
expect(value).toBeGreaterThan(n)
expect(value).toBeLessThan(n)
expect(mock).toHaveBeenCalled()
expect(mock).toHaveBeenCalledWith(args)
expect(mock).toHaveBeenCalledTimes(n)
```

#### Mocking
```js
// Mock a module
jest.mock('./api');

// Mock a function
const mockFn = jest.fn().mockReturnValue(42);
const mockAsync = jest.fn().mockResolvedValue({ data: 'ok' });

// Spy on an existing method
const spy = jest.spyOn(object, 'method');

// Clear mocks between tests
afterEach(() => jest.clearAllMocks());
```

#### Async Tests
```js
// async/await
it('fetches data', async () => {
  const data = await fetchData();
  expect(data).toEqual({ id: 1 });
});

// Promise
it('resolves correctly', () => {
  return fetchData().then(data => {
    expect(data).toEqual({ id: 1 });
  });
});
```

#### Lifecycle Hooks
```js
beforeAll(() => { /* runs once before all tests in block */ });
afterAll(() => { /* runs once after all tests in block */ });
beforeEach(() => { /* runs before each test */ });
afterEach(() => { /* runs after each test */ });
```

---

### Vitest

> Drop-in Jest replacement for Vite projects. Faster, ESM-native.

#### Install
```bash
npm install --save-dev vitest
```

#### Config (`vite.config.ts` or `vitest.config.ts`)
```ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    environment: 'node', // or 'jsdom', 'happy-dom'
    coverage: {
      reporter: ['text', 'html'],
    },
  },
});
```

#### Writing Tests
```ts
import { describe, it, expect, vi } from 'vitest';
import { add } from './math';

describe('add()', () => {
  it('returns the sum', () => {
    expect(add(2, 3)).toBe(5);
  });
});
```

#### Running Tests
```bash
npx vitest              # watch mode by default
npx vitest run          # single run (CI mode)
npx vitest --coverage   # with coverage
npx vitest run src/math # filter by path
npx vitest -t "add"     # filter by test name
npx vitest ui           # browser UI
```

#### Mocking (Vitest)
```ts
import { vi } from 'vitest';

vi.mock('./api');                          // auto-mock module
const mockFn = vi.fn().mockReturnValue(1);
vi.spyOn(object, 'method');
vi.useFakeTimers();                        // fake timers
vi.useRealTimers();
```

---

### Mocha

#### Install
```bash
npm install --save-dev mocha chai
```

#### Writing Tests
```js
const { expect } = require('chai');
const { add } = require('./math');

describe('add()', () => {
  it('returns the sum', () => {
    expect(add(2, 3)).to.equal(5);
  });
});
```

#### Running Tests
```bash
npx mocha                        # looks for test/ folder
npx mocha 'src/**/*.test.js'     # glob pattern
npx mocha --watch                # watch mode
npx mocha --grep "test name"     # filter tests
npx mocha --timeout 5000         # set timeout (ms)
npx mocha --reporter spec        # output format
```

---

### Playwright (E2E)

#### Install
```bash
npm init playwright@latest
# or manually:
npm install --save-dev @playwright/test
npx playwright install            # download browsers
```

#### Writing Tests
```ts
// tests/home.spec.ts
import { test, expect } from '@playwright/test';

test('homepage has title', async ({ page }) => {
  await page.goto('http://localhost:3000');
  await expect(page).toHaveTitle(/My App/);
});

test('button click', async ({ page }) => {
  await page.goto('/');
  await page.getByRole('button', { name: 'Submit' }).click();
  await expect(page.getByText('Success')).toBeVisible();
});
```

#### Running Tests
```bash
npx playwright test                     # run all tests
npx playwright test --headed            # show browser window
npx playwright test tests/home.spec.ts  # single file
npx playwright test --grep "title"      # filter by name
npx playwright test --project=chromium  # specific browser
npx playwright test --debug             # debug mode
npx playwright show-report              # open HTML report
npx playwright codegen http://localhost # record test by clicking
```

#### Config (`playwright.config.ts`)
```ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  use: {
    baseURL: 'http://localhost:3000',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },
  projects: [
    { name: 'chromium', use: { browserName: 'chromium' } },
    { name: 'firefox',  use: { browserName: 'firefox' } },
    { name: 'webkit',   use: { browserName: 'webkit' } },
  ],
});
```

---

### Cypress (E2E)

#### Install
```bash
npm install --save-dev cypress
npx cypress open    # first-time setup wizard
```

#### Writing Tests
```js
// cypress/e2e/home.cy.js
describe('Homepage', () => {
  it('displays the title', () => {
    cy.visit('/');
    cy.get('h1').should('contain', 'Welcome');
  });

  it('submits the form', () => {
    cy.visit('/contact');
    cy.get('[data-cy=email]').type('test@example.com');
    cy.get('[data-cy=submit]').click();
    cy.contains('Thank you').should('be.visible');
  });
});
```

#### Running Tests
```bash
npx cypress open                    # interactive GUI
npx cypress run                     # headless (CI)
npx cypress run --spec "path/*.cy.js"  # specific file
npx cypress run --browser chrome    # specific browser
npx cypress run --headed            # headed mode in CI
```

---

## Python

### pytest

#### Install
```bash
pip install pytest pytest-cov
```

#### Writing Tests
```python
# test_math.py
from math_utils import add

def test_add_positive_numbers():
    assert add(2, 3) == 5

def test_add_negative():
    assert add(-1, 1) == 0

class TestAdd:
    def test_with_zero(self):
        assert add(0, 5) == 5

    def test_returns_int(self):
        assert isinstance(add(1, 2), int)
```

#### Running Tests
```bash
pytest                          # run all tests
pytest test_math.py             # single file
pytest test_math.py::test_add   # single test
pytest -v                       # verbose output
pytest -k "add"                 # filter by name pattern
pytest --tb=short               # shorter tracebacks
pytest --cov=src                # coverage for src/
pytest --cov=src --cov-report=html  # HTML coverage report
pytest -x                       # stop on first failure
pytest -n 4                     # run in parallel (needs pytest-xdist)
pytest --lf                     # re-run only last failures
pytest -s                       # show print() output
```

#### Fixtures
```python
import pytest

@pytest.fixture
def db_connection():
    conn = create_connection()
    yield conn         # test runs here
    conn.close()       # teardown

def test_query(db_connection):
    result = db_connection.execute("SELECT 1")
    assert result is not None

# Scoped fixtures
@pytest.fixture(scope="module")   # once per module
@pytest.fixture(scope="session")  # once per test session
```

#### Parametrize
```python
@pytest.mark.parametrize("a,b,expected", [
    (1, 2, 3),
    (0, 0, 0),
    (-1, 1, 0),
])
def test_add(a, b, expected):
    assert add(a, b) == expected
```

#### Marks & Skip
```python
@pytest.mark.skip(reason="not implemented yet")
def test_future():
    pass

@pytest.mark.skipif(sys.platform == "win32", reason="unix only")
def test_unix():
    pass

@pytest.mark.xfail
def test_known_bug():
    assert buggy_function() == 1

# Custom marks — register in pytest.ini:
# [pytest]
# markers = slow: mark test as slow
@pytest.mark.slow
def test_heavy():
    pass
```

#### Config (`pytest.ini` or `pyproject.toml`)
```ini
# pytest.ini
[pytest]
testpaths = tests
addopts = -v --tb=short
```
```toml
# pyproject.toml
[tool.pytest.ini_options]
testpaths = ["tests"]
addopts = "-v --tb=short"
```

---

### unittest

#### Writing Tests
```python
import unittest
from math_utils import add

class TestAdd(unittest.TestCase):

    def setUp(self):
        # runs before each test
        pass

    def tearDown(self):
        # runs after each test
        pass

    def test_positive(self):
        self.assertEqual(add(2, 3), 5)

    def test_negative(self):
        self.assertNotEqual(add(1, 1), 3)

    def test_raises(self):
        with self.assertRaises(ValueError):
            add("a", 1)

if __name__ == '__main__':
    unittest.main()
```

#### Running Tests
```bash
python -m unittest                       # discover all tests
python -m unittest test_math             # single module
python -m unittest test_math.TestAdd     # single class
python -m unittest test_math.TestAdd.test_positive  # single method
python -m unittest discover -s tests/    # discover in folder
python -m unittest -v                    # verbose
```

---

## Go

#### Writing Tests
```go
// math_test.go
package math

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Add(2, 3) = %d; want 5", result)
    }
}

// Table-driven tests (idiomatic Go)
func TestAddTable(t *testing.T) {
    cases := []struct {
        a, b, expected int
    }{
        {1, 2, 3},
        {0, 0, 0},
        {-1, 1, 0},
    }
    for _, c := range cases {
        got := Add(c.a, c.b)
        if got != c.expected {
            t.Errorf("Add(%d, %d) = %d; want %d", c.a, c.b, got, c.expected)
        }
    }
}

// Benchmark
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(1, 2)
    }
}
```

#### Running Tests
```bash
go test ./...                   # all packages recursively
go test .                       # current package
go test -v ./...                # verbose
go test -run TestAdd            # filter by name (regex)
go test -run TestAdd/table      # sub-test filter
go test -cover ./...            # with coverage
go test -coverprofile=cov.out ./... && go tool cover -html=cov.out
go test -bench=.                # run benchmarks
go test -race ./...             # detect race conditions
go test -count=1 ./...          # disable test caching
go test -timeout 30s ./...      # set timeout
```

---

## Rust

#### Writing Tests
```rust
// src/math.rs
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

#[cfg(test)]           // only compile in test mode
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
    }

    #[test]
    fn test_add_negative() {
        assert_eq!(add(-1, 1), 0);
    }

    #[test]
    #[should_panic]
    fn test_panics() {
        panic!("expected panic");
    }

    #[test]
    fn test_with_message() {
        assert_eq!(add(1, 1), 2, "1 + 1 should be 2");
    }
}
```

#### Integration Tests
```rust
// tests/integration_test.rs  (separate file, not inside src/)
use my_crate::add;

#[test]
fn test_add_integration() {
    assert_eq!(add(10, 20), 30);
}
```

#### Running Tests
```bash
cargo test                      # run all tests
cargo test test_add             # filter by name
cargo test -- --nocapture       # show println! output
cargo test -- --test-threads=1  # run serially
cargo test --lib                # only lib tests
cargo test --test integration_test  # only integration tests
cargo test --doc                # run doc tests
cargo bench                     # run benchmarks
```

---

## General Concepts

### Test Types

| Type          | Purpose                              | Speed    |
|---------------|--------------------------------------|----------|
| Unit          | Test a single function/class         | Fast     |
| Integration   | Test multiple components together    | Medium   |
| E2E / UI      | Test full user flows in browser      | Slow     |
| Snapshot      | Detect unintended UI changes         | Fast     |
| Performance   | Measure speed and resource usage     | Variable |

### Test Structure (AAA Pattern)

```
Arrange → Act → Assert
```

```js
it('adds two numbers', () => {
  // Arrange
  const a = 2, b = 3;

  // Act
  const result = add(a, b);

  // Assert
  expect(result).toBe(5);
});
```

### Naming Conventions

```
test_<what>_<condition>_<expected>
test_add_negative_numbers_returns_zero

// or BDD style:
describe('add') > it('returns 0 when both inputs are negative')
```

### Coverage Goals

| Coverage %  | Meaning                              |
|-------------|--------------------------------------|
| < 50%       | Likely undertested                   |
| 60–80%      | Acceptable for most projects         |
| 80–90%      | Good — aim for this                  |
| > 90%       | High confidence, diminishing returns |
| 100%        | Often impractical; can hide bad tests|

### CI Integration (GitHub Actions example)

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test -- --coverage
```

### Common Flags Summary

| Flag              | Jest       | pytest      | Go           |
|-------------------|------------|-------------|--------------|
| Verbose           | `--verbose`| `-v`        | `-v`         |
| Filter by name    | `-t`       | `-k`        | `-run`       |
| Coverage          | `--coverage`| `--cov`   | `-cover`     |
| Stop on failure   | `--bail`   | `-x`        | (default)    |
| Watch mode        | `--watch`  | `--watch` * | N/A          |
| Parallel          | (default)  | `-n 4` *    | (default)    |

\* requires extra package (`pytest-watch`, `pytest-xdist`)
