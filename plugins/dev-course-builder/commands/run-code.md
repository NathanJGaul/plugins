---
description: Compile and execute code in the course Docker sandbox
argument-hint: "[file] [args] - File to run and optional arguments (e.g., 'example.cpp' or 'main.rs --verbose')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Skill]
---

# Run Code in Sandbox

Compile (if needed) and execute code files within the course's isolated Docker sandbox environment.

## Prerequisites

- Docker must be installed and running
- Course sandbox must be set up (use `/setup-sandbox` if not)
- Container must be running

## Interactive Workflow

### Step 1: Identify Course and Container

Detect the current course from the working directory or ask:

```
Which course sandbox should execute this code?

[1] cpp-fundamentals (course-sandbox-cpp-fundamentals)
[2] rust-intro (course-sandbox-rust-intro)
[3] Specify container name

Please select an option:
```

### Step 2: Select Code to Run

```
What code should be executed?

[1] Specific file (provide path)
[2] Code from current context (paste or reference)
[3] All code in current chapter/exercise

Please select an option:
```

### Step 3: Execution Options

```
Execution options:

Compiler flags: [1] Default  [2] Debug (-g)  [3] Optimized (-O2)  [4] Custom
Timeout: [1] 10s  [2] 30s  [3] 60s  [4] No timeout (dangerous)
Input: [1] None  [2] Provide stdin  [3] Input file

Please select options:
```

## Execution Process

### 1. Verify Container Status

```bash
# Check if container exists and is running
container_status=$(docker inspect -f '{{.State.Running}}' course-sandbox-{course-id} 2>/dev/null)

if [ "$container_status" != "true" ]; then
  echo "Container not running. Starting..."
  docker start course-sandbox-{course-id}
fi
```

### 2. Detect Language

Determine the language from file extension:

| Extension | Language | Compiler/Interpreter |
|-----------|----------|---------------------|
| `.cpp`, `.cc`, `.cxx` | C++ | g++ / clang++ |
| `.c` | C | gcc / clang |
| `.rs` | Rust | rustc / cargo |
| `.py` | Python | python3 |
| `.go` | Go | go run |
| `.java` | Java | javac + java |
| `.js`, `.mjs` | JavaScript | node |
| `.ts` | TypeScript | ts-node |

### 3. Compile (if needed)

For compiled languages, compile first:

**C++:**
```bash
docker exec course-sandbox-{course-id} \
  g++ -std=c++20 -Wall -Wextra -o /tmp/prog /workspace/{file}
```

**Rust:**
```bash
docker exec course-sandbox-{course-id} \
  rustc -o /tmp/prog /workspace/{file}
```

**C:**
```bash
docker exec course-sandbox-{course-id} \
  gcc -std=c17 -Wall -Wextra -o /tmp/prog /workspace/{file}
```

**Go:**
```bash
docker exec course-sandbox-{course-id} \
  go build -o /tmp/prog /workspace/{file}
```

### 4. Execute

Run with timeout to prevent infinite loops:

**Compiled programs:**
```bash
docker exec course-sandbox-{course-id} \
  timeout {timeout}s /tmp/prog {args}
```

**Python:**
```bash
docker exec course-sandbox-{course-id} \
  timeout {timeout}s python3 /workspace/{file} {args}
```

**Node.js:**
```bash
docker exec course-sandbox-{course-id} \
  timeout {timeout}s node /workspace/{file} {args}
```

### 5. Capture and Display Output

```bash
# Capture both stdout and stderr
output=$(docker exec course-sandbox-{course-id} \
  timeout {timeout}s /tmp/prog 2>&1)
exit_code=$?

echo "Exit code: $exit_code"
echo "Output:"
echo "$output"
```

## Output Format

### Successful Execution
```
=== Running: example.cpp ===
Compiled with: g++ -std=c++20 -Wall -Wextra

--- Output ---
Hello, World!
The answer is: 42

--- Execution Summary ---
Exit code: 0
Runtime: 0.003s
```

### Compilation Error
```
=== Running: example.cpp ===
Compiling with: g++ -std=c++20 -Wall -Wextra

--- Compilation Failed ---
example.cpp:5:10: error: expected ';' after expression
    int x = 5
             ^
             ;
1 error generated.

Exit code: 1
```

