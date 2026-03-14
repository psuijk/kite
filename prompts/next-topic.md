# Next Topic Workflow

## Purpose

Recommend the best topics to study next based on the knowledge graph and current skill levels.

## Scoring Formula

For each node in the graph, compute a **recommendation score** from 0.0 to 1.0:

```
score = (priority_weight * 0.30)
      + (growth_potential * 0.25)
      + (dependency_readiness * 0.25)
      + (staleness * 0.10)
      + (difficulty_fit * 0.10)
```

### Components

#### Priority Weight (30%)

Map the node's `priority` field:

| Priority | Weight |
|----------|--------|
| P0       | 1.0    |
| P1       | 0.7    |
| P2       | 0.4    |
| P3       | 0.2    |

#### Growth Potential (25%)

```
growth_potential = (4 - current_level) / 4
```

- Skip topics already at level 4 (growth potential = 0).
- Untested topics (level 0) have maximum growth potential of 1.0.

#### Dependency Readiness (25%)

```
readiness = (number of depends_on nodes at level >= 2) / (total depends_on nodes)
```

- If a node has no dependencies, readiness = 1.0.
- **Hard penalty**: If readiness < 0.5, multiply the entire readiness component by 0.3.

#### Staleness (10%)

```
staleness = min(days_since_last_tested / 90, 1.0)
```

- Untested topics get staleness = 0 (they aren't "stale", they're "new").
- Topics tested long ago get higher staleness, encouraging re-assessment.

#### Difficulty Fit (10%)

Prefer topics whose `difficulty` is approximately `current_level + 1` (i.e., slightly challenging):

```
difficulty_fit = 1.0 - min(abs(difficulty - (current_level + 1)) / 3, 1.0)
```

## Steps

### 1. Load Data

- Read all nodes from `knowledge-graph.yml`.
- Read all skill entries from `skills.yaml` (default to level 0, no test date for missing entries).

### 2. Score Every Node

- Compute the score for each node using the formula above.
- Exclude nodes at level 4.

### 3. Present Recommendations

Show the **top 3-5** topics sorted by score. For each, display:

- **Topic name** and current level
- **Score** (rounded to 2 decimals)
- **Reasoning**: 1-2 sentences explaining why this topic ranks high (e.g., "High priority, no dependencies, not yet tested").
- **Suggested action**: "Take a quiz", "Review fundamentals first", etc.
