# Quiz Workflow

## Purpose

Generate and administer a quiz to assess the user's knowledge level on a topic.

## Steps

### 1. Load Context

- Read the topic's node from `knowledge-graph.yml` — note its `name`, `description`, `children`, `difficulty`, and `depends_on`.
- Read the current skill level from `skills.yaml` (if the file or entry exists). Default to level 0 if not found.

### 2. Generate Questions

- Generate **10-15 questions** that progress from foundational to advanced.
- Cover the topic's children/subtopics broadly to get a thorough read on the user's level.
- Calibrate difficulty to the node's `difficulty` rating:
  - Difficulty 1-2: More conceptual, definition, and basic application questions.
  - Difficulty 3: Mix of conceptual and implementation/design questions.
  - Difficulty 4: Include architecture, trade-off analysis, and edge-case questions.
- Question types to include:
  - **Conceptual**: "What is X? Why does X exist?"
  - **Applied**: "How would you implement X?" / "What happens when Y?"
  - **Analytical**: "Compare X and Y" / "What are the trade-offs of X?"
  - **Debugging**: "Given this scenario, what's wrong and how do you fix it?"

### 3. Administer the Quiz

- Present questions **one at a time**.
- Wait for the user's answer before presenting the next question.
- Do NOT reveal the correct answer after each question — save all evaluation for the end.
- If the user says "skip" or "I don't know", record that and move on.
- Keep the tone encouraging and conversational.

### 4. After All Questions

- Proceed to evaluation using `prompts/evaluate.md`.
