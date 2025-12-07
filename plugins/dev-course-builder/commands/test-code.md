---
description: Run tests for code in the course Docker sandbox
argument-hint: "[path] [options] - Test path and options (e.g., 'tests/' or 'test_module.py -v')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Skill]
---

# Test Code in Sandbox

Execute unit tests, integration tests, and test suites within the course's isolated Docker sandbox environment.

## Prerequisites

- Docker must be installed and running
- Course sandbox must be set up (use `/setup-sandbox` if not)
- Container must be running with testing frameworks installed

## Supported Testing Frameworks

| Language | Frameworks | Command |
|----------|------------|---------|
| C++ | Google Test, Catch2 | `ctest`, direct execution |
| Rust | cargo test | `cargo test` |
| Python | pytest, unittest | `pytest`, `python -m unittest` |
| Go | go test | `go test ./...` |
| JavaScript | Jest, Mocha | `npm test`, `jest` |

## Interactive Workflow

### Step 1: Identify Course and Container

```
Which course sandbox should run the tests?

[1] cpp-fundamentals (course-sandbox-cpp-fundamentals)
[2] rust-intro (course-sandbox-rust-intro)
[3] python-basics (course-sandbox-python-basics)
[4] Specify container name

Please select an option:
```

### Step 2: Select Test Scope

```
What tests should be run?

[1] All tests in the project
[2] Specific test file
[3] Specific test function/case
[4] Tests matching a pattern

Please select an option:
```

### Step 3: Test Options

```
Test execution options:

Verbosity: [1] Normal  [2] Verbose  [3] Quiet
Stop on failure: [1] Continue all  [2] Stop on first failure
Coverage: [1] No coverage  [2] Generate coverage report

Please select options:
```

## Testing by Language

### C++ with Google Test

**Project structure:**
```
project/
├── CMakeLists.txt
├── src/
│   └── calculator.cpp
├── include/
│   └── calculator.h
└── tests/
    └── test_calculator.cpp
```

**CMakeLists.txt:**
```cmake
cmake_minimum_required(VERSION 3.20)
project(example)

enable_testing()
find_package(GTest REQUIRED)

add_executable(tests tests/test_calculator.cpp src/calculator.cpp)
target_link_libraries(tests GTest::gtest GTest::gtest_main)
target_include_directories(tests PRIVATE include)

add_test(NAME tests COMMAND tests)
```

**Run tests:**
```bash
# Build and test
docker exec course-sandbox-cpp-fundamentals \
  bash -c "cd /workspace/project && cmake -B build && cmake --build build && ctest --test-dir build --output-on-failure"

# Run with verbose output
docker exec course-sandbox-cpp-fundamentals \
  bash -c "cd /workspace/project && ./build/tests --gtest_output=xml"

# Run specific test
docker exec course-sandbox-cpp-fundamentals \
  bash -c "cd /workspace/project && ./build/tests --gtest_filter=CalculatorTest.Add"
```

### C++ with Catch2

**Test file:**
```cpp
#define CATCH_CONFIG_MAIN
#include <catch2/catch.hpp>
#include "calculator.h"

TEST_CASE("Calculator operations", "[calculator]") {
    Calculator calc;

    SECTION("Addition") {
        REQUIRE(calc.add(2, 3) == 5);
    }

    SECTION("Subtraction") {
        REQUIRE(calc.subtract(5, 3) == 2);
    }
}
```

**Run tests:**
```bash
# Compile and run
docker exec course-sandbox-cpp-fundamentals \
  bash -c "g++ -std=c++20 -o /tmp/tests tests/*.cpp src/*.cpp -I include -lcatch2 && /tmp/tests"

# Run with verbose output
docker exec course-sandbox-cpp-fundamentals \
  /tmp/tests --success

# Run specific test
docker exec course-sandbox-cpp-fundamentals \
  /tmp/tests "[calculator]"
```

### Rust with Cargo

