---
description: Validate all code examples in course materials by compiling and running them in the sandbox
argument-hint: "[course] [scope] - Course and optional scope (e.g., 'cpp-fundamentals' or 'cpp-fundamentals chapter-5')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Task, Skill]
---

# Validate Course Code Examples

Automatically extract, compile, run, and verify all code examples from course materials using the Docker sandbox. This ensures all code in chapters, exercises, labs, and projects is correct and produces the stated output.

## Prerequisites

- Docker must be installed and running
- Course sandbox must be set up (use `/setup-sandbox` if not)
- Container must be running

## What Gets Validated

### Code Block Types

| Type | Marker | Validation |
|------|--------|------------|
| Working Example | No special marker | Must compile, run, match output |
| Error Example | `// ERROR:` comment | Must fail to compile or crash |
| Partial Snippet | `// SNIPPET:` comment | Syntax check only |
| Output Block | `\`\`\`output` or `**Output:**` | Compare against actual |

### Validation Checks

1. **Compilation** - Code compiles without errors
2. **Execution** - Code runs without crashing
3. **Output Matching** - Actual output matches documented output
4. **Error Validation** - Error examples produce expected errors
5. **Timeout Check** - Code doesn't hang (infinite loop detection)

## Interactive Workflow

### Step 1: Course Selection

```
Which course's examples should be validated?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 2: Scope Selection

```
What scope of validation?

[1] All examples in the entire course
[2] Specific module or chapter
[3] Specific file only
[4] Only chapters (skip exercises/labs)
[5] Only exercises and labs

Please select an option:
```

### Step 3: Validation Depth

```
How thorough should validation be?

[1] Quick (compile only)
[2] Standard (compile + run)
[3] Full (compile + run + output comparison)
[4] Exhaustive (full + sanitizers + lint)

Please select an option:
```

### Step 4: Error Handling

```
How to handle validation failures?

[1] Report all and continue
[2] Stop on first failure
[3] Interactive (ask about each failure)

Please select an option:
```

## Validation Process

### 1. Discovery Phase

Find all markdown files and extract code blocks:

```bash
# Find all markdown files in course
find /workspace -name "*.md" -type f

# Extract code blocks from markdown
# Look for ```cpp, ```python, ```rust, etc.
```

### 2. Code Extraction

Parse markdown to extract:
- Code language (from fence info)
- Code content
- Expected output (from following Output block)
- Special markers (ERROR, SNIPPET)
- File location (for error reporting)

### 3. File Preparation

For each code block:
```bash
# Create temporary file
docker exec course-sandbox-{course-id} \
  bash -c "cat > /tmp/example_{n}.{ext}"

# Add necessary headers if missing (for snippets)
```

### 4. Compilation

```bash
# C++ compilation
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -Wall -Wextra -o /tmp/prog_{n} /tmp/example_{n}.cpp 2>&1

# Capture exit code and output
compile_status=$?
compile_output="..."
```

### 5. Execution

```bash
# Run with timeout
docker exec course-sandbox-cpp-fundamentals \
  timeout 10s /tmp/prog_{n} 2>&1

# Capture exit code and output
run_status=$?
run_output="..."
```

### 6. Output Comparison

```bash
# Compare actual vs expected
if [ "$actual_output" = "$expected_output" ]; then
  result="PASS"
else
  result="FAIL"
fi
```

## Validation Report Format

```
╔══════════════════════════════════════════════════════════════════╗
║             CODE EXAMPLES VALIDATION REPORT                       ║
║             Course: C++ Fundamentals                              ║
║             Date: 2024-01-15 14:30:00                            ║
╚══════════════════════════════════════════════════════════════════╝

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                         SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Total Examples:     127
  ✓ Passed:          119 (93.7%)
  ✗ Failed:            6 (4.7%)
  ⊘ Skipped:           2 (1.6%)

  Compile Errors:      3
  Runtime Errors:      1
  Output Mismatch:     2
  Timeouts:            0

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                      FAILURES DETAIL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

