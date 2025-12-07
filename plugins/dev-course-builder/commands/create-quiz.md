---
description: Create a quiz or assessment for a programming course
argument-hint: "[course] [topics] - Course and topics to cover (e.g., 'cpp-fundamentals chapters 3-4')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task]
---

# Create Quiz

Generate a quiz to assess understanding of programming concepts, including code reading, writing, and conceptual questions.

## Interactive Workflow

### Step 1: Course Selection

```
Which course is this quiz for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option:
```

### Step 2: Chapters/Topics

```
Which chapters or topics should this quiz cover?
(e.g., "Chapters 3-4" or "Pointers, References, Memory Management")
```

### Step 3: Quiz Type

```
What type of quiz?

[1] Reading check (quick comprehension test)
[2] Practice quiz (formative, with explanations)
[3] Graded quiz (summative, answer key separate)
[4] Exam-style (comprehensive, timed)

Please select an option:
```

### Step 4: Question Count

```
How many questions?

[1] 5 questions (10-15 min)
[2] 10 questions (20-30 min)
[3] 15 questions (30-45 min)
[4] 20+ questions (exam-length)

Please select an option:
```

### Step 5: Question Mix

```
What mix of question types?

[1] Code-heavy (mostly code reading/writing)
[2] Balanced (equal code and conceptual)
[3] Concept-heavy (mostly understanding)

Please select an option:
```

### Step 6: Generate Quiz

Create the quiz following these guidelines:

1. Mix question types appropriately
2. Progress from easier to harder
3. Include code that compiles (or explicitly broken for debugging questions)
4. Provide clear point values
5. Create detailed answer key

## Question Types

### Code Tracing
"What does this code output?"
```cpp
// Complete, compilable code
```
Tests: execution understanding, mental model accuracy

### Bug Identification
"This code has a bug. Identify the issue and explain how to fix it."
```cpp
// Code with deliberate error
```
Tests: debugging skills, pattern recognition

### Code Writing
"Write a function that..."
- Clear specification
- Example inputs/outputs
Tests: implementation ability, syntax knowledge

### Fill in the Blank
"Complete this code to make it work:"
```cpp
// Code with strategic blanks
```
Tests: specific syntax, patterns

### Multiple Choice (Conceptual)
"Which statement about X is TRUE?"
Tests: understanding of concepts, common misconceptions

### Short Answer
"Explain why..."
Tests: ability to articulate understanding

### Code Comparison
"What is the difference between these two approaches?"
```cpp
// Approach A
// Approach B
```
Tests: understanding of trade-offs, alternatives

## What the Agent Does

The course-architect agent will:

**Question Design:**
- Create questions targeting specified concepts
- Ensure variety of question types
- Calibrate difficulty appropriately
- Include common misconceptions as distractors

**Code Quality:**
- All code examples compile (or deliberately don't, if testing debugging)
- Realistic scenarios
- Appropriate to course level
- Idiomatic for the language

**Answer Key:**
- Complete correct answers
- Explanation of why answer is correct
- Common wrong answers and why they're wrong
- Partial credit guidelines

## Output

Complete quiz including:
- Quiz header with instructions
- Questions organized by type/difficulty
- Code examples (all tested)
- Point values
- Answer key (separate file or section)
- Grading rubric for code questions
