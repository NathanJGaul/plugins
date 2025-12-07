---
description: Debug code with GDB/LLDB or memory sanitizers in the course Docker sandbox
argument-hint: "[file] [mode] - File to debug and mode (e.g., 'main.cpp gdb' or 'program sanitize')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Skill]
---

# Debug Code in Sandbox

Run debugging tools, memory sanitizers, and profilers on code within the course's isolated Docker sandbox environment.

## Prerequisites

- Docker must be installed and running
- Course sandbox must be set up (use `/setup-sandbox` if not)
- Container must be running with debugging tools installed
- Code must be compiled with debug symbols (`-g` flag)

## Supported Debugging Tools

| Language | Tools | Purpose |
|----------|-------|---------|
| C/C++ | GDB, LLDB | Interactive debugging |
| C/C++ | Valgrind | Memory leak detection |
| C/C++ | AddressSanitizer | Memory error detection |
| C/C++ | UndefinedBehaviorSanitizer | UB detection |
| C/C++ | ThreadSanitizer | Race condition detection |
| Rust | rust-gdb, rust-lldb | Interactive debugging |
| Rust | Miri | Memory safety checking |
| Python | pdb, pdbpp | Interactive debugging |
| Go | delve | Interactive debugging |

## Interactive Workflow

### Step 1: Identify Course and Container

```
Which course sandbox should debug this code?

[1] cpp-fundamentals (course-sandbox-cpp-fundamentals)
[2] rust-intro (course-sandbox-rust-intro)
[3] python-basics (course-sandbox-python-basics)
[4] Specify container name

Please select an option:
```

### Step 2: Select Debug Mode

```
What type of debugging?

[1] Interactive debugger (GDB/LLDB/pdb)
[2] Memory check (Valgrind)
[3] Address sanitizer
[4] Undefined behavior sanitizer
[5] Thread sanitizer
[6] Memory profiling

Please select an option:
```

### Step 3: Code to Debug

```
What should be debugged?

[1] Specific file (provide path)
[2] Compiled binary (provide path)
[3] Current project

Please select an option:
```

## Debugging by Language

### C++ Interactive Debugging

#### Compile with Debug Symbols
```bash
# Compile with debug info
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -g -O0 -o /tmp/prog /workspace/src/main.cpp

# Compile with extra debug info
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -g3 -ggdb -O0 -o /tmp/prog /workspace/src/main.cpp
```

#### GDB Session
```bash
# Start GDB interactively
docker exec -it course-sandbox-cpp-fundamentals \
  gdb /tmp/prog

# Run GDB with commands
docker exec course-sandbox-cpp-fundamentals \
  gdb -ex "break main" -ex "run" -ex "backtrace" /tmp/prog

# GDB batch mode (non-interactive)
docker exec course-sandbox-cpp-fundamentals \
  gdb -batch -ex "run" -ex "bt" /tmp/prog
```

#### Common GDB Commands
```
(gdb) break main          # Set breakpoint at main
(gdb) break file.cpp:25   # Set breakpoint at line 25
(gdb) run                 # Start program
(gdb) run arg1 arg2       # Start with arguments
(gdb) next                # Step over (n)
(gdb) step                # Step into (s)
(gdb) continue            # Continue to next breakpoint (c)
(gdb) print var           # Print variable value (p)
(gdb) print/x ptr         # Print as hex
(gdb) backtrace           # Show call stack (bt)
(gdb) frame 2             # Switch to frame 2
(gdb) info locals         # Show local variables
(gdb) info args           # Show function arguments
(gdb) watch var           # Break when var changes
(gdb) quit                # Exit GDB
```

#### LLDB Session
```bash
# Start LLDB interactively
docker exec -it course-sandbox-cpp-fundamentals \
  lldb /tmp/prog

# LLDB with initial commands
docker exec -it course-sandbox-cpp-fundamentals \
  lldb -o "breakpoint set -n main" -o "run" /tmp/prog
```

#### Common LLDB Commands
```
(lldb) breakpoint set -n main       # Break at main
(lldb) breakpoint set -f file.cpp -l 25  # Break at line
(lldb) run                          # Start program
(lldb) run arg1 arg2                # Start with arguments
(lldb) next                         # Step over
(lldb) step                         # Step into
(lldb) continue                     # Continue
(lldb) frame variable               # Show local variables
(lldb) print var                    # Print variable
(lldb) bt                           # Backtrace
(lldb) quit                         # Exit
```

### Memory Debugging

