# Waking an agent: triggers and scheduled tasks

Every scheduled run starts a fresh session, so a standing job never piles up on one long chat.

## Pick the home

| Trigger | Home | Fits when |
|---|---|---|
| Person asks | On demand | Ask in plain words ("Use the `<name>` agent to ..."), let Claude route by `description`, or type `@agent-<name>` |
| Time of day or week | Local scheduled task (Claude desktop app) | The job needs files, tools, or plugins on this computer. Runs only while the app is open and the computer is awake |
| Time of day or week | Cloud scheduled task | The job must run with the computer off and uses connected apps (plus a GitHub repo when reading a repo's agent file). Minimum interval 1 hour |
| Pull request, release, other GitHub event | Cloud scheduled task, GitHub trigger | Work that starts in a repo |
| Another system calls in (form tool, webhook, script) | Cloud scheduled task, API trigger | The source can send an HTTP POST |
| Short-lived polling during one session | `/loop` | A watch that ends with the session |

## What each home can reach

- **Local tasks** run with the person's own Claude Code setup: user-scope plugins, `~/.claude/agents/`, local files and MCP servers. A computer asleep through the scheduled time gets one catch-up run on wake, possibly hours late, so prompts whose output depends on the time of day carry a guard: "If it is after 5pm, report only what was missed."
- **Cloud tasks** run on a fresh clone of the chosen repo with the connectors attached to the task. They do not see this computer's files, plugins, or `~/.claude/agents/`. Commit the agent to the repo's `.claude/agents/` or write the prompt so it stands alone. All connectors are attached by default; keep only the ones the job needs.

## Create it

1. Write the task: a kebab-case name, the prompt, the trigger, the home, and where it delivers results. End with when to stay quiet ("If nothing changed, end without a report.") unless it is a QA/checklist report or a periodic all-clear heartbeat for rare, costly misses.
2. Create it with the scheduled-task tools in this session when they exist (tool names containing `scheduled_task`, `trigger`, or `routine`).
3. Without those tools, give the person the name, schedule, and prompt to paste:
   - local: in the Claude desktop app's Code tab, ask "Create a scheduled task on this computer named <name>, <schedule>, with this prompt: <prompt>", or use Scheduled → New task → Only on this computer.
   - cloud: in Claude Code run `/schedule <schedule>, <prompt>`, or use claude.ai/code/routines.
4. Suggest a **Run now** once before the first unattended run so safe permission prompts get "always allow". Safe: read-only checks, saving drafts, updating the owner's own tracking Sheet/Notion table, and notifying the owner only (Slack DM or email to yourself). Never "always allow": external sends, posting, paying, CRM/database workflow mutations, creating accounts or granting access, merging, or deleting.

Done when the task exists, or the person has the name, schedule, and prompt to create it.
