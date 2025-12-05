---
description: Create a hands-on coding lab for a programming course
argument-hint: "[course] [chapters] - Course and chapters to cover (e.g., 'cpp-fundamentals chapters 5-6')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task]
---

# Create Lab

Generate a structured lab session where students practice programming concepts through guided exercises and independent challenges.

## Interactive Workflow

This command uses a numbered-option interactive workflow to gather requirements and create the lab.

### Step 1: Course Selection

Ask the user which course this lab is for:

```
Which course is this lab for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option by number:
```

Load the appropriate course profile based on selection.

### Step 2: Chapter/Topic Input

Ask which chapters or topics the lab should reinforce:

```
Which chapters or topics should this lab reinforce?
(Provide chapter numbers or topic names, e.g., "Chapters 5-6" or "Pointers and References")
```

Read the specified chapters if available to analyze content.

### Step 3: Topic Confirmation

Based on the chapters, analyze and present planned topics:

```
Based on [chapters specified], I plan to cover these concepts:
- [Concept 1 identified from chapter analysis]
- [Concept 2 identified from chapter analysis]
- [Concept 3 identified from chapter analysis]

[1] Accept these topics
[2] Add or modify topics

Please select an option:
```

### Step 4: Lab Duration

Ask about time constraints:

```
How long should this lab be?

[1] 60 minutes (4 challenges)
[2] 90 minutes (6 challenges) - recommended
[3] 120 minutes (8 challenges)

Please select an option:
```

### Step 5: Lab Format

```
What format should the lab take?

[1] Markdown with code blocks (for any editor)
[2] Jupyter Notebook (if Python or supported language)
[3] Project template (CMake/Makefile structure)

Please select an option:
```

### Step 6: Save Location

```
Where should I save the lab?

[Suggested path based on course structure]

Please provide the directory path (or press Enter to use suggested path):
```

### Step 7: Generate Lab

Create the lab following the course profile and content templates:

1. Structure the lab with Part A (guided) and Part B (independent)
2. Ensure all code compiles and runs
3. Include test cases for validation
4. Add appropriate scaffolding for the audience level
5. Create instructor solution guide separately

### Step 8: Completion Message

```
Lab created successfully!

Location: [full path to created file]

Contents:
- Part A: Guided Practice ([X] minutes, [Y] sections)
- Part B: Independent Challenges ([X] minutes, [Y] challenges)
- Solution guide: [path to solutions]

Next steps:
1. Review the lab and make any necessary edits
2. Test all code examples compile and run correctly
3. Verify timing estimates are realistic
```

## What the Agent Does

The course-architect agent will:

**Planning Phase:**
- Load appropriate course profile based on selection
- Analyze specified chapters to extract key concepts
- Identify topics requiring hands-on practice
- Determine appropriate difficulty progression
- Confirm all details with user using numbered options

**Content Creation Phase:**
- Generate lab following the exact structure required
- Create Part A with step-by-step guided examples
- Create Part B with progressive challenges
- Include test cases for each challenge
- Add hints at appropriate levels
- Ensure timing estimates are realistic

**Quality Assurance:**
- All code compiles without errors
- Test cases validate correct solutions
- Difficulty progression is appropriate
- Clear instructions at each step

## Course-Specific Requirements

### Systems Programming Courses (C++, Rust, etc.)
- All code must compile with standard flags
- Include memory diagrams where relevant
- Show expected output for all examples
- Include debugging exercises

### Higher-Level Language Courses
- Focus on language idioms and patterns
- Include REPL-style exploration where appropriate
- Test-driven development integration

## Skills Available to Agent

The agent has access to:
- **pedagogy**: General teaching principles for programming
- **content-templates**: Lab structure patterns
- **courses/{course-name}**: Course-specific context

## Output

A complete lab document including:
- Learning objectives
- Setup instructions
- Part A: Guided practice sections with explanations
- Part B: Independent challenges with test cases
- Hints (progressively revealed)
- Solution guide (separate file)
- Wrap-up and reflection questions
