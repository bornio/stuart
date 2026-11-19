---
name: close-the-loop
description: Use when an agent's process is agreed and it needs a way to learn how it is doing and a trigger to run without being asked.
---
# Close the loop

An agent improves when it can see the results of its own work. It runs on its own when something starts it. Set up both before building.

## Feedback

1. Ask: "If you did this yourself, where would you find out it went badly?" Common answers: reviews on Google or Yelp, customer email, social posts, coworker messages, refunds, no-shows.
2. Make each source something the agent can read itself: a connector (Gmail, Slack, Drive and the like), a browser, or a file on the person's computer. If a connector is missing, say which one to connect.
3. Define what the agent does with feedback: match it to the records for that case, find the step that went wrong, and propose a change to the process. The person approves changes. Give the agent a `memory` scope so lessons survive between runs.
4. If the data does not exist, offer to build a small tool that records it. Example: a repair shop logs arrival, first contact, keys handed over, service start, and service end. The wait time then shows where the delay was.
5. Ask what ID links one case across apps: an email address, an order number, a customer ID, a part number. Ask them to use the same ID everywhere. Without a shared ID the agent cannot connect records.

## Trigger

Without a trigger the agent works only when asked, and the person is still the bottleneck.

1. Ask what starts the work today: an email, a chat message, a form, a pull request, a time of day or week.
2. Pick one trigger per job from `../design-an-agent/references/scheduling.md` (relative to this skill's folder). Event triggers suit work that arrives. Schedules suit reviews and reports. Work that arrives by email or chat has no direct event trigger: poll it on a schedule, a few times a day at most, through a connector.
3. Write each as a scheduled task: name, what it does when it fires, where it runs (this computer or the cloud), and when to stay quiet.
4. Add a recurring feedback check, usually weekly, that reads the feedback sources and proposes process changes.

Done when every feedback source is reachable and each scheduled task has a name, a prompt, a home, and a trigger.
