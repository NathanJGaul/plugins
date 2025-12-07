---
description: Comprehensive review of an entire course for quality, consistency, and completeness
argument-hint: "[course] - Course to review (e.g., 'cpp-fundamentals')"
allowed-tools: [Read, Glob, Grep, AskUserQuestion, Task]
---

# Review Course

Comprehensive, course-wide review examining consistency, completeness, structure, and quality across all course materials.

## Interactive Workflow

### Step 1: Course Selection

```
Which course would you like to review?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 2: Review Scope

```
What scope of review would you like?

[1] Full course review (all aspects, all materials)
[2] Structure and organization only
[3] Content consistency only
[4] Learning objectives alignment
[5] Custom scope

Please select an option:
```

### Step 3: Review Depth

```
How thorough should the review be?

[1] Quick scan (identify major issues, 15-30 min)
[2] Standard review (thorough analysis, 1-2 hours)
[3] Deep audit (comprehensive evaluation, 2-4+ hours)

Please select an option:
```

### Step 4: Focus Areas (Optional)

```
Are there specific areas of concern?

[1] No specific concerns - review everything
[2] Code correctness is a priority
[3] Pedagogical quality is a priority
[4] Consistency is a priority
[5] Completeness is a priority

Please select an option:
```

### Step 5: Generate Review

The course-reviewer agent will analyze the entire course and provide a comprehensive report.

## What Gets Reviewed

### Course Architecture
- Learning objectives and their coverage
- Prerequisite chain and dependencies
- Topic sequencing and logical flow
- Scope appropriateness for duration

### Content Quality
- Code correctness in all examples
- Technical accuracy of explanations
- Pedagogical effectiveness
- Audience appropriateness

### Consistency
- Terminology usage across all materials
- Code style uniformity
- Formatting and structure patterns
- Writing voice and tone

### Completeness
- Coverage of all stated objectives
- Gap identification
- Practice opportunity sufficiency
- Assessment alignment

### Cross-References
- Internal link validity
- Prerequisite reference accuracy
- Callback correctness
- Continuation references

## What the Agent Does

The course-reviewer agent will:

**Discovery:**
- Identify all course materials (chapters, exercises, labs, etc.)
- Load the course profile to understand standards
- Map the course structure and dependencies

**Analysis:**
- Review each piece of content systematically
- Check code examples for correctness
- Evaluate explanations for clarity and accuracy
- Assess consistency across materials
- Identify gaps and redundancies

**Cross-Referencing:**
- Track terminology usage
- Verify internal references
- Check prerequisite assumptions
- Validate learning objective coverage

**Synthesis:**
- Compile findings by category and severity
- Prioritize recommendations
- Provide actionable improvement steps
- Generate comprehensive report

## Output

Comprehensive course review report:

```
## Course Review Report: [Course Name]

### Executive Summary
- Overall course quality assessment
- Key strengths (what works well)
- Priority action items (what needs attention)

### Course Architecture Assessment
- Learning objectives evaluation
- Structure and sequencing analysis
- Scope and pacing assessment

### Content Quality Assessment
- Code correctness findings
- Technical accuracy findings
- Pedagogical quality findings

### Consistency Assessment
- Terminology consistency
- Style consistency
- Structural consistency

### Completeness Assessment
- Coverage analysis
- Gap identification
- Practice sufficiency

### Detailed Findings

#### Critical Issues (Must Fix)
| Location | Issue | Recommendation |
|----------|-------|----------------|

#### Major Issues (Should Fix)
| Location | Issue | Recommendation |
|----------|-------|----------------|

#### Minor Issues (Nice to Fix)
| Location | Issue | Recommendation |
|----------|-------|----------------|

### Enhancement Opportunities
- [Suggestion 1]
- [Suggestion 2]

### Recommended Action Plan
1. Immediate actions (address critical issues)
2. Short-term improvements (address major issues)
3. Long-term enhancements (continuous improvement)

### Appendix: Metrics
- Total modules reviewed: X
- Code examples checked: X
- Issues found by category
- Quality scores by dimension
```

## Usage Notes

- For best results, ensure all course materials are accessible
- Review may take significant time for large courses
- The agent will ask clarifying questions if needed
- Results should be saved for tracking improvements over time
- Re-run after making changes to verify fixes
