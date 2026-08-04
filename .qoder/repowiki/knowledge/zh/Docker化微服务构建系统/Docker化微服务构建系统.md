---
kind: build_system
name: Docker化微服务构建系统
category: build_system
scope:
    - '**'
source_files:
    - backend/Dockerfile
    - frontend/Dockerfile
    - docker-compose.yml
    - backend/pyproject.toml
    - frontend/package.json
    - .github/workflows/release.yml
    - backend/entrypoint.sh
    - helm/clawith/values.yaml
---

# Docker化微服务构建系统

Clawith项目采用基于Docker的现代化构建和部署系统，通过多阶段Dockerfile、Docker Compose和Helm Charts实现完整的CI/CD流程。

## 构建系统架构

### 后端构建 (Python)
- 使用多阶段Dockerfile构建，分为`deps`和`production`两个阶段
- 依赖管理使用`pyproject.toml`配合`pip`安装
- 基于Python 3.12-slim镜像，预装了PostgreSQL客户端、Cairo图形库、Chromium浏览器等必要组件
- 支持自定义PyPI镜像源，通过环境变量`CLAWITH_PIP_INDEX_URL`和`CLAWITH_PIP_TRUSTED_HOST`配置

### 前端构建 (React/Vite)
- 使用Node.js 20-alpine作为构建基础镜像
- 构建过程分为两阶段：`build`阶段执行`npm run build`生成静态资源，然后复制到Nginx镜像中
- 使用特定版本的Nginx (1.31.2-alpine)以避免Docker seccomp配置问题

## 核心构建配置

### Docker Compose部署
- 定义了完整的多服务架构：PostgreSQL、Redis、Backend、Frontend
- 支持构建时传递参数，如PyPI镜像配置
- 包含健康检查机制，确保服务正常启动
- 配置了适当的权限和安全选项，包括特权模式和系统级权限

### CI/CD流水线
- GitHub Actions工作流定义在`.github/workflows/release.yml`
- 实现自动版本发布，支持自动检测版本类型（major/minor/patch）
- 集成AI辅助生成发布说明
- 自动更新`backend/VERSION`和`frontend/VERSION`版本文件

### Helm Charts部署
- 提供完整的Kubernetes部署方案
- 包含所有必需组件：后端、前端、PostgreSQL、Redis
- 支持持久化存储配置
- 可配置的资源限制和副本数量

## 构建约定与约束

### 版本管理
- 后端和前端分别维护VERSION文件
- 使用语义化版本控制
- 发布流程自动更新版本号

### 入口脚本机制
- 后端使用`entrypoint.sh`脚本处理容器启动逻辑
- 自动执行数据库迁移(Alembic)和LangGraph检查点初始化
- 实现权限修复和用户切换机制
- 支持不同进程角色(`PROCESS_ROLE`)的差异化启动

### 环境配置
- 通过环境变量进行配置管理
- 支持多种部署场景：Docker Compose、Kubernetes、源码部署
- 预设了合理的默认值，同时允许完全自定义配置

该构建系统体现了现代云原生应用的特点：容器化、微服务架构、自动化部署和版本管理。