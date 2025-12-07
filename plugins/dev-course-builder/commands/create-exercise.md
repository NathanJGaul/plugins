---
description: Create a focused coding exercise for practice or assessment
argument-hint: "[course] [concept] - Course and concept to practice (e.g., 'cpp-fundamentals recursion')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task]
---

# Create Exercise

Generate a standalone coding exercise with clear specifications, starter code, test cases, and solution.

## Interactive Workflow

### Step 1: Course Selection

```
Which course is this exercise for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option:
```

### Step 2: Exercise Type

```
What type of exercise?

[1] Practice Exercise (with hints and solution visible)
[2] Assignment (solution hidden, for submission)
[3] Assessment Question (timed, minimal hints)

Please select an option:
```

### Step 3: Concepts to Practice

```
What concepts should this exercise focus on?
(e.g., "pointers", "recursion", "standard library algorithms")
```

### Step 4: Difficulty Level

```
What difficulty level?

[1] Beginner - Reinforce basic understanding
[2] Intermediate - Apply concepts in new context
[3] Advanced - Combine multiple concepts or optimize
[4] Challenge - Push beyond the course material

Please select an option:
```

### Step 5: Time Estimate

```
How long should students spend on this exercise?

[1] 10-15 minutes (quick practice)
[2] 20-30 minutes (standard exercise)
[3] 45-60 minutes (substantial problem)
[4] 90+ minutes (mini-project)

Please select an option:
```

### Step 6: Generate Exercise

Create the exercise following the exercise template:

1. Clear problem statement
2. Specific requirements
3. Starter code (appropriate to difficulty)
4. Test cases for validation
5. Hints (if practice exercise)
6. Complete solution with explanation

## What the Agent Does

The course-architect agent will:

**Problem Design:**
- Create a realistic, engaging problem
- Ensure requirements are clear and testable
- Design appropriate starter code scaffolding
- Write comprehensive test cases

**Difficulty Calibration:**
- Match complexity to specified level
- Ensure solvable with taught concepts
- Include appropriate hints for the level
- Design solution that demonstrates best practices

**Quality Assurance:**
- All code compiles and runs
- Test cases are comprehensive
- Solution is idiomatic and well-explained
- Time estimate is realistic

## Output

A complete exercise document including:
- Problem statement
- Requirements list
- Starter code
- Test cases
- Hints (for practice exercises)
- Solution with explanation
- Extension challenges (optional)
