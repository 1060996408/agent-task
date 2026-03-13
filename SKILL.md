---
name: agent-task
description: Execute an agent task for the external orchestrator. Use when handling the agent_task skill request that must read task_board.json, invoke the routed model, write results back, and update task status/errors without modifying OpenClaw core.
---

# agent_task

## Input

Expect JSON params:
- task_id
- status
- assigned_to
- meta (object)

## Workflow

1. Load task_board.json.
2. Find task by task_id; if missing, create with status=blocked and error.
3. Route model by assigned_to (use agent_cluster/agent_router.py mapping).
4. Call model with task context + meta.
5. Persist result to task.meta.result and task.meta.output.
6. On success, advance status to next phase if caller already advanced; otherwise leave as-is.
7. On failure, set status=blocked, increment retry_count, store error in task.meta.error.
8. Write task_board.json.

## Output

Return JSON:
- ok: boolean
- task_id
- status
- message
