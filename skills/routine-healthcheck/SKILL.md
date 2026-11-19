---
name: routine-healthcheck
description: Use when auditing scheduled tasks for token waste, deciding how often a task should run, or when the routine-healthcheck scheduled task fires.
---
# Routine healthcheck

Scan the person's scheduled tasks for token waste and misfits. Report what to change. Change a task only after the person picks the fix.

## When to run

- the routine-healthcheck scheduled task fires
- the person asks for a scheduled-task checkup, a token audit, or cheaper runs
- before creating a new scheduled task

## Gather

1. **Local tasks.** Use this session's scheduled-task tools to list them with schedule and status, when those tools exist. Each task's prompt is also on disk at `~/.claude/scheduled-tasks/<task-name>/SKILL.md`; schedule and status are not in that file.
2. **Cloud tasks.** List them with this session's tools when they exist. Otherwise ask the person to run `/schedule list` in Claude Code and paste the output, or note that cloud tasks were skipped.
3. **Agents.** List `~/.claude/agents/` and any project `.claude/agents/` the prompts mention, to check that every agent or skill a prompt names still exists.

For each task note: name, home (local or cloud), trigger, active or paused, and whether the prompt says to stay quiet when nothing changed.

## Flags

Call out each hit with the task name and one fix line.

- **Too frequent.** Denser than hourly, for example every 15 minutes, about 96 runs a day. Prefer hourly or a few times a day. Prefer a GitHub or API trigger on a cloud task when the work starts from an event.
- **Noisy empty runs.** The prompt never says to stay quiet when nothing changed. Add that line.
- **Dead or duplicate.** Paused for weeks, the same job in two tasks, a finite watch past its end condition, or a prompt naming an agent or skill that no longer exists.
- **Wrong home.** A cloud task that needs this computer's files, plugins, or `~/.claude/agents/`, which a cloud run cannot see. A local task that must run while the computer is off.
- **Too much access.** A cloud task carrying connectors its prompt never uses; all connectors are attached by default.
- **No late-run guard.** A local task whose report depends on the time of day. After sleep it gets one catch-up run, possibly hours late.

## Report

One short list: task, flag, suggested fix. When the scheduled task fires and nothing is flagged, end without a report. Offer to apply fixes after the person picks which ones.