┌──────────────────────────────────────────────────────────────────┐
│ FAILURE #1: Compile Error                                        │
│ Location: chapters/05-pointers/chapter.md:127                    │
│ Example: "Pointer Declaration"                                   │
├──────────────────────────────────────────────────────────────────┤
│ Code:                                                            │
│ ```cpp                                                           │
│ int* ptr = nullptr                                               │
│ std::cout << ptr << std::endl;                                   │
│ ```                                                              │
├──────────────────────────────────────────────────────────────────┤
│ Error:                                                           │
│ example.cpp:1:22: error: expected ';' after expression           │
│     int* ptr = nullptr                                           │
│                      ^                                           │
│                      ;                                           │
├──────────────────────────────────────────────────────────────────┤
│ Fix: Add missing semicolon after 'nullptr'                       │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│ FAILURE #2: Output Mismatch                                      │
│ Location: chapters/03-functions/chapter.md:89                    │
│ Example: "Function Return Values"                                │
├──────────────────────────────────────────────────────────────────┤
│ Code:                                                            │
│ ```cpp                                                           │
│ int add(int a, int b) { return a + b; }                          │
│ int main() { std::cout << add(2, 3); }                           │
│ ```                                                              │
├──────────────────────────────────────────────────────────────────┤
│ Expected Output:                                                 │
│ 6                                                                │
│                                                                  │
│ Actual Output:                                                   │
│ 5                                                                │
├──────────────────────────────────────────────────────────────────┤
│ Fix: Documented output is incorrect. 2 + 3 = 5, not 6.           │
│      Update the expected output in the chapter.                  │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│ FAILURE #3: Runtime Error                                        │
│ Location: exercises/ex-07-arrays/exercise.md:45                  │
│ Example: "Array Access"                                          │
├──────────────────────────────────────────────────────────────────┤
│ Code:                                                            │
│ ```cpp                                                           │
│ int arr[5] = {1, 2, 3, 4, 5};                                    │
│ std::cout << arr[5];  // Access element                          │
│ ```                                                              │
├──────────────────────────────────────────────────────────────────┤
│ Error: (with AddressSanitizer)                                   │
│ ERROR: AddressSanitizer: stack-buffer-overflow                   │
│ READ of size 4 at address ...                                    │
├──────────────────────────────────────────────────────────────────┤
│ Fix: Array index out of bounds. arr[5] accesses beyond           │
│      the array. Should be arr[4] for last element.               │
│      If this is intentional error example, add // ERROR: marker  │
└──────────────────────────────────────────────────────────────────┘

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                     BY CHAPTER BREAKDOWN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Chapter 1: Getting Started     15/15 ✓
  Chapter 2: Variables           18/18 ✓
  Chapter 3: Functions           11/12 (1 output mismatch)
  Chapter 4: Control Flow        14/14 ✓
  Chapter 5: Pointers            10/11 (1 compile error)
  Chapter 6: Classes             16/16 ✓
  Chapter 7: Templates           12/12 ✓
  Exercises                      19/20 (1 runtime error)
  Labs                           4/4 ✓

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                     ERROR EXAMPLES VERIFIED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ✓ ch03:42 - Missing return type (correctly fails to compile)
  ✓ ch05:78 - Null pointer dereference (correctly crashes)
  ✓ ch05:112 - Use after free (ASan correctly detects)
  ✓ ch06:95 - Missing constructor (correctly fails to compile)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
                     RECOMMENDATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  1. Fix 3 compile errors (highest priority)
  2. Correct 2 output documentation errors
  3. Review array access example - add // ERROR: if intentional
  4. Consider adding more error examples for common mistakes

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Validation Scripts

