# Evaluate Workflow

## Purpose

Evaluate quiz answers, assign a skill level, and record results.

## Level Scale

| Level | Name              | Description                                                                 |
|-------|-------------------|-----------------------------------------------------------------------------|
| 0     | Unaware           | Has not encountered the topic                                               |
| 1     | Awareness         | Knows the topic exists, can describe it at a high level                     |
| 2     | Working Knowledge | Can use it in practice with some guidance, understands core concepts         |
| 3     | Strong            | Can apply it independently, understands trade-offs and edge cases           |
| 4     | Expert            | Deep mastery, can teach it, design systems around it, debug complex issues  |

## Steps

### 1. Review All Q&A Pairs

- Go through every question and the user's answer.
- For each answer, mentally assess: correct, partially correct, incorrect, or skipped.
- Note patterns: which subtopics were strong, which were weak.

### 2. Determine Level

- Match the overall performance to the level scale above.
- Key decision points:
  - Answered foundational questions correctly but struggled with application? → Level 1-2
  - Good on concepts and application but missed trade-offs/edge cases? → Level 2-3
  - Strong across the board including design and debugging? → Level 3-4
  - Perfect or near-perfect with nuanced, expert-level answers? → Level 4

### 3. Determine Confidence Score

- Assign a confidence score from **0.0 to 1.0** reflecting how certain you are in the level assessment.
- Higher confidence when:
  - Many questions were answered (larger sample)
  - Answers clearly cluster at one level
  - Few ambiguous or borderline responses
- Lower confidence when:
  - Many skipped questions
  - Inconsistent performance (some easy questions wrong, some hard ones right)
  - Topic has broad scope and quiz only covered part of it

### 4. Write Results

#### Update `skills.yaml`

Update or create the entry for this topic:

```yaml
topic_id:
  level: <assigned_level>
  confidence: <confidence_score>
  last_tested: <today's date YYYY-MM-DD>
```

#### Append to `learning-log.md`

Format:

```markdown
## YYYY-MM-DD

- **topic_name**: Level <old> -> <new> (confidence: <score>)
  Notes: <brief summary of performance>
```

If today's date header already exists in the file, append under it. Otherwise create a new date header.

### 5. Present Results to User

Show:
- **Assigned level**: Number and name (e.g., "Level 2 — Working Knowledge")
- **Confidence**: Score with brief explanation
- **Feedback**: 2-3 sentences of constructive feedback
- **Strong areas**: What they demonstrated well
- **Areas to improve**: Specific subtopics or concepts to focus on

Then ask if the user would like a learning plan to improve. If yes, follow `prompts/plan.md` to generate and save it to `plans/`.
