# Learning Plan Workflow

## Purpose

Generate a structured 1-week study plan for a specific topic.

## Steps

### 1. Load Context

- Read the topic's node from `knowledge-graph.yml` — note `name`, `description`, `children`, `difficulty`, `depends_on`.
- Read current skill level from `skills.yaml` (default to 0).
- Check dependency levels to understand prerequisite readiness.

### 2. Calibrate the Plan

- **Don't repeat what's known**: If the user is at level 2, don't spend days on basics.
- **Start from current level**: Build upward from where they are.
- **Target level**: Aim for current_level + 1 (or +2 if current level is 0-1).
- **Respect difficulty**: Higher difficulty topics need more time on fundamentals.

### 3. Generate the Plan

Create a 7-day plan with this structure:

```markdown
# 1-Week Learning Plan: [Topic Name]

**Current level**: [level] — [level name]
**Target level**: [target] — [target name]
**Prerequisite check**: [list any weak dependencies to shore up]

## Day 1: [Theme]
- **Goal**: [What to achieve]
- **Study**: [Concepts to cover]
- **Practice**: [Exercises or activities]
- **Time estimate**: [e.g., 1-2 hours]

## Day 2: [Theme]
...

## Day 4 (Mid-week Checkpoint)
- **Review**: [What to review]
- **Self-check**: [Questions to verify understanding]

## Day 7 (End-of-week Milestone)
- **Deliverable**: [Something tangible to produce]
- **Self-assessment**: [How to know if target level was reached]
```

### 4. Save the Plan

- Write the generated plan to `plans/<topic_id>-<YYYY-MM-DD>.md`.
- Append to `learning-log.md`: "Created learning plan for [topic name]" under today's date.

### 5. Guidelines

- Each day should be achievable in 1-2 hours of focused study.
- Include a mix of reading, coding, and reflection.
- Suggest specific, actionable activities (not vague "study X").
- The mid-week checkpoint should help catch gaps early.
- The end-of-week milestone should produce something tangible.
- Mention when a quiz would be appropriate (typically at the end).
