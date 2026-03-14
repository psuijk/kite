# Expand Workflow

## Purpose

Propose new subtopics to deepen coverage of an existing topic in the knowledge graph.

## Steps

### 1. Load Context

- Read the topic's node from `knowledge-graph.yml` — note its current `children`, `description`, `difficulty`.
- Review what subtopics already exist to avoid duplication.

### 2. Propose Subtopics

- Suggest **3-5 new subtopics** that go deeper into the topic.
- For each subtopic, provide:
  - **id**: Snake_case identifier (e.g., `event_sourcing`)
  - **name**: Human-readable name (e.g., "Event Sourcing")
  - **type**: Usually `concept`
  - **difficulty**: Appropriate difficulty level (1-4)
  - **description**: 1 sentence describing the subtopic

### 3. Present to User

Show the proposals in a clear numbered list:

```
1. **event_sourcing** — Event Sourcing (difficulty: 3)
   Storing state changes as an append-only log of events.

2. **cqrs** — CQRS (difficulty: 3)
   Separating read and write models for scalability.
...
```

Ask: "Which of these would you like to add? (e.g., 1, 3, 5 — or 'all')"

### 4. Add Confirmed Subtopics

For each confirmed subtopic:

1. **Add as a new top-level node** in `knowledge-graph.yml`:
   ```yaml
   event_sourcing:
     name: Event Sourcing
     type: concept
     priority: <inherit from parent or ask user>
     difficulty: 3
     description: Storing state changes as an append-only log of events
     depends_on: [parent_topic_id]
     children: []
     related: []
   ```

2. **Add the subtopic's ID to the parent's `children` list**.

### 5. Confirm Before Writing

- Show the user exactly what will be added and where.
- Ask for final confirmation: "Ready to add these to the knowledge graph?"
- Only write to `knowledge-graph.yml` after explicit confirmation.