**Test file (src/lib.rs or tests/*.rs):**
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
    }

    #[test]
    fn test_subtract() {
        assert_eq!(subtract(5, 3), 2);
    }
}
```

**Run tests:**
```bash
# Run all tests
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace/project && cargo test"

# Run with verbose output
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace/project && cargo test -- --nocapture"

# Run specific test
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace/project && cargo test test_add"

# Run tests matching pattern
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace/project && cargo test calculator"
```

### Python with pytest

**Test file (test_calculator.py):**
```python
import pytest
from calculator import add, subtract

def test_add():
    assert add(2, 3) == 5

def test_subtract():
    assert subtract(5, 3) == 2

@pytest.mark.parametrize("a,b,expected", [
    (1, 1, 2),
    (0, 0, 0),
    (-1, 1, 0),
])
def test_add_parametrized(a, b, expected):
    assert add(a, b) == expected
```

**Run tests:**
```bash
# Run all tests
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest"

# Run with verbose output
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest -v"

# Run specific file
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest test_calculator.py"

# Run specific test
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest test_calculator.py::test_add"

# Run with coverage
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest --cov=. --cov-report=term-missing"

# Run in parallel
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest -n auto"
```

### Go with go test

**Test file (calculator_test.go):**
```go
package calculator

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Add(2, 3) = %d; want 5", result)
    }
}

func TestSubtract(t *testing.T) {
    result := Subtract(5, 3)
    if result != 2 {
        t.Errorf("Subtract(5, 3) = %d; want 2", result)
    }
}
```

**Run tests:**
```bash
# Run all tests
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test ./..."

# Run with verbose output
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -v ./..."

# Run specific package
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -v ./calculator"

# Run specific test
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -v -run TestAdd ./..."

# Run with coverage
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -cover ./..."

# Run with race detection
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -race ./..."
```

## Test Output Format

### Successful Tests
```
=== Running Tests ===
Framework: Google Test
Project: /workspace/project

--- Test Results ---
[==========] Running 5 tests from 2 test suites.
[----------] 3 tests from CalculatorTest
[ RUN      ] CalculatorTest.Add
[       OK ] CalculatorTest.Add (0 ms)
[ RUN      ] CalculatorTest.Subtract
[       OK ] CalculatorTest.Subtract (0 ms)
[ RUN      ] CalculatorTest.Multiply
[       OK ] CalculatorTest.Multiply (0 ms)
[----------] 2 tests from StringTest
[ RUN      ] StringTest.Concat
[       OK ] StringTest.Concat (0 ms)
[ RUN      ] StringTest.Length
[       OK ] StringTest.Length (0 ms)

[==========] 5 tests from 2 test suites ran. (1 ms total)
[  PASSED  ] 5 tests.

--- Summary ---
Tests: 5 passed, 0 failed
Runtime: 0.001s
```

### Failed Tests
```
=== Running Tests ===
Framework: pytest
Project: /workspace

--- Test Results ---
============================= test session starts =============================
collected 3 items

test_calculator.py::test_add PASSED
test_calculator.py::test_subtract FAILED
test_calculator.py::test_multiply PASSED

================================== FAILURES ===================================
__________________________ test_subtract __________________________

    def test_subtract():
>       assert subtract(5, 3) == 3
E       assert 2 == 3
E        +  where 2 = subtract(5, 3)

test_calculator.py:8: AssertionError
=========================== short test summary info ===========================
FAILED test_calculator.py::test_subtract - assert 2 == 3
========================= 1 failed, 2 passed in 0.03s =========================

--- Summary ---
Tests: 2 passed, 1 failed
Runtime: 0.03s
```

## Coverage Reports

### Python Coverage
```bash
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && python -m pytest --cov=. --cov-report=term-missing --cov-report=html"

# View HTML report (copy out of container)
docker cp course-sandbox-python-basics:/workspace/htmlcov ./coverage-report
```

### Rust Coverage
```bash
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo tarpaulin --out Html"
```

### Go Coverage
```bash
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go test -coverprofile=coverage.out ./... && go tool cover -html=coverage.out -o coverage.html"
```

## Testing Exercises and Projects

For course exercises, provide a testing wrapper:

```bash
#!/bin/bash
# test-exercise.sh

exercise_dir=$1
expected_tests=$2

echo "Testing exercise: $exercise_dir"

# Run tests
output=$(docker exec course-sandbox-{course-id} \
  bash -c "cd /workspace/$exercise_dir && {test-command}" 2>&1)
exit_code=$?

# Parse results
passed=$(echo "$output" | grep -c "PASS\|OK\| passed")
failed=$(echo "$output" | grep -c "FAIL\|FAILED\| failed")

echo "Results: $passed passed, $failed failed"

if [ $failed -eq 0 ] && [ $passed -ge $expected_tests ]; then
  echo "Exercise COMPLETE!"
else
  echo "Exercise incomplete or has failures"
fi
```

## Timeout for Tests

Prevent runaway tests:

```bash
# Timeout entire test suite
timeout 60s docker exec course-sandbox-{course-id} \
  bash -c "cd /workspace && cargo test"

# Check for timeout
if [ $? -eq 124 ]; then
  echo "Tests timed out - possible infinite loop in test or code"
fi
```

## Test Discovery

Find all test files in a project:

```bash
# Python
docker exec course-sandbox-python-basics \
  find /workspace -name "test_*.py" -o -name "*_test.py"

# C++ (Google Test)
docker exec course-sandbox-cpp-fundamentals \
  find /workspace -name "*_test.cpp" -o -name "test_*.cpp"

# Rust
docker exec course-sandbox-rust-intro \
  find /workspace -path "*/tests/*.rs" -o -name "*_test.rs"

# Go
docker exec course-sandbox-go-intro \
  find /workspace -name "*_test.go"
```

## Continuous Testing

Watch for changes and re-run tests:

```bash
# Rust with cargo-watch
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo watch -x test"

# Python with pytest-watch (if installed)
docker exec course-sandbox-python-basics \
  bash -c "cd /workspace && ptw"
```

## Best Practices

1. **Run tests frequently** - Catch issues early
2. **Use verbose mode for failures** - Easier debugging
3. **Set timeouts** - Prevent hanging on infinite loops
4. **Generate coverage reports** - Ensure adequate test coverage
5. **Run with sanitizers (C++)** - Catch memory issues in tests
6. **Test in isolation** - Each test should be independent
7. **Clean state between runs** - Avoid test pollution
