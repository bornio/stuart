---
name: automate-anything
description: Use when someone wants to automate a job, hand work to an agent, or build an agent for a goal. Runs the full flow from goal to a working agent.
---
# Automate anything

Automation is a goal plus a process, with an agent doing the process. This skill turns one person's job into one Claude agent that does it without them.

Run the stages in order. Each stage ends in something the person confirms. Building waits for stage 4.

| Stage | Skill | Done when |
|---|---|---|
| 1. Goal | find-the-goal | The person agrees to a one-line goal that names an outcome, not a step |
| 2. Process | capture-the-process | The person says the played-back process and its judgment calls are right, and the plan holds the saved cases |
| 3. Loop | close-the-loop | The agent has a feedback source, a trigger, and a goal check |
| 4. Build | design-an-agent | The agent file exists, reads back as planned, and its scheduled tasks exist or the person holds the lines to create them |

## Rules

- One question per message. Short messages. Plain words.
- Assume the person is not technical. When they doubt an agent can do a step, say what the agent would actually do: click through the site in a browser, read the inbox through a connector, open the spreadsheet, write a small script.
- The goal outranks the process. If a step does not serve the goal, say so and offer to drop it. If the person wants their exact process kept, keep it.
- Stages 1 to 3 are planning only. The job itself waits for the agent.
- Keep a running plan in your own notes: goal, steps, judgment calls, saved cases, sources, feedback, trigger, goal check. Play the whole thing back once before stage 4.
- If the person already answered a stage elsewhere in the chat, play it back and confirm instead of asking again.

## Build

Hand the plan to design-an-agent. The plan maps onto the agent file:

| Plan | Agent file |
|---|---|
| Goal | `description` first sentence, and the body's first line |
| Steps | Body: process |
| Judgment calls | Body: rules, including which source wins and what done means |
| When to ask | Body: when to stop and hand back |
| Feedback | Body: feedback check, plus a `memory` scope |
| Apps and sources | `tools`, and which connectors to connect first |
| Never-do list | Body: anti-jobs, and tools left out |
| Trigger | A scheduled task created per design-an-agent's scheduling reference |
| Goal check | A second scheduled task, `<name>-goal-check`, whose prompt stands alone and does not name the agent |
| Saved cases | The first prompt for the new agent, which runs them and keeps them in its memory |

Then tell the person which connectors to connect first.

After building, offer two things: one review of the process against the goal with a simpler way, if there is one; and a dry run of the new agent on the saved cases in a new session.
