---
description: Lint and analyze code quality in the course Docker sandbox
argument-hint: "[path] [options] - File or directory to lint (e.g., 'src/' or 'main.cpp --fix')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Skill]
---

# Lint Code in Sandbox

Run static analysis, style checks, and linting tools on code within the course's isolated Docker sandbox environment.

## Prerequisites

- Docker must be installed and running
- Course sandbox must be set up (use `/setup-sandbox` if not)
- Container must be running with linting tools installed

## Supported Linting Tools

| Language | Tools | Purpose |
|----------|-------|---------|
| C++ | clang-tidy, cppcheck, clang-format | Static analysis, style |
| Rust | clippy, rustfmt | Lints, formatting |
| Python | ruff, mypy, black | Lints, types, formatting |
| Go | golint, staticcheck, gofmt, go vet | Lints, analysis, formatting |
| JavaScript | ESLint, Prettier | Lints, formatting |

## Interactive Workflow

### Step 1: Identify Course and Container

```
Which course sandbox should lint this code?

[1] cpp-fundamentals (course-sandbox-cpp-fundamentals)
[2] rust-intro (course-sandbox-rust-intro)
[3] python-basics (course-sandbox-python-basics)
[4] Specify container name

Please select an option:
```

### Step 2: Select Lint Scope

```
What should be linted?

[1] Entire project
[2] Specific directory
[3] Specific file
[4] Changed files only (git diff)

Please select an option:
```

### Step 3: Lint Type

```
What type of analysis?

[1] Full analysis (all checks)
[2] Style/formatting only
[3] Static analysis only
[4] Type checking only
[5] Security checks only

Please select an option:
```

### Step 4: Auto-fix Option

```
Should issues be auto-fixed where possible?

[1] Report only (don't modify files)
[2] Auto-fix safe issues
[3] Auto-fix all (including potentially breaking)

Please select an option:
```

## Linting by Language

### C++ Linting

#### clang-tidy (Static Analysis)
```bash
# Lint single file
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy /workspace/src/main.cpp -- -std=c++20 -I/workspace/include

# Lint with all checks
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy -checks='*' /workspace/src/main.cpp -- -std=c++20

# Lint specific categories
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy -checks='modernize-*,performance-*,bugprone-*' \
  /workspace/src/main.cpp -- -std=c++20

# Auto-fix issues
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy -fix /workspace/src/main.cpp -- -std=c++20

# Lint entire directory
docker exec course-sandbox-cpp-fundamentals \
  bash -c "find /workspace/src -name '*.cpp' | xargs clang-tidy -- -std=c++20"
```

#### cppcheck (Additional Static Analysis)
```bash
# Basic check
docker exec course-sandbox-cpp-fundamentals \
  cppcheck --std=c++20 /workspace/src/main.cpp

# Enable all checks
docker exec course-sandbox-cpp-fundamentals \
  cppcheck --enable=all --std=c++20 /workspace/src/

# Check with includes
docker exec course-sandbox-cpp-fundamentals \
  cppcheck --enable=all --std=c++20 -I/workspace/include /workspace/src/

# XML output for parsing
docker exec course-sandbox-cpp-fundamentals \
  cppcheck --enable=all --xml /workspace/src/ 2>&1
```

#### clang-format (Style Checking)
```bash
# Check formatting (dry run)
docker exec course-sandbox-cpp-fundamentals \
  clang-format --dry-run --Werror /workspace/src/main.cpp

# Show what would change
docker exec course-sandbox-cpp-fundamentals \
  clang-format --dry-run -style=file /workspace/src/main.cpp

# Auto-format file
docker exec course-sandbox-cpp-fundamentals \
  clang-format -i /workspace/src/main.cpp

# Format all files
docker exec course-sandbox-cpp-fundamentals \
  bash -c "find /workspace/src -name '*.cpp' -o -name '*.h' | xargs clang-format -i"
```

### Rust Linting

#### clippy (Lints)
```bash
# Run clippy
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo clippy"

# Treat warnings as errors
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo clippy -- -D warnings"

# With all lints
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo clippy -- -W clippy::all -W clippy::pedantic"

# Auto-fix (where possible)
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo clippy --fix --allow-dirty"
```

#### rustfmt (Formatting)
```bash
# Check formatting
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo fmt --check"

# Auto-format
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo fmt"

# Format specific file
docker exec course-sandbox-rust-intro \
  rustfmt /workspace/src/main.rs
```

### Python Linting

#### ruff (Fast Linter)
```bash
# Check all files
docker exec course-sandbox-python-basics \
  ruff check /workspace

# Check specific file
docker exec course-sandbox-python-basics \
  ruff check /workspace/main.py

# Auto-fix issues
docker exec course-sandbox-python-basics \
  ruff check --fix /workspace

# Show all issues (don't stop at first)
docker exec course-sandbox-python-basics \
  ruff check --show-source /workspace

# Select specific rules
docker exec course-sandbox-python-basics \
  ruff check --select E,F,W /workspace
```

#### mypy (Type Checking)
```bash
# Type check file
docker exec course-sandbox-python-basics \
  mypy /workspace/main.py

# Strict type checking
docker exec course-sandbox-python-basics \
  mypy --strict /workspace/main.py

# Type check package
docker exec course-sandbox-python-basics \
  mypy /workspace/src/

# Ignore missing imports
docker exec course-sandbox-python-basics \
  mypy --ignore-missing-imports /workspace/
```

#### black (Formatting)
```bash
# Check formatting
docker exec course-sandbox-python-basics \
  black --check /workspace

# Show diff of changes
docker exec course-sandbox-python-basics \
  black --diff /workspace/main.py

# Auto-format
docker exec course-sandbox-python-basics \
  black /workspace
```

