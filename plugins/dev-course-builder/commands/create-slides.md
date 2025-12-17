---
description: Generate Slidev presentation slides for YouTube videos and online course content
argument-hint: "[course] [topic] - Course and lecture topic (e.g., 'cpp-fundamentals memory-management')"
allowed-tools: [Read, Write, Glob, Grep, AskUserQuestion, Task, Skill]
---

# Create Slides

Generate Slidev presentation slides optimized for video tutorials, YouTube content, and online courses. Creates a single `.md` file with comprehensive presenter notes for video recording.

## Prerequisites

- Course content should exist (chapters, exercises, or labs to transform)
- Course profile should be configured for audience context

## Interactive Workflow

### Step 1: Course Selection

```
Which course are these slides for?

[1] C++ Fundamentals (Junior Developers)
[2] [Other configured courses...]
[3] Specify course directory

Please select an option:
```

### Step 2: Source Content

```
What content should be transformed into video slides?

[1] Existing chapter (provide path)
[2] Existing lab or exercise (provide path)
[3] New topic (describe what to cover)
[4] Module overview (summarize multiple chapters)

Please select an option:
```

### Step 3: Video Length

```
Target video length?

[1] Short (5-7 minutes) - Single concept deep dive
[2] Standard (10-15 minutes) - Complete topic coverage
[3] Long (20-25 minutes) - Multi-concept or workshop

Please select an option:
```

### Step 4: Video Style

```
What style of video?

[1] Tutorial - Step-by-step teaching
[2] Explainer - Concept explanation with examples
[3] Code Walkthrough - Focus on code analysis
[4] Comparison - Contrast approaches/patterns
[5] Quick Tips - Fast-paced practical advice

Please select an option:
```

### Step 5: Generate Slides

The slides-architect agent creates a complete Slidev presentation.

## What Gets Created

### Single `.md` File

A complete Slidev presentation file containing:

```markdown
---
theme: default
title: "Video Title"
author: Course Name
transition: slide-left
highlighter: shiki
mdc: true
aspectRatio: 16/9
---

# Title Slide
...

---
# Content Slides
...

<!--
Presenter notes with visual cues
-->
```

### Slide Types Included

| Type | Purpose | Notes |
|------|---------|-------|
| Hook | Engage viewers | Question or problem statement |
| Concept | Teach ideas | Progressive reveals |
| Code | Show examples | Click-through highlighting |
| Comparison | Contrast options | Two-column layout |
| Diagram | Visualize | Mermaid flowcharts |
| Summary | Reinforce | Key takeaways |
| CTA | Next steps | Subscribe, practice, next video |

### Presenter Notes Include

Every slide has comprehensive notes:
- Main talking points
- Click-by-click explanations
- Visual cues: `[SHOW CODE]`, `[PAUSE]`, `[TRANSITION]`
- Natural, conversational phrasing
- Questions to engage viewers

## Slidev Features Used

### Layouts
- `default` - Standard content
- `center` - Impact statements
- `two-cols` - Code + explanation
- `section` - Topic dividers
- `image-right/left` - Visuals
- `fact` - Statistics
- `quote` - Expert quotes

### Code Features
- Progressive line highlighting `{1|2-3|all}`
- Syntax highlighting (Shiki)
- Line numbers when helpful
- Monaco for interactive demos

### Animations
- `v-click` - Progressive reveals
- `v-clicks` - List animations
- Smooth transitions

### Diagrams
- Mermaid flowcharts
- Sequence diagrams
- Class diagrams

## Video Structure

### Standard 10-15 Minute Video

| Section | Duration | Slides | Purpose |
|---------|----------|--------|---------|
| Hook | 30-60s | 1-2 | Grab attention |
| Overview | 30s | 1 | What we'll learn |
| Core Content | 8-12min | 10-15 | Main teaching |
| Summary | 1-2min | 2-3 | Key takeaways |
| CTA | 30s | 1 | Next steps |

### Slide Pacing

- **1-2 minutes per slide** average
- **2-4 clicks per slide** for reveals
- **One concept per slide** maximum

## Output Format

### File Naming
```
{topic}-slides.md
```

Example: `smart-pointers-slides.md`

### Frontmatter
```yaml
---
theme: default
title: "Smart Pointers in Modern C++"
info: |
  ## C++ Fundamentals - Module 6
  Learn automatic memory management with smart pointers
author: C++ Fundamentals Course
transition: slide-left
highlighter: shiki
drawings:
  persist: false
mdc: true
aspectRatio: 16/9
canvasWidth: 980
fonts:
  sans: Inter
  mono: Fira Code
---
```

## Example Output Structure

```markdown
---
[frontmatter]
---

# Why Your Code Keeps Crashing
## Smart Pointers to the Rescue

<!--
[HOOK] Start with the relatable problem...
-->

---
layout: section
---

# Part 1: The Problem

<!--
[TRANSITION] Let's understand what we're solving...
-->

---
layout: two-cols
---

# Manual Memory Management

<v-clicks>

- You allocate with `new`
- You must free with `delete`
- Miss it? Memory leak
- Double free? Crash

</v-clicks>

::right::

```cpp {1|3|5|all}
int* ptr = new int(42);

// ... use ptr ...

delete ptr;  // Don't forget!
```

<!--
[click] First, we allocate...
[click] Then we use the memory...
[click] Finally, we must clean up...
[click] Full picture - see the pattern?

[VISUAL CUE] Every new needs a delete
-->

---
layout: center
class: text-center
---

# Key Takeaways

<v-clicks>

1. **unique_ptr** for single ownership
2. **shared_ptr** for shared ownership
3. **Never use raw new**

</v-clicks>

<!--
[click] Most common case...
[click] When you need to share...
[click] The golden rule!

[PAUSE] Let these sink in
-->

---
layout: end
---

# Practice Time!

Convert your raw pointers to smart pointers

**Next Video:** Move Semantics Deep Dive

<!--
Clear call to action.
Mention next video for retention.
Thank viewers!
-->
```

## Integration with Course Content

### From Chapters
- Extract core concepts
- Select best code examples
- Condense explanations for video
- Add visual elements

### From Labs
- Focus on guided portion
- Create follow-along format
- Include checkpoint moments
- Add practice prompts

### From Exercises
- Present problem clearly
- Build solution step-by-step
- Show common mistakes
- Reveal solution progressively

## Quality Checklist

Before delivering slides:
- [ ] Hook engages in first 30 seconds
- [ ] One main concept per slide
- [ ] All code has progressive reveals
- [ ] Presenter notes are conversational
- [ ] Visual cues mark all animations
- [ ] Summary reinforces key points
- [ ] Call to action is clear
- [ ] Total time is 10-15 minutes
- [ ] Slidev renders correctly

## Running the Presentation

```bash
# Install Slidev (if needed)
npm install -g @slidev/cli

# Run presentation
slidev {filename}.md

# Export to PDF
slidev export {filename}.md

# Record presentation
slidev {filename}.md --record
```

## Tips for Recording

1. **Practice the flow** - Run through with presenter mode (`p` key)
2. **Check notes** - Ensure all clicks have explanations
3. **Test code** - Verify all examples work
4. **Time yourself** - Aim for target duration
5. **Record in chunks** - Easier to edit mistakes
