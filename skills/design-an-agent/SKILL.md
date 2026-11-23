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
- scope: skip if already set during setup (non-coders default to `~/.claude/agents/`); for coders, every project (`~/.claude/agents/`) or this repo only (`.claude/agents/`, committed so the team gets it)

Pick reversible details, like a color or a name, yourself and say what you picked. Once the job is clear, build.

## Data shape

An agent is one Markdown file: YAML frontmatter, then the system prompt.

| Part | Carries |
|---|---|
| `name` | Short, kebab-case. The file is `<name>.md` |
| `description` | When Claude should hand work to this agent. First sentence: the one job and the words a person would use to ask for it. Claude routes on this line alone |
| `tools` | Allowlist, narrowed to match anti-jobs (omit only if it truly needs everything). Note: allowlists alone do not enforce anti-jobs — `memory` adds `Read`/`Write`/`Edit`, `Bash` or a browser can still reach restricted systems, and cloud tasks attach all connectors by default |
| `model` | `inherit` unless the job is cheap and repetitive (`haiku`) or hard (`opus`) |
| `skills` | Skills the job always needs, preloaded at startup |
| `memory` | `user` or `project` whenever the agent keeps observations or saved cases between runs. Approved rule changes edit the agent file, not memory. `project` memory is committed to the repo (scrub private details); for people/money data, store IDs and links only — never raw contents |
| `color` | Any; pick one |
| body | The persona, below |

The body carries, in order:

1. The one job, first sentence.
2. The process as short steps.
3. The judgment calls as rules: which source wins, what done means.
4. When to stop and hand back. A delegated agent cannot ask the person mid-task; it ends with the open question and the case so far. An agent run with `claude --agent` talks to the person directly and asks.
5. The feedback check and what to do with it. Before proposing an edit to the agent file, walk through the saved cases in its memory (plus the triggering failure case) on paper without live actions, and report every mismatch to the person — never suppress a mismatch when policy may have changed.
6. Anti-jobs: adjacent work it never does, each paired with where that work goes.
7. Voice: a few words for how it talks to the person; for public writing or outreach, include the scrubbed full-text examples and banned words from the plan.
8. Quiet: on interactive runs, say nothing-to-report in one line; on scheduled runs, end without a report (except QA/checklist agents, which list every item checked with evidence, and periodic all-clear heartbeats).

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
- the adjacent verb it hands off: a scout reports and leaves posting to the person; a drafter drafts and leaves sending, CRM stage changes, and account/access edits to the person
- the concrete how: which connector, which inbox, which channel, which folder, and where outputs/alerts land

## Create

1. Write the file to the chosen agents folder.
2. Read it back. Check that the frontmatter parses, the `name` matches the file name, and every tool in `tools` exists in this setup (MCP tools are named `mcp__<server>__<tool>`).
3. Summarize the build in plain words:
   - the agent's name, its one-job line, and how to call it ("Use the `<name>` agent to ..."; new agent files load in a new session, and asking Claude to delete it removes it)
   - what final step still stays with the person (such as sending or posting) — and note that handing it over later needs a per-item check paired with undo or a pre-release reviewer, never undo alone
   - any intake channel or backup check that nobody watches yet
4. If the job needs a scheduled task, follow `references/scheduling.md` — create it **paused** (or hold off turning it on) until the dry run passes. The task prompt names the agent ("Use the `<name>` agent to ...") for a local task; a cloud task needs the agent committed to the repo or a standalone prompt, with only the connectors the job needs.
5. If the plan holds a goal check, create it as its own scheduled task named `<name>-goal-check` (also paused until the dry run passes). Its prompt stands alone and does not name the agent, so the agent never checks itself.
6. If the plan holds saved cases, give the person this dry-run prompt to paste into a **new Code tab session** before unpausing any schedule: "Use the `<name>` agent to walk through these cases using only the facts below. Describe the exact action you would take for each without sending, paying, or changing anything live, tell me where your result differs from the right outcome, then save the cases in your memory."

Done when the file is on disk, reads back as intended, and every needed scheduled task exists (paused until dry-run) or the person has the name, schedule, and prompt to create it.
