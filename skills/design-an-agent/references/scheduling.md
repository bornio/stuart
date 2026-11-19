# Waking an agent: triggers and scheduled tasks

Every scheduled run starts a fresh session, so a standing job never piles up on one long chat.

## Pick the home

| Trigger | Home | Fits when |
|---|---|---|
| Person asks | On demand | Claude delegates by the agent's `description`, or the person types `@agent-<name>`, or starts `claude --agent <name>` to talk to it directly |
| Time of day or week | Local scheduled task (Claude desktop app) | The job needs files, tools, or plugins on this computer. Runs only while the app is open and the computer is awake |
| Time of day or week | Cloud scheduled task | The job must run with the computer off and needs only connectors and a GitHub repo. Minimum interval 1 hour |
| Pull request, release, other GitHub event | Cloud scheduled task, GitHub trigger | Work that starts in a repo |
| Another system calls in (form tool, webhook, script) | Cloud scheduled task, API trigger | The source can send an HTTP POST |
| Short-lived polling during one session | `/loop` | A watch that ends with the session |

## What each home can reach

- **Local tasks** run with the person's own Claude Code setup: user-scope plugins, `~/.claude/agents/`, local files and MCP servers. A computer asleep through the scheduled time gets one catch-up run on wake, possibly hours late, so prompts whose output depends on the time of day carry a guard: "If it is after 5pm, report only what was missed."
- **Cloud tasks** run on a fresh clone of the chosen repo with the connectors attached to the task. They do not see this computer's files, plugins, or `~/.claude/agents/`. Commit the agent to the repo's `.claude/agents/` or write the prompt so it stands alone. All connectors are attached by default; keep only the ones the job needs.

## Create it

1. Write the task: a kebab-case name, the prompt, the trigger, the home. Every prompt ends with when to stay quiet: "If nothing changed, end without a report."
2. Create it with the scheduled-task tools in this session when they exist (tool names containing `scheduled_task`, `trigger`, or `routine`).
3. Without those tools, give the person one line to paste:
   - local: in the Claude desktop app's Code tab, ask "Create a scheduled task on this computer named <name>, <schedule>, with this prompt: <prompt>", or use Scheduled → New task → Only on this computer.
   - cloud: in Claude Code run `/schedule <schedule>, <prompt>`, or use claude.ai/code/routines.
4. Suggest a **Run now** once, so permission prompts get answered with "always allow" before the first unattended run.

Done when the task exists, or the person has the exact line to create it.