### Runtime Error
```
=== Running: example.cpp ===
Compiled successfully

--- Output ---
Starting program...

--- Runtime Error ---
Segmentation fault (core dumped)

Exit code: 139 (SIGSEGV)
```

### Timeout
```
=== Running: infinite_loop.cpp ===
Compiled successfully

--- Execution Timeout ---
Program did not complete within 10 seconds.
Possible infinite loop detected.

Exit code: 124 (TIMEOUT)
```

## Compiler/Interpreter Options

### C++ Options
| Flag | Purpose |
|------|---------|
| `-std=c++20` | Use C++20 standard |
| `-Wall -Wextra` | Enable all warnings |
| `-Werror` | Treat warnings as errors |
| `-g` | Include debug symbols |
| `-O2` | Optimize for speed |
| `-fsanitize=address` | Enable AddressSanitizer |
| `-fsanitize=undefined` | Enable UndefinedBehaviorSanitizer |

### Rust Options
| Flag | Purpose |
|------|---------|
| `--edition 2021` | Use Rust 2021 edition |
| `-g` | Include debug symbols |
| `-O` | Optimize |
| `-W warnings` | Enable warnings |

### Python Options
| Flag | Purpose |
|------|---------|
| `-u` | Unbuffered output |
| `-B` | Don't write .pyc files |
| `-O` | Optimize (remove asserts) |

## Providing Input

### Via stdin
```bash
echo "input data" | docker exec -i course-sandbox-{course-id} /tmp/prog
```

### From file
```bash
docker exec course-sandbox-{course-id} /tmp/prog < /workspace/input.txt
```

### Interactive (not recommended in sandbox)
```bash
docker exec -it course-sandbox-{course-id} /tmp/prog
```

## Running with Sanitizers

For debugging memory issues:

### AddressSanitizer
```bash
docker exec course-sandbox-{course-id} \
  g++ -std=c++20 -fsanitize=address -g -o /tmp/prog /workspace/{file}
docker exec course-sandbox-{course-id} /tmp/prog
```

### UndefinedBehaviorSanitizer
```bash
docker exec course-sandbox-{course-id} \
  g++ -std=c++20 -fsanitize=undefined -g -o /tmp/prog /workspace/{file}
docker exec course-sandbox-{course-id} /tmp/prog
```

### ThreadSanitizer
```bash
docker exec course-sandbox-{course-id} \
  g++ -std=c++20 -fsanitize=thread -g -o /tmp/prog /workspace/{file}
docker exec course-sandbox-{course-id} /tmp/prog
```

## Running Cargo/CMake Projects

### Rust with Cargo
```bash
docker exec course-sandbox-{course-id} \
  bash -c "cd /workspace/{project-dir} && cargo run"
```

### C++ with CMake
```bash
docker exec course-sandbox-{course-id} \
  bash -c "cd /workspace/{project-dir} && cmake -B build && cmake --build build && ./build/{executable}"
```

## Comparing Output

Compare actual output against expected:

```bash
expected="Hello, World!"
actual=$(docker exec course-sandbox-{course-id} /tmp/prog 2>&1)

if [ "$actual" = "$expected" ]; then
  echo "PASS: Output matches expected"
else
  echo "FAIL: Output mismatch"
  echo "Expected: $expected"
  echo "Actual:   $actual"
fi
```

## Error Codes Reference

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 124 | Timeout (killed by timeout command) |
| 126 | Permission denied |
| 127 | Command not found |
| 134 | Abort (SIGABRT) |
| 136 | Floating point exception (SIGFPE) |
| 139 | Segmentation fault (SIGSEGV) |
| 137 | Killed (SIGKILL, usually OOM) |

## Cleanup

After execution, compiled binaries remain in `/tmp` inside the container. To clean up:

```bash
docker exec course-sandbox-{course-id} rm -f /tmp/prog
```

Or clean all temporary files:

```bash
docker exec course-sandbox-{course-id} rm -rf /tmp/*
```

## Usage Tips

1. **Always use timeout** - Prevents infinite loops from hanging
2. **Check exit code** - Non-zero indicates problems
3. **Capture stderr** - Error messages go to stderr
4. **Use sanitizers for debugging** - Find memory issues early
5. **Clean up binaries** - Prevents confusion with old versions
