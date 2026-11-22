---
name: design-an-agent
description: Use when designing or creating a new Claude Code agent (subagent file), or giving an agent a scheduled task. Asks a few preference questions, writes a tight agent file, then creates it.
---
# Design an agent

Create the agent. Ship a shareable template only when the person asked for one.

## Intake

If the person brings a job or goal rather than a finished agent spec, run automate-anything first. Its plan becomes the agent file. Skip it when the job, rules, and wake are already clear.

Before asking anything, list `~/.claude/agents/` and the project's `.claude/agents/`. A working sibling agent settles tools, model, and layout; copy it. An agent that already owns this job means extending it beats creating a second one.

Ask only preference questions no experiment can settle. Skip any already answered:

- the one job
- voice and name, if they care
- wake: on demand, a scheduled task, or both
- scope: every project (`~/.claude/agents/`) or this repo only (`.claude/agents/`, committed so the team gets it)

Pick reversible details, like a color or a name, yourself and say what you picked. Once the job is clear, build.

## Data shape

An agent is one Markdown file: YAML frontmatter, then the system prompt.

| Part | Carries |
|---|---|
| `name` | Short, kebab-case. The file is `<name>.md` |
| `description` | When Claude should hand work to this agent. First sentence: the one job and the words a person would use to ask for it. Claude routes on this line alone |
| `tools` | Allowlist. The anti-jobs, enforced: a drafter without send tools cannot send. Omit only when the agent truly needs everything |
| `model` | `inherit` unless the job is cheap and repetitive (`haiku`) or hard (`opus`) |
| `skills` | Skills the job always needs, preloaded at startup |
| `memory` | `user` or `project` when the agent should keep lessons between runs. The feedback loop writes here, and the saved cases live here |
| `color` | Any; pick one |
| body | The persona, below |

The body carries, in order:

1. The one job, first sentence.
2. The process as short steps.
3. The judgment calls as rules: which source wins, what done means.
4. When to stop and hand back. A delegated agent cannot ask the person mid-task; it ends with the open question and the case so far. An agent run with `claude --agent` talks to the person directly and asks.
5. The feedback check and what to do with it. Before it proposes a process change, it reruns the saved cases in its memory and proposes the change only when they still come out right.
6. Anti-jobs: adjacent work it never does, each paired with where that work goes.
7. Voice: a few words. Match the person, or a named character.
8. Quiet: when there is nothing to report, it says so in one line.

Keep it tight: leave out leftover tools, model essays, and "I can also help with".

## Coding agents

Bake into the body:

- short, plain replies
- bug reports get reproduced first, then fixed only after a confirmed repro
- `isolation: worktree` in the frontmatter when the agent edits code alongside the person
- the person's default model, if they named one

When a skill-writing guide such as writing-for-agents or skill-creator is installed, read it before writing the body.

## Non-coding agents

Scout, shopkeep, life admin, dispatcher, writer. Bake into the body:

- the ONLY job, named in the first sentence
- the adjacent verb it hands off: a scout reports and leaves posting to the person, a drafter drafts and leaves sending to the person
- what would let it take that verb over later: a second agent that checks each item before it goes out, or a way to undo it. Until one exists, the verb stays with the person
- the concrete how: which connector, which inbox, which channel, which folder

## Create

1. Write the file to the chosen agents folder.
2. Read it back. Check that the frontmatter parses, the `name` matches the file name, and every tool in `tools` exists in this setup (MCP tools are named `mcp__<server>__<tool>`).
3. If the job needs a scheduled task, follow `references/scheduling.md`. The task prompt names the agent: "Use the <name> agent to ..." for a local task; a cloud task needs the agent committed to the repo or a prompt that stands alone.
4. If the plan holds a goal check, create it as its own scheduled task named `<name>-goal-check`. Its prompt stands alone and does not name the agent, so the agent never checks itself.
5. Tell the person the name, the one-job line, and how to wake it. New agent files load in new sessions. Deleting the file removes the agent.
6. If the plan holds saved cases, give the person a first prompt for the new agent that carries them: "Run these cases, tell me where your result differs from the right outcome, then keep them in your memory."

Done when the file is on disk, reads back as intended, and every scheduled task exists or the person holds the exact line to create it.
