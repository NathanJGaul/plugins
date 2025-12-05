---
description: Review and provide feedback on course content
argument-hint: "[file-path] - Path to content file to review"
allowed-tools: [Read, Glob, Grep, AskUserQuestion, Task]
---

# Review Content

Comprehensive review of course content (chapters, exercises, labs, etc.) for accuracy, pedagogy, and quality.

## Interactive Workflow

### Step 1: Content Type

```
What type of content are you reviewing?

[1] Chapter/Tutorial
[2] Exercise/Problem
[3] Lab/Workshop
[4] Slides/Presentation
[5] Quiz/Assessment
[6] Project specification

Please select an option:
```

### Step 2: Course Context

```
Which course is this content for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option:
```

### Step 3: Content Location

```
Where is the content to review?
(Provide file path or paste content)
```

### Step 4: Review Focus

```
What aspects should I focus on?

[1] Full review (all aspects)
[2] Technical accuracy (code correctness, factual accuracy)
[3] Pedagogical quality (explanation clarity, progression)
[4] Code quality (style, idioms, best practices)
[5] Alignment with course (audience, prerequisites, style)

Please select an option:
```

### Step 5: Generate Review

The agent will analyze the content and provide detailed feedback.

## Review Dimensions

### 1. Technical Accuracy
- Does all code compile and run correctly?
- Are the explanations factually correct?
- Are there any misleading simplifications?
- Are error messages accurate?

### 2. Code Quality
- Does code follow language idioms?
- Is the style consistent with course standards?
- Are there opportunities for cleaner code?
- Is error handling appropriate?

### 3. Pedagogical Effectiveness
- Is the progression logical?
- Are explanations clear for the target audience?
- Are examples appropriate complexity?
- Is there enough scaffolding?

### 4. Completeness
- Are all concepts covered adequately?
- Are there gaps in the explanation?
- Are edge cases addressed?
- Are common mistakes discussed?

### 5. Engagement
- Will students find this interesting?
- Are examples motivating and relevant?
- Is the tone appropriate?
- Are there opportunities for active learning?

### 6. Course Alignment
- Does it match the target audience level?
- Is it consistent with course philosophy?
- Does it use the specified tools and libraries?
- Does it build on prerequisites appropriately?

## What the Agent Does

The course-architect agent will:

**Analysis:**
- Read and analyze the content thoroughly
- Test any code examples
- Compare against course profile standards
- Check for common issues

**Feedback:**
- Provide specific, actionable feedback
- Highlight strengths as well as improvements
- Prioritize feedback by importance
- Suggest concrete fixes

## Output

Comprehensive review report including:

```
## Review Summary
- Overall assessment
- Key strengths
- Priority improvements

## Technical Accuracy
[Specific findings]

## Code Quality
[Specific findings]

## Pedagogical Effectiveness
[Specific findings]

## Completeness
[Specific findings]

## Engagement
[Specific findings]

## Course Alignment
[Specific findings]

## Recommended Changes
1. [Priority 1 change]
2. [Priority 2 change]
...

## Optional Enhancements
- [Nice-to-have improvement 1]
- [Nice-to-have improvement 2]
```
