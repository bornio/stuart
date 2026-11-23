# Stuart: install and use

Stuart is a plugin for the Claude app that plans a job with you, then builds a Claude agent that does it for you. Installing it takes about a minute, and you don't need the terminal.

[Read the Stuart blog post](https://bornio.github.io/stuart/) for a walkthrough of how it works.

Stuart is heavily based on [dr eggbot](https://x.ai/bot/_jOdbfkB16zxu7MRcmReE) by [@poteto](https://x.com/poteto).

## What you need

- **The Claude desktop app**, signed in. Stuart builds agents and schedules in the app's **Code** tab — no coding needed, that's just where Claude keeps agents and schedules.

## Install

1. In the Claude app, open **Customize**, then **Plugins**.
2. Select **Add**, then **Add marketplace**, and enter `bornio/stuart`.
3. Stuart now shows up among your plugins. Select it and add it.
4. Open the **Code** tab and start a new session on one empty folder you make for Stuart (such as `Claude` in Documents — avoid picking Desktop or Downloads). Type `/` and you should see 8 skills that start with `stuart:`.

If you use Claude Code in a terminal, run `claude plugin install stuart --marketplace bornio/stuart`.

## First run

In a Code tab session, type `/stuart:getting-started` and send it. Stuart asks one question at a time:

1. What to call you, and whether you like it casual or plain.
2. Whether you write code — non-coders get one default home for all agents; coders choose between this repo or all projects.
3. Whether you want the automatic checkups (see below).
4. One job you'd like off your plate. Stuart starts planning it right away.

After that, you can just describe what you want and Claude will pick the right Stuart skill on its own.

## Automate a job

In the Code tab, say "I want to stop doing X", or type `/stuart:automate-anything`. Stuart plans with you in four stages and only builds at the end:

1. **Goal:** one line on what the work is actually for, and the job's shape: ongoing, time-boxed, repeats per case, on-demand, or one-off.
2. **Process:** your steps and the judgment calls you make, tested on three real cases.
3. **Loop:** where results and alerts land, where you find out how it went, and for jobs that run on a schedule, what starts the work and checks that the goal still holds.
4. **Build:** Stuart creates the new agent and, if the job runs on a schedule, sets up its scheduled tasks paused.

**Before it runs on its own.** Stuart hands you a dry-run prompt. Paste it into a new Code tab session. The agent walks through your saved cases without sending, paying, or changing anything, and tells you where its result differs from the right outcome. When the dry run passes, find the scheduled tasks in the Code tab under **Scheduled**, press **Run now** once, answer the permission prompts, and turn the tasks on.

Choose "always allow" only for reading, saving drafts, updating your own tracker, and notifying yourself. Never choose it for sending to other people, posting, paying, changing CRM or database records, creating accounts, granting access, merging, or deleting.

**Using the new agent.** It's ready in your next Code tab session. Claude hands it matching work on its own, or you can ask for it by name: "Use the invoice-chaser agent on this week's invoices." To get rid of an agent, ask Claude to delete it.

**Schedules & apps.** Turn on app connectors under **Settings → Connectors**. Stuart sets up scheduled tasks for you, and you'll find them in the Code tab under **Scheduled**. A task on your computer runs only while the app is open and the computer is awake. A cloud task runs with the computer off, and uses your connected apps (and a GitHub repo when needed).

## Principles

These are the rules the skills follow. Each one names the skill that carries it.

| Principle | In practice | Skill |
| --- | --- | --- |
| **A step is not a goal.** | People name a step, such as sending the email. Stuart asks what the step is for until the answer is an outcome someone would pay for or miss. The goal outranks the process, so a step that does not serve the goal can go. | find-the-goal |
| **Use what already exists.** | If an app you already pay for does the job itself, use that first. Stuart also checks that the apps have connectors and that the deadline fits the trigger. | automate-anything |
| **Judgment comes from real cases.** | You do most of the job without thinking. Three real cases, one of which went wrong, show which source wins, what done means, and when to hand back. Each answer becomes a rule. | capture-the-process |
| **The saved cases are the test.** | The agent walks through them before its first live run and before any change to its rules. It reports every mismatch, because a mismatch can mean your policy changed. | capture-the-process, design-an-agent |
| **The agent reads its own feedback.** | Stuart asks where you would find out the work went badly, and makes each answer a source the agent can read. Your edits to its drafts count. The agent proposes a rule change and you approve it. | close-the-loop |
| **Results land where you already look.** | Drafts, results, and urgent alerts go to a place you open anyway. Open cases sit in a tracker you already use. | close-the-loop |
| **Something outside the agent checks the goal.** | A stopped agent reports nothing, and an agent cannot report work it never saw. The goal check reads the sources directly and never reads the agent's reports or memory. It runs in a different place from the agent where the job allows, because a check on the same computer sleeps when the agent does. Every scheduled job gets one, even when you still do the final step. | close-the-loop |
| **The final step stays with you first.** | The agent drafts and you send, post, or pay. Handing that step over later needs a check on each item, paired with a way to undo or a reviewer before release. Undo alone is never enough. | design-an-agent |
| **Access enforces the limits.** | Each agent has one job and a list of nearby work it never does. Its tools and connectors are narrowed to match. A tool list alone is not enough, because Bash, a browser, or an unused connector can still reach the restricted system. For people or money data, memory holds IDs and links only. | design-an-agent, capture-the-process |
| **Every run costs, so quiet is the default.** | A run with nothing to report ends without a report. Schedules run as rarely as the goal allows. The exception is a short all-clear when a miss is rare and costly, such as a contract renewal. | close-the-loop, routine-healthcheck |

## The checkups

If you said yes during setup, two checkups run on their own. Both stay quiet when there's nothing to report, and neither builds or changes anything until you pick a suggestion.

| Checkup | Runs | Looks for |
| --- | --- | --- |
| transcript-healthcheck | Weekday mornings | Frustration and repeated corrections in your recent Code tab sessions. It suggests a new skill, agent, or scheduled task |
| routine-healthcheck | Monday mornings | Scheduled tasks that run too often, never stay quiet when nothing changed, are dead, missed a run, or run in the wrong place |

Both appear in the Code tab under **Scheduled**, where you can pause them or click **Run now**. They run only while the app is open and the computer is awake.

## Update and remove

All of these are in **Customize**, then **Plugins**:

- **Update it:** select **Check for updates** on the marketplace you added. Turn on **Sync automatically** to get new versions without asking.
- **Turn it off:** open **Stuart** and use the **Disable plugin** toggle.
- **Remove it:** open **Stuart**, open the plugin's menu, and select **Remove**.

Agents Stuart built for you stay after you remove it. The checkup tasks stay too; delete them in the Code tab under **Scheduled**.

## If something doesn't work

| What you see | Try this |
| --- | --- |
| No `stuart:` skills in the `/` menu | Start a new Code tab session, since plugins load when a session starts. Check that the plugin is turned on under **Customize**, then **Plugins** |
| Claude can't find the marketplace | Check that you entered `bornio/stuart` in **Add marketplace** |
| Stuart plans with you but can't create the agent | Building agents and schedules works only in a Code tab session on your computer, not in a regular chat or a cloud session |
| A checkup didn't run | The app was closed or the computer was asleep. It catches up once when the computer wakes |
| A new agent doesn't show up | Start a new Code tab session, since new agents load when a session starts |

## What's inside

| Skill | Does |
| --- | --- |
| getting-started | First chat: your name and tone, the checkups, one job to automate |
| automate-anything | Runs the whole flow, from goal to built agent |
| find-the-goal | Gets past a step ("send the email") to the outcome it serves |
| capture-the-process | Brain dump, play back, real cases, judgment rules |
| close-the-loop | Delivery channel, feedback sources, trigger, and goal check |
| design-an-agent | Writes the agent and any schedules it needs |
| transcript-healthcheck | Mines recent chats for friction; suggests skills, agents, or tasks |
| routine-healthcheck | Flags scheduled tasks that waste runs or live in the wrong place |

The `stuart:stuart` agent runs the flow and remembers your name and tone.
