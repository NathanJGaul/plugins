---
description: Generate actionable improvement suggestions for course content
argument-hint: "[course] [focus] - Course and optional focus area (e.g., 'cpp-fundamentals engagement')"
allowed-tools: [Read, Glob, Grep, AskUserQuestion, Task]
---

# Suggest Improvements

Generate prioritized, actionable suggestions to enhance course quality, engagement, and learning outcomes.

## Interactive Workflow

### Step 1: Course or Content Selection

```
What would you like improvement suggestions for?

[1] Entire course
[2] Specific module or chapter
[3] Specific content file
[4] Specific content type (all exercises, all labs, etc.)

Please select an option:
```

### Step 2: Course Context (if not specified)

```
Which course?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 3: Improvement Focus

```
What aspect should improvements focus on?

[1] All aspects - comprehensive suggestions
[2] Engagement and motivation
[3] Clarity and understanding
[4] Practice and reinforcement
[5] Real-world relevance
[6] Assessment effectiveness
[7] Accessibility and inclusivity

Please select an option:
```

### Step 4: Suggestion Scope

```
What level of suggestions would you like?

[1] Quick wins only (low effort, high impact)
[2] All practical improvements
[3] Ambitious enhancements (including major additions)
[4] Innovation opportunities (creative new approaches)

Please select an option:
```

### Step 5: Generate Suggestions

The course-reviewer agent will analyze content and generate improvement suggestions.

## Categories of Improvements

### Engagement Enhancements
- More compelling examples
- Real-world connections
- Interactive elements
- Storytelling opportunities
- Motivational hooks

### Clarity Improvements
- Clearer explanations
- Better analogies
- Additional visualizations
- Simplified language
- More scaffolding

### Practice Additions
- More exercises
- Different exercise types
- Challenge problems
- Self-assessment opportunities
- Extension activities

### Relevance Connections
- Industry examples
- Career connections
- Current technology links
- Practical applications
- Professional context

### Assessment Refinements
- Better test coverage
- More question types
- Clearer rubrics
- Formative feedback
- Self-check additions

### Accessibility Improvements
- Clearer language
- Alternative explanations
- Multiple representations
- Prerequisite support
- Learning path options

## What the Agent Does

The course-reviewer agent will:

**Analyze Current State:**
- Review existing content thoroughly
- Identify strengths to build on
- Spot gaps and weaknesses
- Understand course philosophy

**Generate Ideas:**
- Brainstorm improvements per category
- Consider different learning styles
- Think about student experience
- Look for opportunities

**Prioritize:**
- Assess impact vs. effort
- Consider dependencies
- Identify quick wins
- Flag transformative opportunities

**Make Actionable:**
- Provide specific suggestions
- Include implementation guidance
- Estimate effort levels
- Suggest sequencing

## Output

Prioritized improvement suggestions:

```
## Improvement Suggestions: [Course/Content Name]

### Current State Assessment
[Brief summary of content quality and areas of strength]

### High-Impact Quick Wins
Easy improvements that significantly enhance learning:

#### 1. [Suggestion Title]
**Location:** [Where to apply]
**Current:** [What exists now]
**Suggested:** [What to add/change]
**Impact:** [Why this helps learners]
**Effort:** Low (X hours)

#### 2. [Suggestion Title]
...

### Substantial Improvements
Medium-effort changes with significant payoff:

#### 1. [Suggestion Title]
**Location:** [Where to apply]
**Problem:** [What issue this addresses]
**Suggested Change:**
[Detailed description of the improvement]
**Implementation Approach:**
1. [Step 1]
2. [Step 2]
**Expected Outcome:** [How this improves learning]
**Effort:** Medium (X hours/days)

#### 2. [Suggestion Title]
...

### Major Enhancements
Significant additions or overhauls:

#### 1. [Suggestion Title]
**Scope:** [What this involves]
**Rationale:** [Why this matters]
**Description:**
[Full description of the enhancement]
**Prerequisites:** [What needs to happen first]
**Effort:** High (X days/weeks)
**Priority:** [When to tackle this]

#### 2. [Suggestion Title]
...

### Innovation Opportunities
Creative ideas for standing out:

#### 1. [Idea Title]
[Description of innovative approach]
**Why it's different:** [What makes this special]
**Challenges:** [What makes it hard]
**Potential Impact:** [What success looks like]

### By Category

#### Engagement
- [ ] [Suggestion 1]
- [ ] [Suggestion 2]

#### Clarity
- [ ] [Suggestion 1]
- [ ] [Suggestion 2]

#### Practice
- [ ] [Suggestion 1]
- [ ] [Suggestion 2]

#### Relevance
- [ ] [Suggestion 1]
- [ ] [Suggestion 2]

### Implementation Roadmap

#### Phase 1: Quick Wins (This Week)
1. [Improvement]
2. [Improvement]

#### Phase 2: Core Improvements (This Month)
1. [Improvement]
2. [Improvement]

#### Phase 3: Major Enhancements (This Quarter)
1. [Enhancement]
2. [Enhancement]

### Metrics to Track
- [Metric 1]: [How to measure improvement]
- [Metric 2]: [How to measure improvement]
```

## Example Suggestions by Focus

### Engagement Focus
- Add "Why This Matters" sections
- Include industry anecdotes
- Create mini-challenges
- Add "Did You Know" facts
- Gamification elements

### Clarity Focus
- Add more visual diagrams
- Include analogies for abstract concepts
- Provide multiple explanation approaches
- Add step-by-step breakdowns
- Include "Common Confusion" callouts

### Practice Focus
- Add warm-up exercises
- Create practice problem sets
- Include debugging challenges
- Add code review exercises
- Create "what's wrong" problems

### Relevance Focus
- Link to real codebases
- Reference industry tools
- Add career context
- Include interview question notes
- Connect to open source projects

## Usage Notes

- Review suggestions critically before implementing
- Not all suggestions will fit every course
- Prioritize based on your specific context
- Track which suggestions were implemented
- Re-run periodically for fresh ideas
