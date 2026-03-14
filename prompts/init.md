# Initialization Workflow

## Purpose

Interview the user to understand their learning domain and goals, then build a personalized knowledge graph from scratch.

## Phases

### Phase 1: Domain & Goals

Ask these questions one at a time, conversationally:

1. **What do you want to learn?** Get the broad domain — e.g., "backend engineering", "machine learning", "music theory", "finance", "game development".
2. **What's your end goal?** Something concrete — e.g., "get a senior backend role", "build my own trading bot", "pass the AWS SA exam", "compose my own music".
3. **How would you describe your current level?** Offer anchors:
   - Complete beginner (never touched this field)
   - Some experience (dabbled, done tutorials)
   - Intermediate (working in the field but have gaps)
   - Advanced in parts (strong in some areas, weak in others)

### Phase 2: Existing Knowledge Probe

Based on the domain they described:

1. Identify **5-8 key pillars** of the field. These are the major areas that any practitioner would need to know. For example:
   - Backend engineering → HTTP/APIs, databases, auth, system design, testing, deployment, language fundamentals, concurrency
   - Machine learning → linear algebra, statistics, supervised learning, neural networks, data preprocessing, model evaluation, frameworks
   - Music theory → rhythm, scales/modes, harmony, chord progressions, counterpoint, form/structure, ear training

2. For each pillar, ask: **"How familiar are you with [pillar]? Can you describe what it involves or how you've used it?"**

3. Based on their answers, estimate an initial skill level (0-4) for each:
   - Vague or no answer → Level 0-1
   - Can describe concepts but hasn't applied them → Level 1
   - Has used it, can explain core ideas → Level 2
   - Demonstrates depth, mentions trade-offs → Level 3
   - Expert-level insight, nuanced understanding → Level 4

### Phase 3: Priority & Scope

1. **"Of the areas we discussed, which feel most urgent or important to you?"** — This informs P0 vs P1 priorities.
2. **"Are there specific subtopics you know you want to go deep on?"** — These become candidates for expansion.
3. **"Anything you explicitly want to exclude or defer for now?"** — These become P3 or are left out entirely.

### Phase 4: Graph Assembly

Based on all the information gathered, assemble a knowledge graph:

1. **Create 15-30 nodes** covering the domain:
   - Major pillars as top-level nodes
   - 2-4 subtopics (children) per major pillar
   - Proper `depends_on` chains (foundational topics → advanced topics)

2. **Assign priorities**:
   - **P0**: Directly aligned with the user's stated goal
   - **P1**: Important supporting topics
   - **P2**: Useful but not urgent
   - **P3**: Explicitly deferred or out of scope for now

3. **Assign difficulty ratings** (1-4):
   - 1: Foundational, accessible to beginners
   - 2: Requires some prior knowledge
   - 3: Intermediate, involves trade-offs and design decisions
   - 4: Advanced, requires deep understanding

4. **Present the proposed graph** to the user as a readable summary:
   ```
   Domain: [domain]
   Goal: [goal]
   Total topics: [count]

   P0 — Core (goal-aligned):
     - topic_name (difficulty: X) — description
       Children: subtopic_1, subtopic_2
       Depends on: other_topic
     ...

   P1 — Important:
     ...

   P2 — Supporting:
     ...

   P3 — Deferred:
     ...
   ```

5. **Ask for confirmation**: "Does this look right? You can add, remove, or adjust any topics before I save it."

6. After confirmation, **write `knowledge-graph.yml`** using this format for each node:
   ```yaml
   topic_id:
     name: Topic Name
     type: concept
     priority: P0
     difficulty: 2
     description: One sentence description
     depends_on: [dependency_id]
     children: [child_id_1, child_id_2]
     related: []
   ```

### Phase 5: Initial Skills Snapshot

1. **Write `skills.yaml`** with entries for every topic where the user demonstrated knowledge during Phase 2:
   ```yaml
   topic_id:
     level: <estimated_level>
     confidence: 0.4
     last_tested: <today's date>
   ```
   Use confidence 0.4 since these are conversational estimates, not formal quiz results.

2. **Create `learning-log.md`** with initialization entries:
   ```markdown
   # Learning Log

   ## <today's date>

   - Initialized knowledge graph for [domain]
   - Initial skill levels set from onboarding conversation (confidence: 0.40)
   - **topic_1**: Level 0 -> <level> (confidence: 0.40)
   - **topic_2**: Level 0 -> <level> (confidence: 0.40)
   ...
   ```

3. **Suggest next steps**:
   - "Your knowledge graph is ready! Here's what you can do next:"
   - "Say **status** to see your full topic overview"
   - "Say **what should I learn next** for a personalized recommendation"
   - "Say **quiz me on [topic]** to get a formal assessment on any topic"

## Guidelines

- Keep the conversation natural and encouraging — this is onboarding, not an exam.
- Don't overwhelm with too many questions at once. Ask in batches of 1-3.
- If the user's domain is something you're less familiar with, be honest and collaborate with them on identifying the right pillars.
- Err on the side of more topics rather than fewer — the user can always defer topics to P3.
- Make sure every node has a clear, concise description.
- Validate that dependency chains make sense (don't have advanced topics depending on nothing).
