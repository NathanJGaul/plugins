---
description: Generate presentation slides for a programming lecture
argument-hint: "[course] [topic] - Course and lecture topic (e.g., 'cpp-fundamentals memory-management')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task]
---

# Create Slides

Generate presentation slides for teaching programming concepts, optimized for live coding demonstrations.

## Interactive Workflow

### Step 1: Course Selection

```
Which course are these slides for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]

Please select an option:
```

### Step 2: Topic

```
What topic should the slides cover?
(e.g., "Pointers and References", "Exception Handling")
```

### Step 3: Lecture Duration

```
How long is the lecture?

[1] 30 minutes (mini-lecture)
[2] 50 minutes (standard)
[3] 75 minutes (extended)
[4] 90+ minutes (workshop-style)

Please select an option:
```

### Step 4: Slide Format

```
What format?

[1] Quarto RevealJS (.qmd) - interactive, code highlighting
[2] Markdown (.md) - portable, simple
[3] LaTeX Beamer (.tex) - academic, precise

Please select an option:
```

### Step 5: Interactive Elements

```
What interactive elements should be included?

[1] Minimal - Primarily presentation
[2] Moderate - Some live coding, 1-2 activities
[3] Heavy - Significant live coding, multiple activities

Please select an option:
```

### Step 6: Generate Slides

Create slides following the course profile and slide template:

1. Clear learning objectives
2. Progressive concept introduction
3. Live coding demonstrations with speaker notes
4. Interactive activities (think-pair-share, predict output)
5. Summary and preview of next lecture

## What the Agent Does

The course-architect agent will:

**Slide Design:**
- Structure content for progressive understanding
- Design live coding segments with clear progression
- Create interactive prediction exercises
- Include speaker notes with teaching tips

**Code Examples:**
- Ensure all code is compilable and correct
- Design incremental build-up examples
- Include deliberate errors for discussion
- Show compiler output where relevant

**Pacing:**
- Estimate time for each section
- Mark natural pause points
- Include buffer for questions
- Design activities for engagement

## Slide Structure

### Standard Lecture Structure
1. **Opening** (2-3 min)
   - Topic introduction
   - Real-world motivation

2. **Learning Objectives** (1 min)
   - 3-4 clear goals

3. **Concept Introduction** (10-15 min per concept)
   - Visual/analogy introduction
   - Formal explanation
   - Live coding demonstration
   - Interactive activity

4. **Synthesis** (5-10 min)
   - How concepts connect
   - Common patterns
   - Common mistakes

5. **Summary** (2-3 min)
   - Key takeaways
   - Preview next session
   - Questions

### Speaker Notes Include
- Exact code to type during live coding
- Timing estimates
- Common student questions and answers
- Points to emphasize
- Transition phrases

## Output

Complete slide deck including:
- Title slide with topic and objectives
- Content slides with code examples
- Live coding placeholders with speaker notes
- Interactive activity slides
- Summary and next steps
- Companion file with all complete code examples
