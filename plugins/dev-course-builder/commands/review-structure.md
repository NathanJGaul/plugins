---
description: Analyze course structure, organization, and learning progression
argument-hint: "[course] - Course to analyze (e.g., 'cpp-fundamentals')"
allowed-tools: [Read, Glob, Grep, AskUserQuestion, Task]
---

# Review Structure

Focused analysis of course architecture, organization, dependencies, and learning progression.

## Interactive Workflow

### Step 1: Course Selection

```
Which course structure would you like to analyze?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory path

Please select an option:
```

### Step 2: Analysis Focus

```
What aspects of structure should I focus on?

[1] Full structural analysis (all aspects)
[2] Learning objectives alignment
[3] Topic sequencing and dependencies
[4] Module organization and balance
[5] Assessment-to-content mapping

Please select an option:
```

### Step 3: Visualization

```
Would you like structural visualizations?

[1] Yes - include dependency diagrams and maps
[2] No - text-based analysis only

Please select an option:
```

### Step 4: Generate Analysis

The course-reviewer agent will analyze the structure and provide a detailed report.

## What Gets Analyzed

### Learning Path Architecture
- Learning objectives hierarchy
- Objective-to-content mapping
- Gaps in objective coverage
- Redundant or overlapping objectives

### Topic Dependencies
- Prerequisite relationships
- Concept dependency chains
- Forward reference violations
- Missing foundational content

### Module Organization
- Logical grouping of topics
- Balance of content across modules
- Granularity consistency
- Section length uniformity

### Progression Analysis
- Complexity progression curve
- Scaffolding adequacy
- Cognitive load distribution
- Review and reinforcement points

### Assessment Alignment
- Assessment-to-objective mapping
- Practice distribution
- Difficulty progression
- Coverage completeness

## What the Agent Does

The course-reviewer agent will:

**Map the Structure:**
- Identify all course components
- Extract learning objectives
- Map content relationships
- Build dependency graph

**Analyze Flow:**
- Trace learning paths
- Identify bottlenecks
- Find circular dependencies
- Spot missing links

**Evaluate Balance:**
- Compare module sizes
- Check depth consistency
- Assess time distribution
- Review practice allocation

**Generate Insights:**
- Structural recommendations
- Reordering suggestions
- Gap identification
- Optimization opportunities

## Output

Comprehensive structural analysis:

```
## Course Structure Analysis: [Course Name]

### Structure Overview
- Total modules: X
- Total chapters: X
- Total exercises: X
- Total labs: X
- Total assessments: X

### Learning Objectives Analysis

#### Objectives Summary
| Module | Objectives | Coverage | Assessment |
|--------|------------|----------|------------|

#### Objective Mapping
- Fully covered objectives: X
- Partially covered objectives: X
- Uncovered objectives: X

#### Gap Analysis
[List of objectives not adequately addressed]

### Dependency Analysis

#### Prerequisite Chain
```
Module 1 → Module 2 → Module 3
              ↓
           Module 4
```

#### Dependency Issues
- Forward references found: [list]
- Missing prerequisites: [list]
- Circular dependencies: [list if any]

### Module Balance Analysis

| Module | Content Units | Exercises | Labs | Est. Time |
|--------|---------------|-----------|------|-----------|

#### Balance Issues
- Overloaded modules: [list]
- Underweight modules: [list]
- Imbalanced sections: [list]

### Progression Analysis

#### Complexity Curve
[Description of how complexity builds]

#### Progression Issues
- Jump too large: [locations]
- Plateau periods: [locations]
- Missing scaffolding: [locations]

### Assessment Alignment

#### Assessment Coverage
| Objective | Assessment Type | Location |
|-----------|-----------------|----------|

#### Alignment Issues
- Untested objectives: [list]
- Over-tested areas: [list]
- Missing practice: [list]

### Structural Recommendations

#### Critical (Structural Integrity)
1. [Recommendation with rationale]

#### Important (Learning Effectiveness)
1. [Recommendation with rationale]

#### Enhancement (Optimization)
1. [Recommendation with rationale]

### Proposed Restructuring
[If applicable, suggest reordering or reorganization]

### Visualization
[Dependency diagram, if requested]
```

## Usage Notes

- Structure analysis helps identify course-wide issues
- Use before major revisions to plan changes
- Combine with content review for full picture
- Re-run after restructuring to verify improvements
- Useful for new course planning as well as review
