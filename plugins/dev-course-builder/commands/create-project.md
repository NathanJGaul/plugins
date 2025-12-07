---
description: Create a multi-session project assignment for a programming course
argument-hint: "[course] [scope] - Course and project scope (e.g., 'cpp-fundamentals capstone')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task, Bash]
---

# Create Project

Generate a comprehensive project assignment that spans multiple sessions, integrating concepts from several chapters.

## Interactive Workflow

### Step 1: Course Selection

```
Which course is this project for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option:
```

### Step 2: Project Scope

```
How large should this project be?

[1] Mini-project (2-4 hours, single concept focus)
[2] Standard project (8-16 hours, multiple concepts)
[3] Capstone project (20-40 hours, course integration)

Please select an option:
```

### Step 3: Concepts to Integrate

```
Which chapters/concepts should this project integrate?
(e.g., "Chapters 4-7: Classes, Containers, Memory Management")
```

### Step 4: Project Type

```
What type of project?

[1] Build from specification (detailed requirements given)
[2] Design and implement (students design the solution)
[3] Extend existing code (add features to provided codebase)
[4] Debugging/refactoring (fix and improve existing code)

Please select an option:
```

### Step 5: Team or Individual

```
Individual or team project?

[1] Individual
[2] Pairs (2 students)
[3] Small teams (3-4 students)

Please select an option:
```

### Step 6: Generate Project

Create the project following the project template:

1. Project overview and motivation
2. Detailed requirements (core + stretch)
3. Milestone breakdown
4. Starter code or project skeleton
5. Test suite for evaluation
6. Grading rubric

## What the Agent Does

The course-architect agent will:

**Project Design:**
- Create engaging, realistic project scenario
- Define clear requirements at multiple levels
- Break down into achievable milestones
- Design appropriate starter material

**Scaffolding:**
- Provide project structure (CMakeLists.txt, directory layout)
- Include necessary boilerplate
- Design interfaces/stubs students will implement
- Create comprehensive test suite

**Documentation:**
- Write clear specification document
- Create milestone guides
- Develop grading rubric
- Include example outputs

## Output

Complete project package including:
- Project specification document
- Starter code/project skeleton
- Test suite
- Grading rubric
- Milestone breakdown
- Example inputs/outputs
