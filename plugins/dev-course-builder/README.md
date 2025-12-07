# dev-course-builder

A Claude Code plugin for creating high-quality educational content for programming and software development courses.

## Features

- **Course Profiles**: Define target audience, technical stack, and content style for any programming course
- **Multiple Content Types**: Chapters, exercises, labs, quizzes, slides, and projects
- **Pedagogically Sound**: Built on proven teaching principles for code-first learning
- **Course-Aware**: Content automatically adapts to the course's audience and technical requirements

## Installation

### Option 1: Plugin Directory
```bash
claude --plugin-dir /path/to/dev-course-builder
```

### Option 2: Project Plugin
Copy to your project's `.claude-plugin/` directory.

## Commands

### Content Creation

| Command | Description | Example |
|---------|-------------|---------|
| `/create-course-profile` | Create a new course profile | `/create-course-profile rust-fundamentals` |
| `/write-chapter` | Write a textbook chapter | `/write-chapter cpp-fundamentals pointers` |
| `/create-quiz` | Generate assessments | `/create-quiz cpp-fundamentals chapters 3-4` |
| `/create-exercise` | Create coding exercises | `/create-exercise cpp-fundamentals recursion` |
| `/create-project` | Multi-session project | `/create-project cpp-fundamentals capstone` |
| `/create-lab` | Hands-on lab session | `/create-lab cpp-fundamentals chapters 5-6` |
| `/create-slides` | Lecture slides | `/create-slides cpp-fundamentals memory-management` |

### Content Review

| Command | Description | Example |
|---------|-------------|---------|
| `/review-content` | Review existing content | `/review-content ./chapters/ch03.md` |
| `/review-course` | Full course review | `/review-course cpp-fundamentals` |
| `/review-structure` | Analyze course structure | `/review-structure cpp-fundamentals` |
| `/review-code-examples` | Audit code examples | `/review-code-examples cpp-fundamentals chapter-5` |
| `/suggest-improvements` | Generate improvements | `/suggest-improvements cpp-fundamentals engagement` |

### Sandbox & Code Execution

| Command | Description | Example |
|---------|-------------|---------|
| `/setup-sandbox` | Initialize Docker sandbox | `/setup-sandbox cpp-fundamentals` |
| `/run-code` | Compile and execute code | `/run-code example.cpp` |
| `/test-code` | Run tests in sandbox | `/test-code tests/` |
| `/lint-code` | Lint and analyze code | `/lint-code src/ --fix` |
| `/debug-code` | Debug with GDB/sanitizers | `/debug-code main.cpp gdb` |
| `/validate-examples` | Validate all code examples | `/validate-examples cpp-fundamentals` |

## Course Profiles

Course profiles define how content is generated. Each profile specifies:

- **Target Audience**: Experience level, prerequisites
- **Technical Stack**: Language, compiler, tools, libraries
- **Content Style**: Tone, code format, diagram requirements
- **Course Structure**: Modules, labs, assessments

### Included Profiles

- `cpp-fundamentals` - C++ for junior developers (C++17/20, modern idioms)
- `systems-programming` - Base profile for low-level languages (C, C++, Rust, Zig)

### Creating New Profiles

```
/create-course-profile python-web-development
```

The interactive workflow will guide you through:
1. Course name and ID
2. Target audience selection
3. Programming language
4. Framework philosophy
5. Course focus
6. Prerequisites
7. Duration and environment

## Skills

The plugin provides specialized knowledge through skills:

| Skill | Purpose |
|-------|---------|
| `pedagogy` | Teaching principles for code-first learning |
| `content-templates` | Structural templates for all content types |
| `course-review` | Review frameworks and quality checklists |
| `sandbox` | Docker-based code execution infrastructure |
| `sandbox-templates` | Language-specific Dockerfile templates |
| `courses/cpp-fundamentals` | C++ course configuration |
| `courses/systems-programming` | Systems programming base profile |

## Agents

| Agent | Purpose |
|-------|---------|
| `course-architect` | Content creation - chapters, exercises, labs, quizzes, slides, projects |
| `course-reviewer` | Content review - code correctness, pedagogy, consistency, quality |

Both agents integrate with the Docker sandbox for code validation.

## Code Sandbox

The plugin includes a Docker-based sandbox system for safely executing, testing, linting, and debugging code examples.

### Features

- **Isolated Execution**: All code runs in Docker containers
- **Persistent Environment**: One container per course, maintains state
- **Language Support**: C++, Rust, Python, Go, C, and multi-language
- **Full Toolchain**: Compilers, linters, debuggers, and test frameworks
- **Security**: Dropped capabilities, no network, resource limits