#### Valgrind (Memory Leak Detection)
```bash
# Basic memory check
docker exec course-sandbox-cpp-fundamentals \
  valgrind /tmp/prog

# Detailed leak check
docker exec course-sandbox-cpp-fundamentals \
  valgrind --leak-check=full --show-leak-kinds=all /tmp/prog

# Track origins of uninitialized values
docker exec course-sandbox-cpp-fundamentals \
  valgrind --track-origins=yes /tmp/prog

# Memory profiling
docker exec course-sandbox-cpp-fundamentals \
  valgrind --tool=massif /tmp/prog
```

#### Valgrind Output Example
```
==12345== HEAP SUMMARY:
==12345==     in use at exit: 72 bytes in 1 blocks
==12345==   total heap usage: 3 allocs, 2 frees, 73,800 bytes allocated
==12345==
==12345== 72 bytes in 1 blocks are definitely lost in loss record 1 of 1
==12345==    at 0x4C2FB0F: malloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==12345==    by 0x10916E: allocate_memory (main.cpp:15)
==12345==    by 0x1091A5: main (main.cpp:22)
==12345==
==12345== LEAK SUMMARY:
==12345==    definitely lost: 72 bytes in 1 blocks
==12345==    indirectly lost: 0 bytes in 0 blocks
==12345==      possibly lost: 0 bytes in 0 blocks
==12345==    still reachable: 0 bytes in 0 blocks
==12345==         suppressed: 0 bytes in 0 blocks
```

### Sanitizers

#### AddressSanitizer (Memory Errors)
```bash
# Compile with ASan
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -fsanitize=address -g -O1 -o /tmp/prog /workspace/src/main.cpp

# Run (ASan enabled automatically)
docker exec course-sandbox-cpp-fundamentals /tmp/prog
```

Detects:
- Buffer overflows (stack, heap, global)
- Use-after-free
- Use-after-return
- Double-free
- Memory leaks

#### ASan Output Example
```
=================================================================
==12345==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x602000000054
READ of size 4 at 0x602000000054 thread T0
    #0 0x55555555528d in main /workspace/src/main.cpp:10
    #1 0x7ffff7a2d82f in __libc_start_main
    #2 0x555555555119 in _start

0x602000000054 is located 4 bytes to the right of 16-byte region
    #0 0x7ffff7b89458 in operator new[](unsigned long)
    #1 0x555555555247 in main /workspace/src/main.cpp:7
```

#### UndefinedBehaviorSanitizer
```bash
# Compile with UBSan
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -fsanitize=undefined -g -o /tmp/prog /workspace/src/main.cpp

# Run
docker exec course-sandbox-cpp-fundamentals /tmp/prog
```

Detects:
- Integer overflow
- Null pointer dereference
- Division by zero
- Invalid shift operations
- Out-of-bounds array access

#### ThreadSanitizer (Race Conditions)
```bash
# Compile with TSan
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -fsanitize=thread -g -o /tmp/prog /workspace/src/main.cpp

# Run
docker exec course-sandbox-cpp-fundamentals /tmp/prog
```

Detects:
- Data races
- Deadlocks
- Lock order violations

#### Combined Sanitizers
```bash
# ASan + UBSan (common combination)
docker exec course-sandbox-cpp-fundamentals \
  g++ -std=c++20 -fsanitize=address,undefined -g -o /tmp/prog /workspace/src/main.cpp
```

### Rust Debugging

#### rust-gdb
```bash
# Compile with debug symbols
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo build"

# Debug with rust-gdb
docker exec -it course-sandbox-rust-intro \
  rust-gdb target/debug/program

# GDB with Rust pretty-printing enabled
docker exec -it course-sandbox-rust-intro \
  gdb -ex "set auto-load safe-path /" target/debug/program
```

#### Miri (Memory Safety)
```bash
# Run with Miri for memory safety checking
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo +nightly miri run"

# Run tests with Miri
docker exec course-sandbox-rust-intro \
  bash -c "cd /workspace && cargo +nightly miri test"
```

Miri detects:
- Use of uninitialized memory
- Out-of-bounds memory access
- Use-after-free
- Invalid pointer use
- Memory leaks

### Python Debugging

#### pdb (Built-in Debugger)
```bash
# Run with pdb
docker exec -it course-sandbox-python-basics \
  python3 -m pdb /workspace/script.py

# Post-mortem debugging (on exception)
docker exec -it course-sandbox-python-basics \
  python3 -c "import pdb; pdb.pm()" < /workspace/script.py
```

#### pdb Commands
```
(Pdb) break 25          # Set breakpoint at line 25
(Pdb) break func        # Set breakpoint at function
(Pdb) continue          # Continue execution (c)
(Pdb) next              # Step over (n)
(Pdb) step              # Step into (s)
(Pdb) print var         # Print variable (p)
(Pdb) pp var            # Pretty print
(Pdb) list              # Show current location (l)
(Pdb) where             # Show stack trace (w)
(Pdb) quit              # Exit (q)
```

