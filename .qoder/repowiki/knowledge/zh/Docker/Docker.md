---
kind: external_dependency
name: Docker
slug: docker
category: external_dependency
category_hints:
    - migration_status
scope:
    - '**'
source_files:
    - docker-compose.yml
    - setup.sh
    - restart.sh
---

### Docker
- 容器化部署平台，支持一键部署整个 Clawith 应用栈
- 包含 PostgreSQL、Redis、Backend、Frontend 等多个服务
- 支持 Docker Compose 编排，自动处理服务依赖关系
- 本地模式和容器化模式并存，可根据环境自动选择