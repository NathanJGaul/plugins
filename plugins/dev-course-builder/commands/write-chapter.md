---
description: Write a textbook chapter for a programming course
argument-hint: "[course] [topic] - Course name and chapter topic (e.g., 'cpp-fundamentals pointers')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task]
---

# Write Chapter

Create a textbook chapter tailored to a specific programming course's audience and learning objectives.

## Process

1. **Invoke the course-architect agent** to handle the chapter creation
2. The agent will:
   - Ask which course this chapter is for
   - Load the appropriate course profile
   - Ask for the chapter topic
   - Generate a chapter outline based on course standards
   - Write the complete chapter with appropriate:
     - Explanations at the right level
     - Code examples in the correct language and style
     - Exercises and checkpoints
     - Memory diagrams and visualizations (for systems programming)

## What the Agent Does

The course-architect will:
- Adapt writing style to the student level (beginner vs advanced)
- Use the programming language and toolchain specified in the course profile
- Follow the course's pedagogical philosophy (framework vs no-framework, etc.)
- Structure content according to learning objectives
- Include compilable, runnable code examples

The agent has access to skills for:
- **pedagogy**: Programming teaching principles
- **content-templates**: Chapter structure templates
- **courses/{course-name}**: Course-specific context and standards

## Output

A complete markdown chapter ready to use in your course, including:
- Learning objectives
- Prerequisites
- Conceptual explanations
- Working code examples with compilation instructions
- Common mistakes and how to fix them
- Practice problems with test cases
- Summary and key takeaways
