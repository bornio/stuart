---
name: close-the-loop
description: Use when an agent's process is agreed and it needs a way to learn how it is doing, a trigger to run without being asked, and a check that the goal still holds.
---
# Close the loop

An agent improves when it can see the results of its own work. It runs on its own when something starts it. It cannot report work it never saw, so something else checks the goal. Set up all three before building.

## Feedback

1. Ask: "If you did this yourself, where would you find out it went badly?" Common answers: reviews on Google or Yelp, customer email, social posts, coworker messages, refunds, no-shows.
2. Make each source something the agent can read itself: a connector (Gmail, Slack, Drive and the like), a browser, or a file on the person's computer. If a connector is missing, say which one to connect.
3. Define what the agent does with feedback: match it to the records for that case, find the step that went wrong, and propose a change to the process. Before it proposes a change, it reruns the saved cases from capture-the-process through the changed process, and proposes the change only when they still come out right. The person approves changes. Give the agent a `memory` scope so lessons and saved cases survive between runs.
4. If the data does not exist, offer to build a small tool that records it. Example: a repair shop logs arrival, first contact, keys handed over, service start, and service end. The wait time then shows where the delay was.
5. Ask what ID links one case across apps: an email address, an order number, a customer ID, a part number. Ask them to use the same ID everywhere. Without a shared ID the agent cannot connect records.

## Trigger

Without a trigger the agent works only when asked, and the person is still the bottleneck.

1. Ask what starts the work today: an email, a chat message, a form, a pull request, a time of day or week.
2. Ask where else this work can arrive that the trigger will not see: a phone call, a text, a walk-in, a second inbox. Make it a source the agent can read, or write it in the plan as work the agent will miss.
3. Pick one trigger per job from `../design-an-agent/references/scheduling.md` (relative to this skill's folder). Event triggers suit work that arrives. Schedules suit reviews and reports. Work that arrives by email or chat has no direct event trigger: poll it on a schedule, a few times a day at most, through a connector.
4. Write each as a scheduled task: name, what it does when it fires, where it runs (this computer or the cloud), and when to stay quiet.
5. Add a recurring feedback check, usually weekly, that reads the feedback sources and proposes process changes.

## Goal check

A stopped agent reports nothing, and an agent cannot report work it never saw. Quiet then looks the same as all is well. One more scheduled task checks the goal itself.

1. Turn the goal line into a question the sources can answer. Example: does every booking request from the last day have a confirmed slot?
2. Write the task prompt so it stands alone. It reads the sources directly and looks everywhere the work can arrive. It does not name the working agent, and it does not read that agent's reports or memory.
3. It tells the person when the goal failed, or when none of the agent's work has shown up in the sources since the last check. Otherwise it ends without a report.
4. Run it as often as the goal needs and no more, usually daily.
5. Give it a different home from the agent where the job allows: a cloud check for an agent on this computer. A check on the same computer sleeps when the agent does and will not catch a stopped agent. Say so to the person when both must be local.
6. Name it `<agent-name>-goal-check`, so the routine healthcheck does not read it as a duplicate.

Done when every feedback source is reachable, the goal check is written, and each scheduled task has a name, a prompt, a home, and a trigger.
