---
description: Audit code examples for correctness, best practices, and consistency
argument-hint: "[course] [scope] - Course and optional scope (e.g., 'cpp-fundamentals chapter-5')"
allowed-tools: [Read, Glob, Grep, Bash, AskUserQuestion, Task]
---

# Review Code Examples

Systematic audit of code examples across course materials for correctness, style, best practices, and consistency.

## Interactive Workflow

### Step 1: Course Selection

```
Which course's code examples should be reviewed?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 2: Scope Selection

```
What scope of code review?

[1] All code examples in the course
[2] Specific module or chapter
[3] Specific file or content piece
[4] Only code marked as "working examples"
[5] Only code marked as "error examples"

Please select an option:
```

### Step 3: Review Depth

```
How thorough should the code review be?

[1] Compilation check only (verify code compiles)
[2] Execution check (verify output matches stated)
[3] Full review (compilation, execution, style, best practices)
[4] Style and idioms only (skip compilation)

Please select an option:
```

### Step 4: Verification Method

```
How should code be verified?

[1] Manual analysis (trace through code mentally)
[2] Actual compilation and execution (if toolchain available)
[3] Hybrid (compile what's possible, analyze the rest)

Please select an option:
```

### Step 5: Generate Code Audit

The course-reviewer agent will systematically review all code examples.

## What Gets Reviewed

### Correctness
- Does code compile without errors?
- Does code produce stated output?
- Are there logical bugs?
- Do error examples actually fail?
- Are fixes correct and complete?

### Style & Idioms
- Language-specific conventions followed?
- Naming conventions consistent?
- Code formatting uniform?
- Modern idioms used appropriately?
- Comments helpful and accurate?

### Best Practices
- Proper error handling?
- Resource management correct?
- Security considerations addressed?
- No deprecated features?
- Performance reasonable?

### Presentation
- Syntax highlighting correct?
- Line numbers useful (if present)?
- Output formatting matches actual?
- Error messages realistic?
- Code properly excerpted?

### Consistency
- Style matches course standards?
- Patterns used uniformly?
- Naming aligns across examples?
- Complexity level appropriate?
- Approach consistent with course philosophy?

## What the Agent Does

The course-reviewer agent will:

**Discovery:**
- Find all code blocks in course materials
- Categorize by type (working, error, partial)
- Identify the language and context
- Note stated expectations (output, errors)

**Analysis:**
- Check syntax validity
- Trace through logic
- Verify expected behavior
- Compare against course standards
- Identify style issues

**Verification (if requested):**
- Compile code examples
- Run and capture output
- Compare to stated output
- Test error examples fail correctly

**Reporting:**
- Categorize issues by severity
- Provide exact locations
- Suggest specific fixes
- Track patterns across examples

## Output

Comprehensive code audit report:

```
## Code Examples Audit: [Course Name]

### Audit Summary
- Total code blocks found: X
- Working examples: X
- Error examples: X
- Partial/snippet examples: X
- Examples verified: X

### Overall Assessment
[Summary of code quality across the course]

### Compilation Results
| Example | Location | Status | Issue |
|---------|----------|--------|-------|

### Output Verification
| Example | Location | Expected | Actual | Status |
|---------|----------|----------|--------|--------|

### Critical Issues (Code Won't Compile/Run)

#### Issue C1: [File:Line]
**Code:**
```[lang]
// The problematic code
```
**Problem:** [Description]
**Fix:**
```[lang]
// The corrected code
```

### Major Issues (Logic Errors or Wrong Output)

#### Issue M1: [File:Line]
**Code:**
```[lang]
// The problematic code
```
**Problem:** [Description]
**Expected:** [What should happen]
**Actual:** [What happens]
**Fix:** [How to fix]

### Style Issues

| Location | Issue | Current | Recommended |
|----------|-------|---------|-------------|

### Best Practice Violations

| Location | Pattern | Issue | Recommendation |
|----------|---------|-------|----------------|

### Consistency Issues

| Issue | Locations | Recommendation |
|-------|-----------|----------------|

### Pattern Analysis
- Common issues found: [list]
- Style drift detected: [yes/no]
- Naming consistency: [assessment]

### Recommendations

#### Immediate (Critical Fixes)
1. [Specific fix with location]

#### Important (Quality Issues)
1. [Improvement with approach]

#### Style Guide Updates
1. [If patterns suggest guide needs updating]

### Code Metrics
- Examples by complexity: [breakdown]
- Average example length: X lines
- Languages used: [list]
- Error example ratio: X%
```

## Usage Notes

- Actual compilation requires appropriate toolchain
- Large courses may take significant time
- Run after adding new content
- Track trends across reviews
- Consider running before course launches
- Use alongside full course review for complete picture
