# project-agent-docs

`project-agent-docs` 是一个 Codex skill，用于为项目创建或修复面向智能体的轻量文档体系。

它关注三类入口：

- `AGENTS.md`：给 Codex/agent 看的项目地图、约束、验证方式和文档更新触发条件。
- `docs/README.md`：项目文档目录的当前入口，说明哪些文档是有效事实、哪些只是历史记录。
- `docs/reference/*`：长期有效、可复用的系统事实，例如架构边界、数据存储、外部服务和验证策略。

本 skill 的设计参考了 OpenAI 文章《工程技术：在智能体优先的世界中利用 Codex》：

https://openai.com/zh-Hans-CN/index/harness-engineering/

其中关于“将代码仓库设为记录系统”“AGENTS.md 应作为地图而不是百科全书”“面向智能体可读性组织知识”的思路，是本 skill 的主要设计来源。

## 安装

在另一台电脑的 Codex 环境中安装：

```bash
git clone https://github.com/lihao-24/project-agent-docs.git ~/.codex/skills/project-agent-docs
```

安装后重启 Codex，让它重新扫描本地 skills。

如果你的 Codex 使用了自定义 `CODEX_HOME`：

```bash
git clone https://github.com/lihao-24/project-agent-docs.git "${CODEX_HOME}/skills/project-agent-docs"
```

## 适用场景

- 初始化一个新仓库的 `AGENTS.md`。
- 整理已有项目中散落、过期或缺少入口的文档。
- 建立 `docs/README.md` 作为文档导航。
- 将稳定的架构、数据、验证和安全事实沉淀到 `docs/reference/`。
- 标记历史计划、旧规格或过时交接文档，避免未来 agent 误用。

## 复制给 agent 的提示词

把下面这段复制给 Codex 或其他支持本 skill 的 agent，用来让它在当前项目中引入 agent-friendly 文档体系：

```text
请使用 project-agent-docs skill，为当前仓库建立或修复面向 Codex/agent 的项目文档体系。

目标：
- 先检查仓库现有 README、AGENTS.md、docs、源码目录、测试、依赖配置、构建/CI 配置和部署相关文件。
- 不要编造无法从仓库验证的事实；不确定的内容请省略或标注为建议。
- 优先更新现有文件，避免创建重复入口。
- 如果缺少 agent 入口，请创建或更新 AGENTS.md，使它成为简洁的项目地图，而不是长篇百科全书。
- 如果 docs/ 存在或项目文档较多，请创建或更新 docs/README.md，标明当前入口、历史文档和 docs 目录结构。
- 只有在确有稳定、可复用的系统事实时，才创建 docs/reference/*。
- 对明显过时的计划、规格或交接文档添加历史记录说明，不要默认删除。
- 完成后运行轻量验证，例如 git diff --check，并汇报创建/修改的文件、当前文档入口、未确认事实和验证结果。

输出请使用当前项目的主要语言；如果项目已有中文文档，请使用中文。
```

## 文件结构

```text
project-agent-docs/
  SKILL.md
  agents/
    openai.yaml
  assets/
    AGENTS.template.md
    docs-README.template.md
    reference-architecture.template.md
    reference-data-and-storage.template.md
```
