---
name: getting-started
description: Use for the first conversation with a new Stuart owner, or when they ask to set up Stuart or its checkups.
---
# Getting started

Say in one line what you do: you design Claude agents, and if they bring a job to automate you plan it with them first, then build an agent that does it.

Ask one at a time, skipping anything already answered:

1. What should I call you, and do you want me casual or plain?
2. Do you write code? If yes, ask whether new agents should default to this repo (`.claude/agents/`, shared with the team) or to all their projects (`~/.claude/agents/`). If no, default to `~/.claude/agents/` (all sessions), save that default so build time never asks about repos, and suggest using one dedicated empty folder (like `Claude` in Documents) for Stuart sessions.
3. Do you want regular checkups that look for friction in your Code-tab sessions (not regular chats) and for wasteful scheduled tasks? If yes, create the two tasks below at the times they pick.
4. What is one job you would like off your plate?

Save their name, tone, and default agent scope. When running as `stuart:stuart`, write them to your memory. Otherwise ask before saving those preferences to their Claude setup file (`~/.claude/CLAUDE.md`) — explain it in plain words without jargon if they do not write code.

For question 4, run automate-anything with their answer.

## Checkup tasks

Both read files on this computer, so both are local scheduled tasks in the Claude desktop app. Create them per `../design-an-agent/references/scheduling.md` (relative to this skill's folder). Suggested times, in the person's local time: weekdays around 8:45, and Mondays around 8:50.

**transcript-healthcheck**, weekdays:

> Look for friction across the owner's Claude Code sessions and agents and propose skills, agents, or scheduled tasks. Run the stuart:transcript-healthcheck skill. Window: since the last successful run, or the last 24 hours if unknown. Report friction and proposals tagged skill, agent, or scheduled task. If there is nothing worth proposing, end without a report. Create nothing from the report alone; wait for the owner to pick.

**routine-healthcheck**, Mondays:

> Flag wasteful or dead scheduled tasks. Run the stuart:routine-healthcheck skill. Report a short list of task, flag, and suggested fix. If there is nothing worth proposing, end without a report. Change a task only after the owner picks the fix.

Done when the name and tone are saved, the checkups exist or were declined, and automate-anything has started on their job.
