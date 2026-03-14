# Personal Learning System

A personal learning system powered by [Claude Code](https://docs.anthropic.com/en/docs/claude-code). No scripts, no dependencies — just open Claude Code in this repo and start talking.

Claude builds a personalized knowledge graph of your domain, tracks your skill levels through quizzes, recommends what to study next, and generates learning plans and projects.

## Getting Started

1. [Install Claude Code](https://docs.anthropic.com/en/docs/claude-code/getting-started) if you haven't already
2. Clone this repo (or fork it)
3. Open Claude Code in the repo directory:
   ```
   cd your-repo
   claude
   ```
4. Say anything — Claude will detect that your knowledge graph doesn't exist yet and walk you through an initialization interview to set up your personalized learning domain

The interview takes about 5 minutes and covers:
- What you want to learn (any domain — engineering, music, finance, etc.)
- Your end goal
- Your current knowledge level across key areas

After that, you're set up with a full knowledge graph and initial skill assessments.

## What You Can Do

Once initialized, just talk naturally. Some examples:

| Say this | What happens |
|----------|-------------|
| "status" | See all your topics, levels, and progress |
| "what should I learn next" | Get a scored recommendation based on priorities and gaps |
| "quiz me on [topic]" | Take a 10-15 question adaptive quiz |
| "learning plan for [topic]" | Get a structured 1-week study plan |
| "project for [topic]" | Get a hands-on project calibrated to your level |
| "expand [topic]" | Add subtopics to go deeper |
| "add [topic]" | Manually add a new topic |
| "import" | Import learnings from other LLM conversations |

## How It Works

Your learning data lives in three files (all generated automatically):

- **`knowledge-graph.yml`** — Your topics, their relationships, priorities, and difficulty ratings
- **`skills.yaml`** — Your assessed skill level per topic (0-4 scale)
- **`learning-log.md`** — Append-only history of all skill changes

The `prompts/` folder contains detailed workflow instructions that Claude follows. You don't need to read them, but you can customize them if you want to change how quizzes work, how topics are scored, etc.

## Skill Levels

| Level | Name | Meaning |
|-------|------|---------|
| 0 | Unaware | Haven't encountered it |
| 1 | Awareness | Know it exists, high-level understanding |
| 2 | Working Knowledge | Can use it with some guidance |
| 3 | Strong | Can apply independently, understand trade-offs |
| 4 | Expert | Deep mastery, can teach and design around it |

## Importing from Other Conversations

If you learn something in a separate LLM chat, you can import those learnings:

1. Open `prompts/discussion-extract.md` and copy the prompt at the bottom
2. Paste it into your other LLM chat at the end of a learning session
3. It will output a YAML block — paste that into Claude Code
4. Claude will match topics to your graph and update your skills

## Customizing

Everything is in plain text files — feel free to edit:

- **`CLAUDE.md`** — The main instructions Claude follows (workflows, rules, triggers)
- **`prompts/*.md`** — Individual workflow details (quiz format, scoring formula, plan structure)
- **`knowledge-graph.yml`** — Add/remove/reorganize topics directly if you prefer

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/getting-started) (requires an Anthropic API key or Claude subscription)
