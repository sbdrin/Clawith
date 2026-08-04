---
kind: external_dependency
name: Redis
slug: redis
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

### Redis
- 内存数据结构存储，用于缓存和会话管理
- 使用 hiredis 客户端库，支持高级数据结构操作
- 在 Docker 部署中使用 Redis 7-alpine 镜像
- verify exact API/params against official docs