#### pdbpp (Enhanced pdb)
```bash
# If pdbpp is installed, it auto-replaces pdb
docker exec -it course-sandbox-python-basics \
  python3 -m pdb /workspace/script.py
```

### Go Debugging

#### Delve
```bash
# Start delve
docker exec -it course-sandbox-go-intro \
  bash -c "cd /workspace && dlv debug"

# Debug specific test
docker exec -it course-sandbox-go-intro \
  bash -c "cd /workspace && dlv test"

# Attach to running process
docker exec -it course-sandbox-go-intro \
  dlv attach <pid>
```

#### Delve Commands
```
(dlv) break main.main           # Set breakpoint
(dlv) break main.go:25          # Break at line
(dlv) continue                  # Continue (c)
(dlv) next                      # Step over (n)
(dlv) step                      # Step into (s)
(dlv) print var                 # Print variable (p)
(dlv) locals                    # Show local variables
(dlv) stack                     # Show stack trace
(dlv) goroutines                # List goroutines
(dlv) exit                      # Exit
```

## Debugging Output Format

### Crash Analysis Report
```
=== Debug Analysis: /workspace/src/main.cpp ===
Tool: AddressSanitizer

--- Crash Detected ---
Type: heap-buffer-overflow
Location: main.cpp:10, in function 'process_data'

Stack Trace:
  #0 main.cpp:10 - process_data()
  #1 main.cpp:25 - main()

Memory Information:
  Address: 0x602000000054
  Region: 16-byte heap allocation at main.cpp:7
  Overflow: 4 bytes past end of allocation

--- Root Cause Analysis ---
The code reads 4 bytes beyond the allocated array.

Line 10: data[size]  // BUG: should be data[size-1] or loop should use < not <=

--- Suggested Fix ---
Change loop condition from 'i <= size' to 'i < size'
```

### Memory Leak Report
```
=== Memory Analysis: /tmp/prog ===
Tool: Valgrind

--- Memory Leaks ---

Leak 1: 72 bytes (definitely lost)
  Allocated at: main.cpp:15 in allocate_memory()
  Not freed by program exit

Leak 2: 128 bytes (definitely lost)
  Allocated at: utils.cpp:42 in create_buffer()
  Not freed by program exit

--- Summary ---
Total leaked: 200 bytes in 2 blocks
Heap usage: 3 allocations, 1 free

--- Recommendations ---
1. Add delete[] call for array allocated at line 15
2. Ensure create_buffer() result is freed
3. Consider using smart pointers (std::unique_ptr)
```

## Debugging Course Examples

For debugging code examples during course development:

```bash
#!/bin/bash
# debug-example.sh

file=$1
container="course-sandbox-cpp-fundamentals"

echo "Debugging: $file"

# Compile with all sanitizers
docker exec $container \
  g++ -std=c++20 -fsanitize=address,undefined -g -O1 \
  -o /tmp/debug_prog "$file" 2>&1

if [ $? -ne 0 ]; then
  echo "Compilation failed"
  exit 1
fi

# Run and capture sanitizer output
output=$(docker exec $container /tmp/debug_prog 2>&1)
exit_code=$?

if echo "$output" | grep -q "ERROR:"; then
  echo "Memory/UB issue detected:"
  echo "$output"
else
  echo "No issues detected"
  echo "Output: $output"
fi
```

## Common Debugging Scenarios

### Segmentation Fault
```bash
# Compile with debug symbols
g++ -g -O0 -o prog main.cpp

# Run in GDB
gdb prog
(gdb) run
# After crash:
(gdb) bt       # See where it crashed
(gdb) frame 0  # Go to crash location
(gdb) info locals  # Check variable values
```

### Memory Leak
```bash
# Run with Valgrind
valgrind --leak-check=full ./prog
# Look for "definitely lost" in output
```

### Infinite Loop
```bash
# Run in GDB
gdb prog
(gdb) run
# Press Ctrl+C when it hangs
(gdb) bt  # See where it's stuck
```

### Race Condition
```bash
# Compile with ThreadSanitizer
g++ -fsanitize=thread -g -o prog main.cpp
./prog
# TSan will report any data races
```

## Best Practices

1. **Always compile with -g for debugging** - Debug symbols are essential
2. **Use -O0 or -O1 for debugging** - Higher optimization makes debugging harder
3. **Run sanitizers during development** - Catch issues early
4. **Use Valgrind for leak detection** - More thorough than ASan for leaks
5. **Set breakpoints strategically** - Near suspected bug locations
6. **Examine variable state** - Print values at each step
7. **Check all error paths** - Bugs often hide in error handling
8. **Test with edge cases** - Empty inputs, large values, etc.
