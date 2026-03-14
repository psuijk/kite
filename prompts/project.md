# Project Workflow

## Purpose

Generate a hands-on engineering project that exercises a specific topic.

## Steps

### 1. Load Context

- Read the topic's node from `knowledge-graph.yml` — note `name`, `description`, `children`, `difficulty`, `depends_on`.
- Read current skill level from `skills.yaml` (default to 0).

### 2. Calibrate the Project

- **Match the level**: The project should be challenging but achievable for someone at the user's current skill level.
  - Level 0-1: Guided tutorial-style project with clear steps.
  - Level 2: Semi-guided project with room for decisions.
  - Level 3: Open-ended project with requirements but no hand-holding.
  - Level 4: Advanced project pushing boundaries (optimize, scale, innovate).
- **Completable in 2-4 hours** of focused work.
- **Must produce something tangible**: working code, a running system, a demo, a tool.

### 3. Generate the Project

Use this structure:

```markdown
# Project: [Project Title]

**Topic**: [Topic name]
**Difficulty**: [Calibrated to user's level]
**Estimated time**: 2-4 hours

## Objective

[1-2 sentences describing what the user will build and why it's valuable]

## Requirements

1. [Specific, testable requirement]
2. [Another requirement]
3. ...

## Implementation Guide

### Step 1: [Setup / Foundation]
[What to do and key decisions to make]

### Step 2: [Core Implementation]
[Main logic and concepts to apply]

### Step 3: [Integration / Polish]
[Connecting pieces, error handling, testing]

## Stretch Goals

- [Optional challenge 1]
- [Optional challenge 2]
- [Optional challenge 3]

## Success Criteria

- [How to know the project is complete]
- [What to test or demonstrate]
```

### 4. Guidelines

- The project should exercise the topic's children/subtopics naturally.
- Prefer projects that are practical and could be part of a real system.
- Include enough detail to get started but leave room for creative decisions.
- Stretch goals should push toward the next skill level.
