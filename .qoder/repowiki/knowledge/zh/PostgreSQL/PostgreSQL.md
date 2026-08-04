---
kind: external_dependency
name: PostgreSQL
slug: postgresql
category: external_dependency
category_hints:
    - vendor_identity
scope:
    - '**'
source_files:
    - docker-compose.yml
    - pyproject.toml
    - setup.sh
---

### PostgreSQL
- 企业级关系型数据库，用于存储 Clawith 的核心数据（用户、Agent、消息、配置等）
- 支持 PostgreSQL 15+ 版本，通过 asyncpg 异步驱动连接
- 默认使用本地实例或外部 PostgreSQL 服务
- verify exact API/params against official docs