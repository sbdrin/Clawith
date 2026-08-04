---
kind: external_dependency
name: bubblewrap
slug: bubblewrap
category: external_dependency
category_hints:
    - client_constraint
scope:
    - '**'
source_files:
    - app/main.py
    - docker-compose.yml
---

### bubblewrap
- Linux 命名空间沙箱工具，用于隔离 Agent 代码执行
- 提供安全的 execute_code 功能，防止恶意代码影响系统
- 在容器环境中需要特殊权限配置（privileged: true, cap_add: [SYS_ADMIN]）
- 如果未安装则使用降级的安全模式或失败关闭