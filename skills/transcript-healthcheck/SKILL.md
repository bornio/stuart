---
name: transcript-healthcheck
description: Use when auditing Claude Code session transcripts for user friction and proposing new skills, agents, or scheduled tasks, or when the transcript-healthcheck scheduled task fires.
---
# Transcript healthcheck

Scan Claude Code transcripts on this computer for user friction in a time window. Propose new skills, agents, or scheduled tasks only when evidence earns them. Create nothing until the person picks a proposal.

## When to run

- the transcript-healthcheck scheduled task fires
- the person asks for a checkup, a friction audit, or "what should we automate"

## Window

1. Read `last_transcript_healthcheck` from `~/.claude/dr-eggbot/state.json`. The window runs from that time to now.
2. Without it, use the last 24 hours, unless the task or the person names another window.
3. Transcripts older than the retention period (30 days by default) are gone; say so if the window reaches past it.

## Corpus

- Sessions: `~/.claude/projects/<project>/<session-id>.jsonl` (under `$CLAUDE_CONFIG_DIR` instead of `~/.claude` when that is set). `<project>` is the working directory path with every non-alphanumeric character turned into `-`, so it names the project.
- Skip everything under a `subagents/` folder: those are delegated runs with no person typing.
- Keep files modified inside the window, newest first.
- The line format is internal to Claude Code and changes between versions. Open one file and read a few lines before mining, then tell each miner how a person-typed message looks in this version: a user-role entry whose content is text the person wrote, as opposed to tool results, command output, or injected meta entries.
- Skip sessions whose only person message is a scheduled-task prompt.

State the window, the project count, and the session count before mining.

## Mine

Fan out parallel subagents, each with a slice of transcript paths and the format note. Keep only their findings in the main thread. Each returns one block per project with person traffic in the window:

- project name
- what the person was trying to get done
- friction signals, each with a short quote
- repeated corrections and misunderstandings
- which agents or skills were in play, from the Agent and Skill tool calls
- candidate gaps, each tagged skill, agent, or scheduled task

Friction looks like: frustration, "stop", "wrong", "i said", "undo", the same instruction restated, the person doing work an agent should own, Claude asking questions an experiment could settle, a delegated agent's result being redone by hand, abandoned threads.

## Report

Lead with at most 5 bullets. Then a short list of proposals, each tagged skill, agent, or scheduled task, with the evidence that earned it.

When the scheduled task fires and nothing is worth proposing, end without a report.

After a successful run, write the current time to `last_transcript_healthcheck` in `~/.claude/dr-eggbot/state.json`, creating the file if needed and keeping its other keys.

## Implement, after the person picks

1. Skills: write a generic skill in `~/.claude/skills/<name>/SKILL.md`, or the repo's `.claude/skills/` for a team convention. Use writing-for-agents or skill-creator if installed.
2. Agents: use design-an-agent.
3. Scheduled tasks: use design-an-agent's scheduling reference.