#### isort (Import Sorting)
```bash
# Check imports
docker exec course-sandbox-python-basics \
  isort --check-only /workspace

# Auto-fix imports
docker exec course-sandbox-python-basics \
  isort /workspace
```

### Go Linting

#### golint (Style)
```bash
docker exec course-sandbox-go-intro \
  golint /workspace/...
```

#### staticcheck (Static Analysis)
```bash
docker exec course-sandbox-go-intro \
  staticcheck /workspace/...
```

#### go vet (Analysis)
```bash
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && go vet ./..."
```

#### gofmt (Formatting)
```bash
# Check formatting
docker exec course-sandbox-go-intro \
  gofmt -d /workspace

# Auto-format
docker exec course-sandbox-go-intro \
  gofmt -w /workspace
```

#### golangci-lint (Comprehensive)
```bash
# Run all linters
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && golangci-lint run"

# Run specific linters
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && golangci-lint run --enable gosec,govet,errcheck"

# Auto-fix
docker exec course-sandbox-go-intro \
  bash -c "cd /workspace && golangci-lint run --fix"
```

## Output Format

### Lint Report
```
=== Linting: /workspace/src ===
Tool: clang-tidy
Standard: C++20

--- Issues Found ---

/workspace/src/main.cpp:15:5: warning: use range-based for loop [modernize-loop-convert]
    for (int i = 0; i < vec.size(); ++i) {
    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    for (auto & elem : vec) {

/workspace/src/main.cpp:23:10: warning: use nullptr instead of 0 [modernize-use-nullptr]
    int* p = 0;
             ^
             nullptr

/workspace/src/utils.cpp:8:1: warning: function 'helper' could be declared static [misc-use-anonymous-namespace]

--- Summary ---
Files checked: 5
Issues found: 3
  Warnings: 3
  Errors: 0

Recommended fixes:
  - Modernize loop on line 15
  - Use nullptr instead of 0 on line 23
  - Consider making 'helper' function static
```

### Format Check Output
```
=== Format Check: /workspace/src ===
Tool: clang-format

--- Formatting Issues ---

/workspace/src/main.cpp
@@ -15,7 +15,7 @@
-    int x=5;
+    int x = 5;

/workspace/src/utils.cpp
@@ -8,10 +8,10 @@
-void foo(){
+void foo() {

--- Summary ---
Files with issues: 2
Files correctly formatted: 3
Total files: 5
```

## Pre-defined Lint Configurations

### C++ Configuration (.clang-tidy)
```yaml
---
Checks: >
  -*,
  bugprone-*,
  modernize-*,
  performance-*,
  readability-*,
  -modernize-use-trailing-return-type
WarningsAsErrors: ''
HeaderFilterRegex: '.*'
AnalyzeTemporaryDtors: false
FormatStyle: file
```

### Python Configuration (pyproject.toml)
```toml
[tool.ruff]
select = ["E", "F", "W", "I", "N", "B", "A", "C4", "SIM"]
ignore = ["E501"]  # line length handled by black

[tool.mypy]
strict = true
ignore_missing_imports = true

[tool.black]
line-length = 88
```

### Rust Configuration (clippy.toml)
```toml
too-many-arguments-threshold = 7
type-complexity-threshold = 250
```

## Linting Course Examples

For validating code examples in course materials:

```bash
#!/bin/bash
# lint-examples.sh

course_id=$1
container="course-sandbox-$course_id"

echo "Linting all code examples..."

# Find all code files in course
find /workspace -name "*.cpp" -o -name "*.py" -o -name "*.rs" | while read file; do
  echo "Checking: $file"

  case "$file" in
    *.cpp)
      docker exec $container clang-tidy "$file" -- -std=c++20 2>&1
      ;;
    *.py)
      docker exec $container ruff check "$file" 2>&1
      docker exec $container mypy "$file" 2>&1
      ;;
    *.rs)
      docker exec $container rustfmt --check "$file" 2>&1
      ;;
  esac
done
```

## Severity Levels

| Level | Meaning | Action |
|-------|---------|--------|
| Error | Code won't compile or has critical bug | Must fix |
| Warning | Potential issue or bad practice | Should fix |
| Info | Style suggestion or improvement | Consider fixing |
| Hint | Minor improvement opportunity | Optional |

## Filtering Output

### By Severity
```bash
# Only errors
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy -warnings-as-errors='*' /workspace/src/main.cpp -- -std=c++20

# Only specific categories
docker exec course-sandbox-cpp-fundamentals \
  clang-tidy -checks='-*,bugprone-*' /workspace/src/main.cpp -- -std=c++20
```

### By File Pattern
```bash
# Only source files (not headers)
docker exec course-sandbox-cpp-fundamentals \
  bash -c "find /workspace/src -name '*.cpp' | xargs clang-tidy -- -std=c++20"
```

## Integration with Code Review

When reviewing course content:

1. **Run lint on all examples** - Catch style and correctness issues
2. **Check formatting consistency** - Ensure uniform style
3. **Verify type correctness** - For typed languages
4. **Check for deprecated patterns** - Ensure modern practices
5. **Security analysis** - Check for vulnerabilities

## Best Practices

1. **Lint before committing** - Catch issues early
2. **Use auto-fix carefully** - Review changes before accepting
3. **Configure project standards** - Use config files for consistency
4. **Don't ignore warnings** - They often indicate real issues
5. **Run multiple tools** - Each catches different issues
6. **Integrate with CI** - Automate linting checks
