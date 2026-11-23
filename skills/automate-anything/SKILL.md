---
name: automate-anything
description: Use when someone wants to automate a job, hand work to an agent, or build an agent for a goal. Runs the full flow from goal to a working agent.
---
# Automate anything

Automation is a goal plus a process, with an agent doing the process. This skill turns one person's job into one Claude agent that does it without them.

Run the stages in order. Each stage ends in something the person confirms. Building waits for stage 4.

| Stage | Skill | Done when |
|---|---|---|
| 1. Goal | find-the-goal | The person agrees to a one-line goal and job shape, and the quick feasibility check passes |
| 2. Process | capture-the-process | The person says the played-back process and its judgment calls are right, and the saved cases are in the plan |
| 3. Loop | close-the-loop | The plan has a delivery channel and feedback source; ongoing, time-boxed, and repeats-per-case jobs also have a trigger and goal check |
| 4. Build | design-an-agent | The agent file exists, reads back as planned, and any scheduled tasks exist (paused until dry-run) or the person has the details to create them |

## Rules

- Short messages, plain words. Default to one question per message; group 2–3 quick questions when the person wants to move faster.
- Assume the person is not technical.
- **Quick feasibility check (right after Stage 1, before Stage 2):**
  1. Check which needed apps have connectors; warn plainly on login-walled or anti-bot sites (LinkedIn, Instagram, SSO/2FA) instead of promising browser clicking.
  2. Check if an app they already pay for does this natively (ad-platform rules, budget alerts, Google Alerts) and prefer that first.
  3. Check that any deadline fits the trigger (email/chat polling cannot hit sub-hourly deadlines).
- The goal outranks the process. If a step does not serve the goal, say so and offer to drop it. If the person wants their exact process kept, keep it.
- Stages 1 to 3 are planning only (reading 2–3 past examples without acting is allowed). The job itself waits for the agent.
- Save the running plan to a plan note or memory after each stage so the person can stop and resume: goal, job shape, steps, judgment calls, voice/proof rules (if needed), saved cases, sources, delivery channel, feedback, trigger, goal check. Play the whole thing back once before stage 4.
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
| Apps and sources | `tools`, and which connectors to connect under Settings → Connectors |
| Delivery | Where outputs and alerts land (Gmail draft, Slack DM to self, existing Notion/Sheet) |
| Voice / proof | Body: full-text voice examples (for public writing), source citations (for external facts), or checked-item evidence (for QA checkers) |
| Never-do list | Body: anti-jobs, and tools/connectors narrowed |
| Trigger | For ongoing, time-boxed, or repeats-per-case jobs, a scheduled task per design-an-agent's scheduling reference |
| Goal check | For those scheduled jobs, a separate `<name>-goal-check` task per close-the-loop |
| Saved cases | Tested in a simulated dry run in a new session before unpausing any schedule |

Then confirm any remaining connectors to turn on under **Settings → Connectors**, and hand the person the dry-run prompt to run in a new Code tab session before turning schedules on.
