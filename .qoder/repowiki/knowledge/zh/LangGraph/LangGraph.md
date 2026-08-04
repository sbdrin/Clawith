---
kind: external_dependency
name: LangGraph
slug: langgraph
category: external_dependency
category_hints:
    - framework_behavior
scope:
    - '**'
source_files:
    - pyproject.toml
    - app/main.py
---

### LangGraph
- Agent 运行时框架，基于 LangGraph 构建确定性的 Agent 执行图
- 支持状态图节点: control_guard → compact → model → tool → verify → wait → terminal
- 提供检查点系统，支持 Postgres 持久化
- verify exact API/params against official docs