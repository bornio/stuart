# Dr. Eggbot: install and use

Dr. Eggbot is a plugin for the Claude app that plans a job with you, then builds a Claude agent that does it for you. Installing it takes about a minute, and you don't need the terminal.

> Reading this after unzipping? Install from the original `dr-eggbot.zip`, not from the unzipped folder.

## What you need

- **The Claude desktop app**, signed in. Eggbot builds agents and schedules in the app's **Code** tab.
- **The file** `dr-eggbot.zip`. Keep it zipped.

## Install

1. In the Claude app, open **Customize**, then **Plugins**.
2. Select **Add**, then **Upload plugin**, and choose `dr-eggbot.zip`.
3. Open the **Code** tab and start a new session on any folder. Type `/` and you should see 8 skills that start with `dr-eggbot`.

The plugin is saved to your Claude account, so it also appears in Claude Code on any computer where you're signed in.

Shortcut: drop `dr-eggbot.zip` into a Claude chat and ask it to install the plugin. Claude shows the plugin's contents and asks you to approve before it installs anything.

## First run

In a Code tab session, type `/dr-eggbot:getting-started` and send it. Eggbot asks one question at a time:

1. What to call you, and whether you like it casual or plain.
2. Whether you write code, which decides where new agents are saved: one project, or all your projects.
3. Whether you want the automatic checkups (see below).
4. One job you'd like off your plate. Eggbot starts planning it right away.

After that, you can just describe what you want and Claude will pick the right Eggbot skill on its own.

## Automate a job

In the Code tab, say "I want to stop doing X", or type `/dr-eggbot:automate-anything`. Eggbot plans with you in four stages and only builds at the end:

1. **Goal:** one line on what the work is actually for.
2. **Process:** your steps and the judgment calls you make, tested on three real cases.
3. **Loop:** where you find out how it went, and what should start the work.
4. **Build:** Eggbot creates the new agent and, if the job runs on a schedule, sets up its scheduled task.

**Using the new agent.** It's ready in your next Code tab session. Claude hands it matching work on its own, or you can ask for it by name: "Use the invoice-chaser agent on this week's invoices." To get rid of an agent, ask Claude to delete it.

**Schedules.** Eggbot sets up scheduled tasks for you, and you'll find them in the Code tab under **Scheduled**. A task on your computer runs only while the app is open and the computer is awake. A cloud task runs with the computer off, but it sees only a GitHub repo and your connected apps.

## The checkups

If you said yes during setup, two checkups run on their own. Both stay quiet when there's nothing to report, and neither builds or changes anything until you pick a suggestion.

| Checkup | Runs | Looks for |
| --- | --- | --- |
| transcript-healthcheck | Weekday mornings | Frustration and repeated corrections in your recent Code tab sessions. It suggests a new skill, agent, or scheduled task |
| routine-healthcheck | Monday mornings | Scheduled tasks that run too often, report nothing, are dead, or run in the wrong place |

Both appear in the Code tab under **Scheduled**, where you can pause them or click **Run now**. They run only while the app is open and the computer is awake.

## Update and remove

All of these are in **Customize**, then **Plugins**, then **Dr. Eggbot**:

- **Turn it off:** use the **Disable plugin** toggle.
- **Remove it:** open the plugin's menu and select **Remove**.
- **Update it:** remove the old version, then upload the new zip the same way you installed it.

Agents Eggbot built for you stay after you remove it. The checkup tasks stay too; delete them in the Code tab under **Scheduled**.

## If something doesn't work

| What you see | Try this |
| --- | --- |
| No `dr-eggbot` skills in the `/` menu | Start a new Code tab session, since plugins load when a session starts. Check that the plugin is turned on under **Customize**, then **Plugins** |
| The upload is rejected | Upload `dr-eggbot.zip` exactly as you received it. If you unzipped it and zipped it again, the folder layout may have changed |
| Eggbot plans with you but can't create the agent | Building agents and schedules works only in a Code tab session on your computer, not in a regular chat or a cloud session |
| A checkup didn't run | The app was closed or the computer was asleep. It catches up once when the computer wakes |
| A new agent doesn't show up | Start a new Code tab session, since new agents load when a session starts |

## What's inside

| Skill | Does |
| --- | --- |
| getting-started | First chat: your name and tone, the checkups, one job to automate |
| automate-anything | Runs the whole flow, from goal to built agent |
| find-the-goal | Gets past a step ("send the email") to the outcome it serves |
| capture-the-process | Brain dump, play back, real cases, judgment rules |
| close-the-loop | Feedback sources the agent can read, and a trigger |
| design-an-agent | Writes the agent and its scheduled task |
| transcript-healthcheck | Mines recent chats for friction; suggests skills, agents, or tasks |
| routine-healthcheck | Flags scheduled tasks that waste runs or live in the wrong place |

Plus one agent, `dr-eggbot`, which runs the flow and remembers your name and tone.
