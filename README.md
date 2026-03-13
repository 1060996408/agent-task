# agent-task

## 中文

用于外部编排系统的 agent_task skill 说明与约定，负责读取任务板、调用模型并回写结果。

### 输入
- task_id
- status
- assigned_to
- meta

### 输出
- ok
- task_id
- status
- message

---

## English

Specification for the agent_task skill used by an external orchestrator. It reads the task board, calls the routed model, and writes back results.

### Input
- task_id
- status
- assigned_to
- meta

### Output
- ok
- task_id
- status
- message
