---
description: Create a new course profile for a programming course
argument-hint: "[course-name] - Optional name for the new course (e.g., 'rust-fundamentals')"
allowed-tools: [Read, Write, Glob, AskUserQuestion, Task]
---

# Create Course Profile

Generate a comprehensive course profile that configures how content is created for a specific programming course.

## Interactive Workflow

### Step 1: Course Name and ID

```
What should this course be called?
(e.g., "Rust for Systems Programmers", "Python Web Development")

Course ID (lowercase, hyphens, for directory name):
(e.g., "rust-systems", "python-web")
```

### Step 2: Target Audience

```
Who is the target audience?

[1] Complete beginners (no programming experience)
[2] Beginners (basic programming in another language)
[3] Junior developers (1-2 years experience)
[4] Intermediate developers (2-5 years experience)
[5] Advanced developers (5+ years, new to this language)

Please select an option:
```

### Step 3: Programming Language

```
What programming language?

[1] C++
[2] Rust
[3] Go
[4] Python
[5] JavaScript/TypeScript
[6] Java
[7] C#
[8] Other (specify)

Please select an option:
```

### Step 4: Framework Philosophy

```
Should this course use frameworks?

[1] No frameworks - focus on language and standard library only
[2] Minimal frameworks - introduce 1-2 key frameworks late in course
[3] Framework-centric - teach primarily through a specific framework
[4] Framework comparison - compare multiple frameworks

Please select an option:
```

If frameworks are included:
```
Which framework(s)?
(e.g., "Qt", "Django", "React", "Spring")
```

### Step 5: Course Focus

```
What is the primary focus?

[1] Language fundamentals (syntax, semantics, standard library)
[2] Systems programming (memory, performance, low-level)
[3] Application development (building complete applications)
[4] Web development (frontend/backend/full-stack)
[5] Data processing (analysis, manipulation, visualization)
[6] Game development
[7] Embedded/IoT

Please select an option:
```

### Step 6: Prerequisites

```
What should students already know before starting?
(List specific skills or concepts, one per line)

Example:
- Basic programming in any language
- Command line familiarity
- Version control basics
```

### Step 7: Course Duration

```
How long is this course?

[1] 4-6 weeks (intensive bootcamp)
[2] 8-10 weeks (short course)
[3] 12-16 weeks (semester-length)
[4] Self-paced (no fixed duration)

Please select an option:
```

### Step 8: Learning Environment

```
What development environment?

[1] Local development (IDE + compiler/runtime)
[2] Online IDE (Replit, CodeSandbox, etc.)
[3] Cloud-based (Jupyter, Google Colab)
[4] Hybrid (local + online for practice)

Please select an option:
```

### Step 9: Generate Profile

Create a comprehensive course profile including:

1. Course overview and philosophy
2. Target audience with prerequisites
3. Technical stack (language, tools, frameworks)
4. Content style guidelines
5. Module/chapter outline
6. Lab/exercise structure
7. Assessment philosophy
8. Quality standards

## What the Agent Does

The course-architect agent will:

**Profile Design:**
- Structure course based on language and focus
- Design appropriate module sequence
- Define content style for audience
- Specify technical requirements

**Template Generation:**
- Create course-specific callout box types
- Define code example format
- Specify diagram requirements
- Set assessment standards

## Output

Complete course profile file at:
`skills/courses/{course-id}/course-profile.md`

Including:
- Course metadata
- Audience definition
- Learning philosophy
- Technical stack
- Content style guide
- Module outline
- Lab structure
- Assessment approach
- Quality checklist

The profile can then be used by all other commands to generate course-specific content.
