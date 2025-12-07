---
description: Initialize Docker sandbox for a course's code execution environment
argument-hint: "[course] - Course to set up sandbox for (e.g., 'cpp-fundamentals')"
allowed-tools: [Read, Write, Glob, Grep, Bash, AskUserQuestion, Task, Skill]
---

# Setup Course Sandbox

Initialize a Docker-based isolated development environment for compiling, running, testing, linting, and debugging code in course materials.

## Interactive Workflow

### Step 1: Course Selection

```
Which course needs a sandbox environment?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 2: Sandbox Template Selection

```
Select the sandbox template for this course:

[1] C++ Sandbox (GCC 13, Clang 17, CMake, GDB, Valgrind, clang-tidy)
[2] Rust Sandbox (rustc, cargo, clippy, rustfmt, miri)
[3] Python Sandbox (Python 3.12, pytest, mypy, ruff, black)
[4] Go Sandbox (Go 1.23, gofmt, staticcheck, delve)
[5] C Sandbox (GCC 13, Clang 17, Make, GDB, Valgrind)
[6] Multi-Language Sandbox (C, C++, Python, Go, Rust)
[7] Custom (I'll provide a Dockerfile)

Please select an option:
```

### Step 3: Configuration Options

```
Configure sandbox settings:

Container Name: course-sandbox-{course-id}
Memory Limit: [1] 1GB  [2] 2GB  [3] 4GB  [4] Custom
CPU Limit: [1] 1 CPU  [2] 2 CPUs  [3] 4 CPUs
Network Access: [1] Disabled (recommended)  [2] Enabled

Please select options:
```

### Step 4: Verify Docker Installation

Before proceeding, verify Docker is available:

```bash
# Check Docker is installed and running
docker --version
docker info
```

If Docker is not available, provide installation guidance.

### Step 5: Generate Sandbox Configuration

Create the `.sandbox/` directory structure in the course:

```
{course-directory}/
└── .sandbox/
    ├── Dockerfile
    ├── docker-compose.yml
    ├── .dockerignore
    └── scripts/
        ├── setup.sh
        ├── validate.sh
        └── cleanup.sh
```

## What Gets Created

### Dockerfile

Language-specific Dockerfile from the sandbox-templates skill, customized for the course:
- Base image with appropriate compilers/interpreters
- Linting tools (clang-tidy, clippy, ruff, etc.)
- Testing frameworks (gtest, catch2, pytest, etc.)
- Debugging tools (gdb, lldb, valgrind, etc.)
- Non-root user for security

### docker-compose.yml

Container orchestration with security constraints:
```yaml
version: '3.8'

services:
  sandbox:
    build:
      context: ..
      dockerfile: .sandbox/Dockerfile
    container_name: course-sandbox-{course-id}
    volumes:
      - ..:/workspace
    working_dir: /workspace
    stdin_open: true
    tty: true
    cap_drop:
      - ALL
    security_opt:
      - no-new-privileges:true
    deploy:
      resources:
        limits:
          memory: {memory-limit}
          cpus: '{cpu-limit}'
    network_mode: {none|bridge}
```

### .dockerignore

Excludes unnecessary files from the build context:
- Build artifacts (build/, target/, __pycache__/)
- IDE configuration (.idea/, .vscode/)
- Git data (.git/)
- Large binary files

### Scripts

**setup.sh** - Post-creation initialization:
```bash
#!/bin/bash
# Verify container is running
# Install any additional dependencies
# Set up environment variables
```

**validate.sh** - Validate all code examples:
```bash
#!/bin/bash
# Find all code files
# Compile each one
# Run and capture output
# Compare to expected output
# Generate report
```

**cleanup.sh** - Clean up temporary files:
```bash
#!/bin/bash
# Remove compiled binaries
# Clear /tmp
# Reset container state
```

## Post-Setup Actions

### Build the Sandbox Image

```bash
cd {course-directory}
docker build -t course-sandbox-{course-id}:latest -f .sandbox/Dockerfile .
```

### Create and Start the Container

```bash
docker run -d \
  --name course-sandbox-{course-id} \
  -v "$(pwd):/workspace" \
  -w /workspace \
  --cap-drop=ALL \
  --security-opt=no-new-privileges \
  --memory=2g \
  --cpus=2 \
  --network=none \
  course-sandbox-{course-id}:latest \
  tail -f /dev/null
```

### Verify Setup

```bash
# Check container is running
docker ps --filter "name=course-sandbox-{course-id}"

# Test a simple command
docker exec course-sandbox-{course-id} echo "Sandbox ready!"

# Test compiler (for C++)
docker exec course-sandbox-{course-id} g++ --version
```

## Usage After Setup

Once the sandbox is set up, use these commands:
- `/run-code` - Compile and execute code files
- `/test-code` - Run tests in the sandbox
- `/lint-code` - Lint code with language-appropriate tools
- `/debug-code` - Start debugging session
- `/validate-examples` - Validate all code examples in course

## Sandbox Management

### Status
```bash
docker ps -a --filter "name=course-sandbox-{course-id}"
```

### Start (if stopped)
```bash
docker start course-sandbox-{course-id}
```

### Stop (to save resources)
```bash
docker stop course-sandbox-{course-id}
```

### Rebuild (after Dockerfile changes)
```bash
docker rm -f course-sandbox-{course-id}
docker build -t course-sandbox-{course-id}:latest -f .sandbox/Dockerfile .
# Then run the create command again
```

### Full Reset
```bash
docker rm -f course-sandbox-{course-id}
docker rmi course-sandbox-{course-id}:latest
# Then rebuild from scratch
```

## Integration with Course Profile

After setup, the course profile should be updated to include sandbox configuration:

```markdown
## Sandbox Configuration

**Container:** course-sandbox-{course-id}
**Template:** {template-name}
**Status:** Configured

### Quick Commands
- Build: `docker build -t course-sandbox-{course-id}:latest -f .sandbox/Dockerfile .`
- Start: `docker start course-sandbox-{course-id}`
- Stop: `docker stop course-sandbox-{course-id}`
- Shell: `docker exec -it course-sandbox-{course-id} /bin/bash`
```

## Troubleshooting

### Docker Not Running
```
Error: Cannot connect to Docker daemon
Solution: Start Docker daemon or Docker Desktop
```

### Permission Denied
```
Error: Permission denied while trying to connect to Docker
Solution: Add user to docker group: sudo usermod -aG docker $USER
```

### Image Build Failed
```
Error: Dockerfile build failed
Solution: Check Dockerfile syntax, network connectivity for package downloads
```

### Container Won't Start
```
Error: Container exits immediately
Solution: Check container logs: docker logs course-sandbox-{course-id}
```

## Security Notes

- Containers run with dropped capabilities (`--cap-drop=ALL`)
- No new privileges can be gained (`--security-opt=no-new-privileges`)
- Network is disabled by default (`--network=none`)
- Memory and CPU are limited to prevent resource exhaustion
- Non-root user inside container
- Course files are mounted read-write; consider read-only for production
