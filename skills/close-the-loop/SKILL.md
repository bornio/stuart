---
name: close-the-loop
description: Use when an agent's process is agreed and it needs a way to learn how it is doing, a trigger to run without being asked, and a check that the goal still holds.
---
# Close the loop

An agent improves when it can see the results of its own work, delivers outputs where the person actually looks, and — for scheduled jobs — runs on a trigger with a separate check on the goal. Set up what the job needs before building.

## Delivery

Ask where results, drafts, and urgent alerts should land: a Gmail draft, a Slack DM to the owner, or an existing Notion page or Google Sheet. Never leave urgent alerts buried only in the Scheduled tab.

## Feedback

1. Ask: "If you did this yourself, where would you find out it went badly?" Common answers: your edits to its drafts before sending or posting, reviews on Google or Yelp, customer email, social posts, coworker messages, refunds, no-shows.
2. Make each source something the agent can read itself: a connector (Gmail, Slack, Drive and the like), a file on the person's computer, or — only where logins and site rules allow — a browser. If a connector is missing, say which one to connect or suggest a simple bridge (such as forwarding alert emails to Gmail).
3. Define how the agent handles feedback: match it to the case records, find the step that went wrong, and propose an edit to the agent file (or to the standalone cloud prompt, if the job runs there). Before proposing, walk through the saved cases plus this new failure on paper without live actions, and report every mismatch — never hide a mismatch when policy may have changed. The person approves changes; approved rules edit the agent file (or prompt), while memory holds observations and saved cases only.
4. For multi-step follow-ups, repeats-per-case, or threshold monitors (such as marking a SKU "PO Pending" to stop repeat alerts), keep open status in a tracker the person already opens (a Notion table, Google Sheet, or CRM field). Only if no tracker exists, offer to build a small one.
5. Ask what ID links one case across apps: an email address, an order number, a customer ID, a part number. Ask them to use the same ID everywhere; when records cannot share a clean ID, write a conservative stop-and-ask rule so the agent never guesses on money or customers.

## Trigger

For ongoing, time-boxed, or repeats-per-case jobs, without a trigger the agent works only when asked and the person is still the bottleneck. Skip triggers for one-off or on-demand jobs.

1. Ask what starts the work today: an email, a chat message, a form, a pull request, a time of day or week.
2. Ask where else this work can arrive that the trigger will not see: a phone call, a text, a walk-in, a second inbox. Make it a source the agent can read, or write it in the plan as work the agent will miss.
3. Pick the right trigger from `../design-an-agent/references/scheduling.md` (relative to this skill's folder). Event triggers suit work that arrives. Schedules suit reviews, reports, and daily sweeps over repeats-per-case trackers. Work that arrives by email or chat has no direct event trigger: poll it on a schedule, a few times a day at most, through a connector.
4. Write each as a scheduled task: name, what it does when it fires, where it runs (this computer or the cloud), where it delivers results, and when to stay quiet. For time-boxed jobs, add "After <date>, report that this task can be deleted."
5. Add a calendar feedback review (usually weekly or monthly) only when the job needs one; otherwise let failures trigger feedback review so routines stay lean.

## Goal check

Needed for ongoing, time-boxed, and repeats-per-case jobs — even when the final send or post stays with the person. Skip for one-off or on-demand jobs. A stopped agent reports nothing, and an agent cannot report work it never saw. Quiet then looks the same as all is well. One more scheduled task checks the goal itself.

1. Turn the goal line into a check that preserves its deadline and spans outages. Example: for "confirmed slot within 4 hours during business hours", check whether any booking request older than 4 business hours is still unconfirmed (not just "from the last day", which misses the deadline and flags brand-new requests).
2. Write the task prompt so it stands alone. It reads the sources directly and checks every readable channel where work can arrive (noting any unreadable channel from Trigger step 2 as a known blind spot). It does not name the working agent, and it does not read that agent's reports or memory.
3. Deliver alerts to the chosen delivery channel when the goal failed, when a source could not be read, or when a fixed scheduled obligation was missed. A quiet period where sources were read cleanly and nothing is overdue is healthy — end without a report. Exception: when misses are rare and costly (such as contract auto-renewals), send a short periodic all-clear heartbeat listing the next upcoming deadlines.
4. Run it as often as the goal needs and no more, usually daily.
5. Give it a different home from the agent where the job allows: a cloud check for an agent on this computer. A check on the same computer sleeps when the agent does and will not catch a stopped agent. Say plainly to the person when both must be local, or when nothing independent watches the checker itself.
6. Name it `<agent-name>-goal-check`, so the routine healthcheck does not read it as a duplicate.

Done when the delivery channel is set, every feedback source is reachable, and any needed trigger and goal check each have a name, a prompt, a home, and a schedule.