### Main Validation Script
```bash
#!/bin/bash
# validate-course.sh

COURSE_ID=$1
CONTAINER="course-sandbox-$COURSE_ID"
WORKSPACE="/workspace"

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[0;33m'
NC='\033[0m'

passed=0
failed=0
skipped=0

# Function to extract code blocks from markdown
extract_code_blocks() {
  local file=$1
  # Use awk/grep to find ```lang ... ``` blocks
  # Return: language, line_number, code_content
}

# Function to validate a code block
validate_code() {
  local lang=$1
  local code=$2
  local expected_output=$3
  local location=$4

  case $lang in
    cpp|c++)
      validate_cpp "$code" "$expected_output" "$location"
      ;;
    rust)
      validate_rust "$code" "$expected_output" "$location"
      ;;
    python)
      validate_python "$code" "$expected_output" "$location"
      ;;
    *)
      echo "Skipping unsupported language: $lang"
      ((skipped++))
      ;;
  esac
}

# C++ validation
validate_cpp() {
  local code=$1
  local expected=$2
  local location=$3

  # Write code to temp file
  echo "$code" | docker exec -i $CONTAINER tee /tmp/test.cpp > /dev/null

  # Check for snippet marker
  if echo "$code" | grep -q "// SNIPPET:"; then
    echo "Skipping snippet at $location"
    ((skipped++))
    return
  fi

  # Compile
  compile_out=$(docker exec $CONTAINER \
    g++ -std=c++20 -Wall -Wextra -fsanitize=address,undefined \
    -o /tmp/test /tmp/test.cpp 2>&1)
  compile_status=$?

  # Check if it's supposed to fail
  if echo "$code" | grep -q "// ERROR:"; then
    if [ $compile_status -ne 0 ]; then
      echo -e "${GREEN}✓ Error example correctly fails: $location${NC}"
      ((passed++))
    else
      # Might be runtime error, try running
      run_out=$(docker exec $CONTAINER timeout 5s /tmp/test 2>&1)
      if [ $? -ne 0 ]; then
        echo -e "${GREEN}✓ Error example correctly fails at runtime: $location${NC}"
        ((passed++))
      else
        echo -e "${RED}✗ Error example should fail: $location${NC}"
        ((failed++))
      fi
    fi
    return
  fi

  if [ $compile_status -ne 0 ]; then
    echo -e "${RED}✗ Compile error at $location${NC}"
    echo "$compile_out"
    ((failed++))
    return
  fi

  # Run
  run_out=$(docker exec $CONTAINER timeout 10s /tmp/test 2>&1)
  run_status=$?

  if [ $run_status -eq 124 ]; then
    echo -e "${RED}✗ Timeout at $location${NC}"
    ((failed++))
    return
  fi

  if [ $run_status -ne 0 ]; then
    echo -e "${RED}✗ Runtime error at $location (exit code: $run_status)${NC}"
    echo "$run_out"
    ((failed++))
    return
  fi

  # Compare output if expected is provided
  if [ -n "$expected" ]; then
    if [ "$run_out" = "$expected" ]; then
      echo -e "${GREEN}✓ Pass: $location${NC}"
      ((passed++))
    else
      echo -e "${RED}✗ Output mismatch at $location${NC}"
      echo "Expected: $expected"
      echo "Actual:   $run_out"
      ((failed++))
    fi
  else
    echo -e "${GREEN}✓ Pass (no output check): $location${NC}"
    ((passed++))
  fi
}

# Main validation loop
find "$WORKSPACE" -name "*.md" | while read file; do
  echo "Validating: $file"
  # Extract and validate each code block
  # ...
done

# Print summary
echo ""
echo "===== VALIDATION SUMMARY ====="
echo -e "Passed:  ${GREEN}$passed${NC}"
echo -e "Failed:  ${RED}$failed${NC}"
echo -e "Skipped: ${YELLOW}$skipped${NC}"
```

## Code Block Markers

### Working Example (Default)
```cpp
// This code should compile and run correctly
int main() {
    std::cout << "Hello, World!\n";
    return 0;
}
```

### Error Example
```cpp
// ERROR: Demonstrates null pointer dereference
// This code intentionally crashes to show what happens
int* ptr = nullptr;
*ptr = 42;  // Crash!
```

### Snippet (Not Standalone)
```cpp
// SNIPPET: This is part of a larger program
void processData(const std::vector<int>& data) {
    for (const auto& item : data) {
        // process item...
    }
}
```

### Expected Output Format

After a code block, provide the expected output:

````markdown
```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!\n";
    return 0;
}
```

**Output:**
```
Hello, World!
```
````

Or using an output block:

````markdown
```cpp
// code here
```

```output
Hello, World!
```
````

## Integration with Course Review

The `/validate-examples` command works alongside `/review-code-examples`:

1. **validate-examples** - Automated compilation and execution testing
2. **review-code-examples** - Human review for style, best practices, pedagogy

Run both for comprehensive code quality assurance:

```bash
# First, validate all code actually works
/validate-examples cpp-fundamentals

# Then, review for style and best practices
/review-code-examples cpp-fundamentals
```

## Best Practices

1. **Run validation after any code changes** - Catch regressions immediately
2. **Include output blocks for all examples** - Enables output comparison
3. **Mark error examples clearly** - Use `// ERROR:` comment
4. **Mark snippets that can't run alone** - Use `// SNIPPET:` comment
5. **Keep validation fast** - Use timeouts to catch infinite loops
6. **Run with sanitizers** - Catch memory errors in examples
7. **Review failures carefully** - May indicate documentation or code bugs
8. **Automate in CI** - Run validation before publishing changes