### Quick Start

```bash
# 1. Set up sandbox for a course
/setup-sandbox cpp-fundamentals

# 2. Run code in sandbox
/run-code examples/hello.cpp

# 3. Run tests
/test-code tests/

# 4. Validate all course examples
/validate-examples cpp-fundamentals
```

### Sandbox Templates

Pre-configured environments available:

| Template | Languages | Tools |
|----------|-----------|-------|
| C++ Sandbox | C++17/20/23 | GCC 13, Clang 17, CMake, GDB, Valgrind, clang-tidy |
| Rust Sandbox | Rust stable/nightly | cargo, clippy, rustfmt, miri |
| Python Sandbox | Python 3.12 | pytest, mypy, ruff, black |
| Go Sandbox | Go 1.23+ | go test, staticcheck, delve |
| C Sandbox | C11/17/23 | GCC 13, Clang 17, GDB, Valgrind |
| Multi-language | All above | Full toolchains for each |

### Validation Workflow

Before publishing course content:

1. **Set up sandbox**: `/setup-sandbox course-name`
2. **Validate all examples**: `/validate-examples course-name`
3. **Review failures**: Fix any compile/runtime/output issues
4. **Lint for consistency**: `/lint-code src/`
5. **Check memory safety**: `/debug-code example.cpp sanitize`

## Content Structure

Generated content follows consistent templates:

### Chapters
- Learning objectives
- Prerequisites
- Concept explanations with working code
- Common mistakes and fixes
- Exercises (beginner to challenge)
- Summary and next steps

### Labs
- Part A: Guided practice (35-40 min)
- Part B: Independent challenges (40-45 min)
- Wrap-up and reflection

### Quizzes
- Code tracing questions
- Bug identification
- Code writing
- Conceptual questions
- Detailed answer key

## Quality Standards

All generated content adheres to:

- [ ] Complete, compilable code examples
- [ ] Actual program output (not placeholder)
- [ ] Appropriate for target audience level
- [ ] Progressive complexity
- [ ] Error examples with real compiler messages
- [ ] Memory diagrams for pointer topics (systems courses)

## Directory Structure

```
dev-course-builder/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   ├── course-architect.md      # Content creation agent
│   └── course-reviewer.md       # Quality review agent
├── commands/
│   ├── create-course-profile.md
│   ├── create-exercise.md
│   ├── create-lab.md
│   ├── create-project.md
│   ├── create-quiz.md
│   ├── create-slides.md
│   ├── write-chapter.md
│   ├── review-content.md
│   ├── review-course.md
│   ├── review-structure.md
│   ├── review-code-examples.md
│   ├── suggest-improvements.md
│   ├── setup-sandbox.md         # Sandbox commands
│   ├── run-code.md
│   ├── test-code.md
│   ├── lint-code.md
│   ├── debug-code.md
│   └── validate-examples.md
├── skills/
│   ├── content-templates/
│   │   └── SKILL.md
│   ├── course-review/
│   │   └── SKILL.md
│   ├── courses/
│   │   ├── cpp-fundamentals/
│   │   │   └── SKILL.md
│   │   └── systems-programming/
│   │       └── SKILL.md
│   ├── pedagogy/
│   │   └── SKILL.md
│   ├── sandbox/                  # Sandbox skills
│   │   └── SKILL.md
│   └── sandbox-templates/
│       └── SKILL.md
└── README.md
```

## Example Workflow

1. **Create a course profile** (if you don't have one):
   ```
   /create-course-profile
   ```

2. **Generate a chapter**:
   ```
   /write-chapter cpp-fundamentals smart-pointers
   ```

3. **Create a lab for practice**:
   ```
   /create-lab cpp-fundamentals chapters 5-6
   ```

4. **Generate a quiz**:
   ```
   /create-quiz cpp-fundamentals memory-management
   ```

5. **Review the content**:
   ```
   /review-content ./chapters/smart-pointers.md
   ```

## Tips

- Always specify the course name to ensure content matches your audience
- Use `/review-content` to check quality before publishing
- Course profiles are stored in `skills/courses/` - customize as needed
- The agent respects your course's "no framework" or "framework-centric" philosophy

## Contributing

To add a new course profile:

1. Create `skills/courses/your-course/SKILL.md`
2. Include YAML frontmatter with description and trigger phrases
3. Define audience, technical stack, and content style
4. Add module outline and assessment philosophy

## License

MIT
