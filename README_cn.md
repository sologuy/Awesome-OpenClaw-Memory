# Awesome-OpenClaw-Memory

<p align="center">
    【<a href="README.md">English</a> | 中文】
</p>

<div align="center">
    <img src="assets/banner.png" alt="OpenClaw 记忆生态系统" width="82%">
</div>

[![Awesome](https://awesome.re/badge.svg)](https://github.com/sologuy/Awesome-OpenClaw-Memory)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/badge/PRs-Welcome-red)
[![Papers](https://img.shields.io/badge/论文-2-blue.svg)](#-openclaw-相关论文)
[![Open Source Projects](https://img.shields.io/badge/开源项目-22-green.svg)](#-系统与开源项目)
[![OpenClaw Plugins](https://img.shields.io/badge/OpenClaw%20插件-7-red.svg)](#-openclaw-记忆插件)


## 👋 简介

[OpenClaw](https://github.com/OpenClaw/OpenClaw)（🦞 龙虾）是一个开源的自主 AI 虚拟助理项目，由奥地利软件工程师 Peter Steinberger 开发。2025 年 11 月以 "Clawdbot" 之名在 GitHub 首发，后更名为 "Moltbot"，最终于 2026 年 1 月定名 "OpenClaw"。截至 2026 年 2 月，GitHub 星标数已超过 20 万。OpenClaw 可部署在 macOS/Windows 等本地设备上，调用各种 AI 大模型与 API，通过 WhatsApp、Telegram、Signal、Discord 等即时通讯平台接收用户指令，自主完成日程安排、消息发送、文件整理、代码编写等工作。

OpenClaw 的一大特色是**持久记忆**——它在本地存储配置数据和交互历史，实现跨会话的连续性。然而，这一记忆系统的设计、安全性和可扩展性仍是社区活跃探索的前沿。

**Awesome-OpenClaw-Memory** 是一个精选集合，致力于 OpenClaw 生态系统中的记忆系统、架构和最佳实践。本仓库收集了与增强 OpenClaw 记忆能力相关的研究论文、开源记忆框架和实际实现。

无论你是在扩展 OpenClaw 的内置本地记忆、集成 Mem0 或 Zep 等外部框架，还是在研究 Agent 记忆安全（如记忆投毒攻击）——这里是你的一站式资源。

---

## 🎯 仓库目标

我们的使命是为 OpenClaw 记忆系统构建最全面的知识库，服务于探索 Agent 记忆前沿的研究者和在生产中部署记忆增强 OpenClaw 的实践者。我们旨在加速 OpenClaw 持久记忆能力的发展——从本地交互历史到可扩展、安全的跨会话知识管理。

---

## 📏 项目范围

本仓库聚焦于扩展或增强 OpenClaw 认知能力的记忆机制和系统设计，涵盖理论研究和工程实践。

🌀 包含内容（范围内）
- OpenClaw Agent 的记忆架构设计
- OpenClaw 专属记忆技能和插件
- 可与 OpenClaw 集成的外部记忆框架（Mem0、Zep、Letta、LangMem 等）
- 记忆管理策略（写入、检索、更新、遗忘、压缩）
- 记忆安全（记忆投毒、完整性检查、沙箱隔离）
- OpenClaw 工作流中的多 Agent 共享记忆
- Agent 记忆的评测方法与数据集
- 最佳实践和生产模式

🌀 不包含内容（范围外）
- 与 Agent 记忆无关的通用 LLM 预训练研究
- 与 AI Agent 无关的传统数据库或检索系统
- 对 OpenClaw 无迁移价值的非 Agent 记忆系统

---

## 🔔 最近更新
+ 2026-03-22 - 🎉 新增 mem9（ContextEngine 原生持久记忆，PingCAP/TiDB 创始人出品）
+ 2026-03-21 - 🎉 新增 5 个 OpenClaw 记忆插件（memory-lancedb-pro、openclaw-supermemory、MemOS-Cloud、graph-memory、openclaw-memory-mem0）
+ 2026-03-21 - 🎉 首次发布，收录 2 篇 OpenClaw 论文、22 个开源记忆系统和 Adam 框架

---

## 🗺️ 目录
- [简介](#-简介)
- [仓库目标](#-仓库目标)
- [项目范围](#-项目范围)
- [最近更新](#-最近更新)
- [核心概念](#-核心概念)
- [OpenClaw 相关论文](#-openclaw-相关论文)
- [资源](#-资源)
  - [系统与开源项目](#-系统与开源项目)
  - [OpenClaw 记忆插件](#-openclaw-记忆插件)
  - [OpenClaw 记忆框架](#-openclaw-记忆框架)
- [参与贡献](#-参与贡献)
- [Star 趋势](#-star-趋势)

---

## 🧠 核心概念

- **OpenClaw 内置记忆**：OpenClaw 在用户设备本地存储配置数据和交互历史，提供跨会话的持久记忆。这种本地优先的设计保障了隐私，但随着交互历史的增长，在可扩展性、检索准确性和记忆管理方面带来了挑战。

- **记忆层次**：
  - **会话记忆**：单次对话会话中的活跃上下文，包括当前任务状态和中间推理过程。
  - **交互历史**：本地存储的跨消息平台（WhatsApp、Telegram、Signal、Discord）历史对话和任务执行记录，构成 OpenClaw 的原生长期记忆。
  - **配置记忆**：持久化的用户偏好、API 凭证、技能配置和行为设置。

- **OpenClaw 记忆面临的挑战**：
  - **可扩展性**：随着数月使用中交互历史的积累，高效检索变得至关重要。
  - **跨平台一致性**：在多个消息平台间维护连贯的记忆。
  - **记忆安全**：自主 Agent 面临记忆投毒（通过精心构造的消息注入恶意持久数据）、意图漂移（记忆引发的行为偏移）和隐私泄露等威胁——正如 "Taming OpenClaw" 论文所揭示的。
  - **记忆增强**：集成外部记忆框架（Mem0、Zep、Letta 等）以向量搜索、知识图谱和语义检索来增强 OpenClaw 的原生本地存储。

---

## 📄 OpenClaw 相关论文

<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="width: 15%;">日期</th>
      <th style="width: 55%;">标题</th>
      <th style="width: 15%;">标签</th>
      <th style="width: 15%;">链接</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" style="width: 15%;">2026-03-11</td>
      <td style="width: 55%;"><strong>Taming OpenClaw: Security Analysis and Mitigation of Autonomous LLM Agent Threats</strong></td>
      <td style="width: 15%;">
        <img src="https://img.shields.io/badge/安全-orange" alt="安全">
        <img src="https://img.shields.io/badge/OpenClaw-red" alt="OpenClaw">
      </td>
      <td style="width: 15%;"><a href="https://arxiv.org/pdf/2603.11619v1">
        <img src="https://img.shields.io/badge/arXiv-论文-%23D2691E?logo=arxiv" alt="论文">
      </a></td>
    </tr>
    <tr>
      <td colspan="3">
        • 系统分析了 OpenClaw 等自主大语言模型 Agent 在初始化、输入、推理、决策和执行五个生命周期阶段面临的安全威胁。<br>
        • 以 OpenClaw 为案例详细展示了这些威胁的破坏性。例如，攻击者可以通过"记忆投毒"将瞬时恶意输入转化为长期行为控制；在决策和执行阶段，模糊指令可能触发"意图漂移"，导致 Agent 将简单的安全检查任务升级为破坏性的防火墙修改和高风险命令执行。<br>
        • 缓解策略包括：初始化阶段的插件验证与签名；输入阶段的语义防火墙隔离；推理阶段的动态记忆完整性检查与状态回滚；决策阶段的意图一致性验证；执行阶段的内核级沙箱和最小权限控制。
      </td>
    </tr>
    <tr>
      <td rowspan="2" style="width: 15%;">2026-03-11</td>
      <td style="width: 55%;"><strong>When OpenClaw Meets Hospital: Toward an Agentic Operating System for Dynamic Clinical Workflows</strong></td>
      <td style="width: 15%;">
        <img src="https://img.shields.io/badge/多Agent-orange" alt="多Agent">
        <img src="https://img.shields.io/badge/OpenClaw-red" alt="OpenClaw">
        <img src="https://img.shields.io/badge/医疗-green" alt="医疗">
      </td>
      <td style="width: 15%;"><a href="https://arxiv.org/pdf/2603.11721">
        <img src="https://img.shields.io/badge/arXiv-论文-%23D2691E?logo=arxiv" alt="论文">
      </a></td>
    </tr>
    <tr>
      <td colspan="3">
        • 将 Agent 约束在隔离环境中，只允许读写特定文件和调用预审"医学技能库"，在操作系统层面切断任意代码执行和网络访问，确保数据安全和合规。<br>
        • 不使用传统向量检索，而是将临床文档组织为树状结构并附加清单。Agent 通过自然语言理解阅读这些清单，执行"渐进式披露"导航，从而以精确和可解释的方式获取长期病历上下文。<br>
        • 多个 Agent 不直接通信，而是通过向共享临床文档的追加写入和事件订阅进行隐式协作。这使得 Agent 能够即时协调任务，灵活处理传统系统无法应对的复杂长尾临床需求。
      </td>
    </tr>
  </tbody>
</table>

---

## 📦 资源

### 💻 系统与开源项目

以下系统按**发布日期**排序：

| 系统        | 时间       | Stars | GitHub 与网站 |
|-------------|------------|-------|---------------|
| Zep         | 2023-05-19 | ![GitHub Repo stars](https://img.shields.io/github/stars/getzep/zep?style=social) | https://github.com/getzep/zep<br>https://www.getzep.com/ |
| Agentmemory | 2023-07-07 | ![GitHub Repo stars](https://img.shields.io/github/stars/elizaOS/agentmemory?style=social) | https://github.com/elizaOS/agentmemory<br>无官网 |
| Cognee      | 2023-10-09 | ![GitHub Repo stars](https://img.shields.io/github/stars/topoteretes/cognee?style=social) | https://github.com/topoteretes/cognee<br>https://www.cognee.ai/ |
| Letta       | 2023-10-26 | ![GitHub Repo stars](https://img.shields.io/github/stars/letta-ai/letta?style=social) | https://github.com/letta-ai/letta<br>https://www.letta.com/ |
| Supermemory | 2024-02-22 | ![GitHub Repo stars](https://img.shields.io/github/stars/supermemoryai/supermemory?style=social) | https://github.com/supermemoryai/supermemory<br>https://supermemory.ai/ |
| Memary      | 2024-04-26 | ![GitHub Repo stars](https://img.shields.io/github/stars/kingjulio8238/Memary?style=social) | https://github.com/kingjulio8238/Memary<br>无官网 |
| Second-Me   | 2024-06-26 | ![GitHub Repo stars](https://img.shields.io/github/stars/mindverse/Second-Me?style=social) | https://github.com/mindverse/Second-Me<br>https://home.second.me/ |
| Mem0        | 2024-07-11 | ![GitHub Repo stars](https://img.shields.io/github/stars/mem0ai/mem0?style=social) | https://github.com/mem0ai/mem0<br>https://mem0.ai/ |
| Memobase    | 2024-10-05 | ![GitHub Repo stars](https://img.shields.io/github/stars/memodb-io/memobase?style=social) | https://github.com/memodb-io/memobase<br>https://www.memobase.io/ |
| LangMem     | 2025-01-22 | ![GitHub Repo stars](https://img.shields.io/github/stars/langchain-ai/langmem?style=social) | https://github.com/langchain-ai/langmem<br>https://langchain-ai.github.io/langmem/ |
| A-Mem       | 2025-02-17 | ![GitHub Repo stars](https://img.shields.io/github/stars/agiresearch/A-mem?style=social) | https://github.com/agiresearch/A-mem<br>无官网 |
| Mirix       | 2025-04-16 | ![GitHub Repo stars](https://img.shields.io/github/stars/Mirix-AI/MIRIX?style=social) | https://github.com/Mirix-AI/MIRIX<br>https://mirix.io/ |
| MemEngine   | 2025-05-04 | ![GitHub Repo stars](https://img.shields.io/github/stars/nuster1128/MemEngine?style=social) | https://github.com/nuster1128/MemEngine<br>无官网 |
| MemOS       | 2025-05-28 | ![GitHub Repo stars](https://img.shields.io/github/stars/MemTensor/MemOS?style=social) | https://github.com/MemTensor/MemOS<br>https://memos.openmem.net/ |
| MemoryOS    | 2025-05-30 | ![GitHub Repo stars](https://img.shields.io/github/stars/BAI-LAB/MemoryOS?style=social) | https://github.com/BAI-LAB/MemoryOS<br>https://baijia.online/memoryos/ |
| ReMe        | 2025-06-05 | ![GitHub Repo stars](https://img.shields.io/github/stars/agentscope-ai/ReMe?style=social) | https://github.com/agentscope-ai/ReMe<br>https://reme.agentscope.io/ |
| Nemori      | 2025-06-30 | ![GitHub Repo stars](https://img.shields.io/github/stars/nemori-ai/nemori?style=social) | https://github.com/nemori-ai/nemori<br>无官网 |
| Memori      | 2025-07-24 | ![GitHub Repo stars](https://img.shields.io/github/stars/MemoriLabs/Memori?style=social) | https://github.com/MemoriLabs/Memori<br>https://memorilabs.ai/ |
| MemU        | 2025-08-09 | ![GitHub Repo stars](https://img.shields.io/github/stars/NevaMind-AI/memU?style=social) | https://github.com/NevaMind-AI/memU<br>https://memu.pro/ |
| SuperLocalMemory | 2026-03-01 | ![GitHub Repo stars](https://img.shields.io/github/stars/qualixar/superlocalmemory?style=social) | https://github.com/qualixar/superlocalmemory<br>https://superlocalmemory.com/ |
| MemMachine  | 2025-08-16 | ![GitHub Repo stars](https://img.shields.io/github/stars/MemMachine/MemMachine?style=social) | https://github.com/MemMachine/MemMachine<br>https://memmachine.ai/ |
| MineContext | 2025-09-30 | ![GitHub Repo stars](https://img.shields.io/github/stars/volcengine/MineContext?style=social) | https://github.com/volcengine/MineContext<br>无官网 |
| EverMemOS   | 2025-10-29 | ![GitHub Repo stars](https://img.shields.io/github/stars/EverMind-AI/EverMemOS?style=social) | https://github.com/EverMind-AI/EverMemOS<br>https://evermind.ai/ |
| MemoryBear  | 2025-12-17 | ![GitHub Repo stars](https://img.shields.io/github/stars/SuanmoSuanyangTechnology/MemoryBear?style=social) | https://github.com/SuanmoSuanyangTechnology/MemoryBear<br>https://www.memorybear.ai/ |

### 🔌 OpenClaw 记忆插件

以下插件为 OpenClaw 生态专属，按 **Star 数**排序：

| 插件 | Stars | 简介 | 技术栈 |
|------|-------|------|--------|
| [memory-lancedb-pro](https://github.com/CortexReach/memory-lancedb-pro) | ![GitHub Repo stars](https://img.shields.io/github/stars/CortexReach/memory-lancedb-pro?style=social) | 生产级 LanceDB 混合检索记忆 — Vector + BM25 搜索、Cross-Encoder 重排序、多作用域隔离、管理 CLI | TypeScript |
| [openclaw-supermemory](https://github.com/supermemoryai/openclaw-supermemory) | ![GitHub Repo stars](https://img.shields.io/github/stars/supermemoryai/openclaw-supermemory?style=social) | Supermemory 云端自动召回记忆 — 为 OpenClaw Agent 提供长期记忆和自动召回 | TypeScript |
| [mem9](https://github.com/mem9-ai/mem9) | ![GitHub Repo stars](https://img.shields.io/github/stars/mem9-ai/mem9?style=social) | TiDB 驱动的持久云端记忆 — ContextEngine 生命周期钩子、一虾一库数据隔离、Memory Space 可视化。创始人：黄东旭（PingCAP/TiDB 联合创始人） | TypeScript, Go |
| [MemOS-Cloud-OpenClaw-Plugin](https://github.com/MemTensor/MemOS-Cloud-OpenClaw-Plugin) | ![GitHub Repo stars](https://img.shields.io/github/stars/MemTensor/MemOS-Cloud-OpenClaw-Plugin?style=social) | MemOS 官方云端生命周期记忆 — 执行前召回上下文、运行后保存对话 | JavaScript |
| [graph-memory](https://github.com/adoresever/graph-memory) | ![GitHub Repo stars](https://img.shields.io/github/stars/adoresever/graph-memory?style=social) | 知识图谱上下文引擎 — 提取结构化三元组、压缩上下文 75%、跨会话经验复用 | TypeScript |
| [openclaw-memory-mem0](https://github.com/serenichron/openclaw-memory-mem0) | ![GitHub Repo stars](https://img.shields.io/github/stars/serenichron/openclaw-memory-mem0?style=social) | Mem0 自托管语义提取记忆 — 基于 Mem0 REST API 的 OpenClaw 记忆插件 | TypeScript |

### 🧠 OpenClaw 记忆框架

#### mem9

- **描述：** 基于 TiDB Cloud 的 OpenClaw 持久云端记忆。创始人为黄东旭（PingCAP/TiDB 联合创始人）。首个集成 OpenClaw **ContextEngine** 生命周期 API（OpenClaw 3.7+）的记忆插件。
- **核心特性：**
  - **ContextEngine 钩子**：`before_prompt_build`（每次 LLM 调用前注入记忆）、`before_reset`（重置前保存会话摘要）、`agent_end`（捕获最终响应）——参与完整的记忆生命周期，而非事后召回补丁。
  - **一虾一库**：每个 Agent 独立存储、独立加密、独立密钥，非行级租户隔离。
  - **Memory Space**：在 mem9.ai 的网页上可视化查看龙虾记住了什么——透明、可审查的记忆。
  - **多 Agent 支持**：Claude Code、OpenCode 和 OpenClaw 通过无状态插件 + 云端服务器共享同一记忆池。
  - **可自部署**：使用自己的 TiDB/MySQL 实例部署 mnemo-server，实现完全数据主权。
- **工具**：`memory_store`、`memory_search`、`memory_get`、`memory_update`、`memory_delete`
- **安装**：告诉你的龙虾：`请阅读 https://mem9.ai/SKILL.md 并按照说明安装和配置 mem9`
- **链接：** [GitHub](https://github.com/mem9-ai/mem9) | [官网](https://mem9.ai)

#### Adam Framework

- **描述：** 基于 OpenClaw 构建的 5 层持久记忆与一致性架构，用于本地 AI 助手。解决 AI 遗忘症（跨会话）和会话内一致性退化问题。
- **层次：** Vault 注入、会话中记忆搜索、神经图谱（7219+ 神经元）、每夜 Gemini 调和、带 scratchpad dropout 检测的一致性监控。
- **验证：** 353 个会话、6619 条消息轮次、8 个月由非开发者在真实业务中使用。
- **平台：** Windows/macOS/Linux，OpenClaw，本地优先，模型无关。
- **链接：** [GitHub](https://github.com/strangeadvancedmarketing/Adam) | [在线演示](https://strangeadvancedmarketing.github.io/Adam/) | [交互式证明](https://strangeadvancedmarketing.github.io/Adam/showcase/ai-amnesia-solved.html)

---

## 🤝 参与贡献

欢迎社区贡献！请提交 Issue 或 Pull Request。

**Issue 模板：**
```
标题：[论文/项目标题]
类型：[论文 / 框架 / 技能 / 最佳实践]
发表于：[arXiv / 会议 / GitHub]
摘要：
  - 创新点：
  - 与 OpenClaw 的相关性：
  - 显著结果：
```

**Pull Request 指南：**
- 将新条目添加到适当的章节
- 为每个条目附带简要说明
- 确保链接有效且可访问
- 遵循现有的格式和风格

---

## ⭐ Star 趋势

<a href="https://star-history.com/#sologuy/Awesome-OpenClaw-Memory&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=sologuy/Awesome-OpenClaw-Memory&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=sologuy/Awesome-OpenClaw-Memory&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=sologuy/Awesome-OpenClaw-Memory&type=Date" />
 </picture>
</a>

---

## 📜 许可证

本项目采用 [MIT 许可证](LICENSE) 开源。

---

<p align="center">
  🦞 为 OpenClaw 社区用 ❤️ 构建
</p>
