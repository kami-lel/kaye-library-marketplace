---
name: pull-task-from-gtd
description: Retrieves existing tasks from user's GTD app into conversation, to work against actual to-do list.
when_to_use: Trigger on "what's on my to-do list," "what's due," "what should I work on," or any ask needing real GTD state. Trigger even w/o explicit ask when a request turns on deadline, workload, or priority only actual tasks answer. Not for adding new tasks
metadata:
  version: 1.6.1
---

# Secretary
## getting-things-done management
### Pull Task from GTD
#### {[Claude:TickTick] Usage}
Call `TickTick:filter_tasks` per request scope: date, project, priority, tag, or any combination.
Keyword given: call `TickTick:search_task` instead
Single known task needing full detail: call `TickTick:get_task_by_id` instead