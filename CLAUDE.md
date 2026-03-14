# Personal Learning System

This repo is a personal learning system. It uses Claude Code as the interface — no CLI tools, no Python scripts, no dependencies. Just open Claude Code in this repo and talk naturally.

## First-Time Setup

If `knowledge-graph.yml` does not exist, this repo has not been initialized yet.
Run the initialization workflow before anything else:

1. Follow `prompts/init.md` to interview the user and build their knowledge graph.
2. All other workflows require `knowledge-graph.yml` to exist first.

## Files

| File | Purpose |
|------|---------|
| `knowledge-graph.yml` | Learning ontology — all topics, their relationships, priorities, and difficulty |
| `skills.yaml` | Your skill levels per topic (created on first assessment) |
| `learning-log.md` | Append-only log of all skill level changes (created on first change) |
| `plans/` | Saved learning plans as markdown files (e.g., `plans/topic-2026-03-14.md`) |
| `prompts/*.md` | Detailed instructions for each workflow |
| `prompts/discussion-extract.md` | Prompt to copy-paste into other LLM chats to extract learnings |

## Skill Levels

| Level | Name | Description |
|-------|------|-------------|
| 0 | Unaware | Has not encountered the topic |
| 1 | Awareness | Knows the topic exists, can describe it at a high level |
| 2 | Working Knowledge | Can use it in practice with some guidance, understands core concepts |
| 3 | Strong | Can apply it independently, understands trade-offs and edge cases |
| 4 | Expert | Deep mastery, can teach it, design systems around it, debug complex issues |

## Workflows

Respond to natural language requests by matching to these workflows.

### Status

**Triggers**: "status", "how am I doing", "show my progress", "where do I stand"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Display a summary table of all topics with columns: Topic, Level, Confidence, Last Tested.
3. Group by priority (P0 first, then P1, etc.).
4. Show aggregate stats: total topics, tested count, average level, topics at each level.
5. If any plans exist in `plans/`, show the most recent plan with its topic and date.

### Next Topic

**Triggers**: "what should I learn next", "recommend", "what's next", "suggest a topic"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Follow `prompts/next-topic.md` to score every topic and recommend the top 3-5.

### Quiz

**Triggers**: "quiz me on [topic]", "test me on [topic]", "assess [topic]", "start [topic]"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Look up the topic node (match by id or name, case-insensitive).
3. Follow `prompts/quiz.md` to generate and administer the quiz.
4. After all questions, follow `prompts/evaluate.md` to assess, record results, and present feedback.

### Test (Re-quiz)

**Triggers**: "test me on [topic] again", "re-test [topic]", "retest"

Same as Quiz, but:
- Note the previous level and confidence before starting.
- After evaluation, show a comparison: "Level X -> Y, Confidence X -> Y".

### Plan

**Triggers**: "learning plan for [topic]", "plan for [topic]", "how should I study [topic]"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Follow `prompts/plan.md` to generate a 1-week study plan.
3. Save the plan to `plans/<topic_id>-<YYYY-MM-DD>.md`.
4. Append an entry to `learning-log.md`: "Created learning plan for [topic]".

### Project

**Triggers**: "project for [topic]", "give me a project", "hands-on [topic]", "build something for [topic]"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Follow `prompts/project.md` to generate a hands-on project.

### Expand

**Triggers**: "expand [topic]", "go deeper on [topic]", "add subtopics to [topic]"

1. Read `knowledge-graph.yml`.
2. Follow `prompts/expand.md` to propose subtopics, confirm with user, and edit `knowledge-graph.yml`.

### Import Discussion Extract

**Triggers**: user pastes a YAML block containing `# DISCUSSION EXTRACT`, or says "import", "import discussion"

1. Read `knowledge-graph.yml` and `skills.yaml`.
2. Follow `prompts/import.md` to parse, validate, present for review, and add confirmed topics.

### Add

**Triggers**: "add a topic", "add [topic name]", "new topic"

1. Ask the user for:
   - **id**: Snake_case identifier
   - **name**: Human-readable name
   - **type**: Usually `concept`
   - **priority**: P0-P3
   - **difficulty**: 1-4
   - **depends_on**: List of existing node IDs (validate they exist in graph)
   - **description**: 1 sentence
2. Show the proposed node and ask for confirmation.
3. Add to `knowledge-graph.yml`.

## Rules

1. **Always read first**: Read `skills.yaml` and `knowledge-graph.yml` before any workflow.
2. **Never modify `knowledge-graph.yml` without user confirmation**.
3. **Always log changes**: Append to `learning-log.md` whenever a skill level changes.
4. **Create files as needed**: Create `skills.yaml` and `learning-log.md` on first use if they don't exist.
5. **Match topics flexibly**: Match by node ID or name, case-insensitive. If ambiguous, ask.
6. **Refer to prompt files**: Follow the detailed instructions in `prompts/*.md` for each workflow.
