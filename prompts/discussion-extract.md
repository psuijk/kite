# Discussion Extract Prompt

Copy-paste the prompt below into your other LLM chat at the end of a learning discussion. It will generate a structured block you can paste into Claude Code.

**Before pasting**: replace `<PARENT_TOPIC_ID>` with the actual topic ID from your knowledge graph (e.g., `typescript`, `distributed_systems`). Check `knowledge-graph.yml` if unsure.

---

## Prompt to copy

```
Based on our discussion, extract the key topics and subtopics I've been learning about. Output them in the following YAML block format exactly — this will be imported into my learning knowledge graph.

```yaml
# DISCUSSION EXTRACT
parent_topic: <PARENT_TOPIC_ID>
date: <today's date YYYY-MM-DD>
summary: <1-2 sentence summary of what we covered>

topics:
  - id: <snake_case_id>
    name: <Human Readable Name>
    difficulty: <1-4>
    description: <1 sentence>
    depends_on:
      - <parent_topic or other dependency id>
    my_level: <your honest estimate of my understanding: 0-4, see calibration guide below>
    notes: <what I demonstrated understanding of, or gaps you noticed>

  - id: <next_topic>
    ...
```

my_level calibration guide:
- Level 0: Not discussed or I showed no understanding
- Level 1: I heard about it and can describe it at a high level — the minimum for anything discussed
- Level 2: I understand the core concepts and could use it with guidance — this is the expected ceiling for most discussion topics
- Level 3: Only if I demonstrated deep understanding, could explain trade-offs, and caught edge cases myself — rare from a single discussion
- Level 4: Never appropriate from a discussion — requires proven independent mastery over time

Rules:
- Most topics from a single discussion should be level 1-2. Level 3 is rare. Level 4 should never be assigned from a discussion.
- Only include topics we actually discussed in depth, not passing mentions
- Be honest about my_level — base it on the questions I asked and how I engaged with the concepts, using the calibration guide above
- difficulty should reflect the inherent complexity of the topic (1=basic, 4=expert)
- Use snake_case for all IDs
- depends_on should reference the parent topic or other topics from this list that are prerequisites
- Include 3-10 topics depending on how much ground we covered
```
