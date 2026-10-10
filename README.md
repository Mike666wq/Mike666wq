# 你好，我是 Mike 👋

关注 **Linux、云计算与 DevOps/SRE**，正在探索 **Agent 开发与大模型基础设施**。

这里记录我的技术探索、实践作品和知识整理。目前还在不断学习，希望通过具体项目，把接触到的技术与实际问题联系起来，也让每一次探索留下可以回顾的记录。

## 🧭 关注方向

### 系统与基础设施

- **Linux**：关注系统管理、服务运行与问题排查，逐步理解应用背后的运行环境。
- **云计算与容器**：围绕 Docker 与 Kubernetes 实践应用交付，关注镜像构建、运行配置与服务部署。
- **DevOps**：通过 GitHub Actions 实践 CI/CD，把代码检查、测试、构建与镜像发布串成可重复的流程。
- **SRE**：学习从可观测性、故障排查与可靠性的角度看待系统，关注服务能否持续、稳定地运行。

这些方向彼此相连：应用需要运行环境，部署需要可重复的流程，长期运行则需要对系统状态和故障有足够的理解。

### Agent 与 AI 基础设施

- **Agent 开发**：探索大模型与工具、上下文和工作流的结合，关注如何让模型参与具体任务。
- **大模型基础设施**：关注模型部署、推理服务与资源管理，逐步了解 AI 应用背后的工程支撑。

目前以学习和实践为主。这些是我希望继续深入的方向，也会随着实际探索不断调整。

## 🛠️ 实践作品

### ☀️ [光伏空调可视化](https://github.com/Mike666wq/photovoltaic-air-conditioner)

面向光伏空调实验的数据导入、交互可视化与实时监控项目，也承载了从应用构建、容器交付到 Kubernetes 发布维护的实践。

**主要技术：** React · TypeScript · Node.js · GitHub Actions · Docker · GHCR · Kubernetes

- **持续集成**：PR 与主分支提交触发类型检查、单元测试、实时 API 测试及前端构建；构建生产镜像并执行健康接口、页面与场景读写的容器冒烟检查。
- **容器交付**：Docker 多阶段构建分离构建环境与运行环境，配置健康检查，镜像默认以非 root 用户运行。
- **版本发布**：版本 Tag 触发校验与镜像发布，通过 Buildx 构建并推送 GHCR，记录镜像 digest，将版本号与提交 SHA 注入页面，方便定位运行版本。
- **Kubernetes 运维**：部署文档覆盖镜像更新、发布状态检查、日志查看与修订回滚，以及 PVC 持久化、Secret 和 HTTPS/Ingress 接入配置。

当前流水线自动完成校验、构建和镜像发布，集群更新由人工执行。实时模块采用单副本、Recreate 发布策略，维护时需要考虑内存会话、缓存与持久数据的恢复边界。

→ [CI 工作流](https://github.com/Mike666wq/photovoltaic-air-conditioner/blob/main/.github/workflows/ci.yml) · [镜像发布](https://github.com/Mike666wq/photovoltaic-air-conditioner/blob/main/.github/workflows/release.yml) · [Kubernetes 运维说明](https://github.com/Mike666wq/photovoltaic-air-conditioner/blob/main/deploy/README.md)

### 📚 [个人知识站](https://github.com/Mike666wq/knowledge-web)

基于 VitePress 的个人 Markdown 笔记站，把知识整理与容器化交付结合起来：笔记更新进入构建流程，生成可部署的静态站点镜像。

**主要技术：** VitePress · GitHub Actions · Docker Buildx · GHCR · Nginx

- **构建与发布**：GitHub Actions 在 PR 中验证镜像构建，在主分支更新或版本 Tag 推送后发布 GHCR 镜像；递归检出子模块，确保相关笔记进入构建上下文。
- **质量检查**：镜像构建依次执行笔记同步、Markdown 语法检查与 VitePress 构建，检查失败会中止构建。
- **多阶段镜像**：Node.js 阶段构建静态产物，Nginx 阶段提供站点服务，运行镜像不包含构建工具链。
- **交付与访问优化**：使用 Buildx 与 Actions 缓存加速镜像构建，生成版本及提交标签；Nginx 配置 gzip、哈希资源长期缓存与页面重新验证，并提供容器健康检查。

当前自动化流程止于镜像发布，可通过 Docker 或 Compose 手动部署。这也是把内容更新转化为可重复构建、可追溯交付的一次实践。

→ [镜像构建工作流](https://github.com/Mike666wq/knowledge-web/blob/main/.github/workflows/build-image.yml) · [Dockerfile](https://github.com/Mike666wq/knowledge-web/blob/main/Dockerfile) · [Nginx 配置](https://github.com/Mike666wq/knowledge-web/blob/main/nginx.conf)

---

如果你也对 Linux、云计算、DevOps/SRE 或 Agent 与 AI 基础设施感兴趣，欢迎关注，也欢迎围绕具体项目交流想法。
