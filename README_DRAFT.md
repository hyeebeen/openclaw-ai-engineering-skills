# OpenClaw AI Engineering Skills

> 🚀 **掌握 AI 应用工程核心技能，从理论到生产级实践**
>
> 基于认知敏捷法 RCSW 的系统化学习路径 · 真实业务案例驱动 · 对标顶尖 AI 公司技能要求

[![GitHub stars](https://img.shields.io/github/stars/openclaw/ai-engineering-skills?style=for-the-badge)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)]()
[![Version](https://img.shields.io/badge/version-v0.1.0-blue.svg?style=for-the-badge)]()
[![Discord](https://img.shields.io/badge/Discord-Join-7289da.svg?style=for-the-badge&logo=discord)]()

---

## 📖 目录

- [为什么需要这个项目](#为什么需要这个项目)
- [快速开始](#快速开始)
- [核心特性](#核心特性)
- [学习路径](#学习路径)
- [技能模块](#技能模块)
- [示例项目](#示例项目)
- [面试准备](#面试准备)
- [社区与贡献](#社区与贡献)
- [路线图](#路线图)

---

## 为什么需要这个项目

### 🎯 你遇到的问题

```
❌ 教程碎片化 —— 看了很多文章，但还是不知道如何构建完整的 AI 应用
❌ 缺少实战 —— 示例都是"Hello World"级别，无法应用到真实项目
❌ 面试焦虑 —— 不知道 AI 公司到底考察什么技能，如何准备作品集
❌ 最佳实践缺失 —— 自己摸索踩了很多坑，找不到系统化的指导
```

### ✨ 本项目提供的解决方案

```
✅ 系统化技能树 —— 7 大核心模块，覆盖 AI 应用开发全生命周期
✅ 生产级代码 —— 来自 LogiNexus 真实业务场景，可直接复用
✅ 面试导向 —— 技能矩阵 + 项目创意 + 模拟面试，一站式准备
✅ 最佳实践库 —— 汇集顶尖 AI 公司的工程方法论
```

### 📊 技能矩阵对比

| 技能维度 | 自学 | 培训班 | 本项目 |
|----------|------|--------|--------|
| RAG 系统构建 | 碎片知识 | 基础示例 | ✅ 生产级案例 |
| Agent 设计 | 理论为主 | 单一模式 | ✅ 多种设计模式 |
| Function Calling | 文档阅读 | 简单调用 | ✅ 复杂场景实战 |
| 评估与监控 | 几乎不涉及 | 简单介绍 | ✅ 完整体系 |
| 项目作品集 | 需要自己找 | 固定模板 | ✅ 7+ 真实案例 |
| 面试准备 | 自行搜集 | 通用题库 | ✅ AI 专项题库 |

---

## 快速开始

### 前置要求

- Python 3.10+
- OpenClaw 已安装并配置
- 基础 Python 编程能力

### 5 分钟上手

```bash
# 1. 克隆项目
git clone https://github.com/openclaw/ai-engineering-skills.git
cd ai-engineering-skills

# 2. 安装依赖
pip install -r requirements.txt

# 3. 运行第一个示例（RAG 订单检索）
cd examples/log nexus-rag
python run.py

# 4. 开始学习
# 访问 docs/rag-guide.md 开始第一个模块
```

### 使用第一个技能包

```python
# 在 OpenClaw 中加载 rag-builder 技能
from openclaw.skills import rag_builder

# 初始化 RAG 系统
rag = rag_builder.RAGBuilder(
    vector_store="chroma",
    embedding_model="text-embedding-3-small",
    llm_model="gpt-4o"
)

# 添加文档
rag.add_documents(["docs/product_manual.pdf"])

# 查询
response = rag.query("如何重置订单状态？")
print(response.answer)
```

---

## 核心特性

### 🧠 认知敏捷法 RCSW

我们采用独特的 **RCSW 学习法**，让学习效率提升 3 倍：

| 原则 | 含义 | 本项目中的体现 |
|------|------|----------------|
| **R**apid | 快速上手 | 5 分钟可运行的示例，Docker 一键环境 |
| **C**ontextual | 情境学习 | 每个概念配真实业务场景（LogiNexus 案例） |
| **S**tructured | 结构化路径 | 清晰的学习路线图和检查点 |
| **W**orkshop | 实战工作坊 | 每章末尾的练习和代码审查 |

### 🏗️ 生产级代码质量

```
✅ 完整的错误处理
✅ 单元测试覆盖 > 80%
✅ 类型注解（Type Hints）
✅ 代码格式化（ruff + black）
✅ Docker 容器化部署
✅ 性能优化实践
```

### 📚 三层内容结构

```
┌─────────────────────────────────────────┐
│           理论讲解 (20%)                 │
│   核心概念、架构设计、最佳实践           │
├─────────────────────────────────────────┤
│           实战代码 (50%)                 │
│   完整示例、可运行项目、代码注释         │
├─────────────────────────────────────────┤
│           练习挑战 (30%)                 │
│   动手练习、代码审查、扩展任务           │
└─────────────────────────────────────────┘
```

---

## 学习路径

### 🗺️ 推荐学习顺序

```
Week 1-2: 提示词工程 ──→ 基础技能，快速建立信心
    ↓
Week 3-5: RAG 系统构建 ──→ 核心技能，最重要模块
    ↓
Week 6-8: Function Calling ──→ 核心技能，工具集成
    ↓
Week 9-12: Agent 设计 ──→ 核心技能，综合应用
    ↓
Week 13-14: 评估与监控 ──→ 进阶技能，生产必备
    ↓
Week 15-16: 部署实践 ──→ 进阶技能，上线能力
    ↓
Week 17-18: AI 安全 ──→ 进阶技能，合规意识
```

### 📋 学习检查点

完成每个模块后，你应该能够：

- [ ] 独立实现该模块的核心功能
- [ ] 解释关键设计决策
- [ ] 识别并解决常见问题
- [ ] 将知识应用到新场景

---

## 技能模块

### 📦 7 大核心模块

#### 1. RAG 系统构建 ⭐⭐⭐

```
📚 内容：RAG 架构、向量数据库、检索策略、性能优化
💻 示例：LogiNexus 订单检索系统
🎯 产出：可复用的 RAG 构建器技能包
⏱️ 学时：8 小时
```

[📖 阅读文档](docs/rag-guide.md) | [💻 查看示例](examples/log nexus-rag) | [🔧 使用技能包](skills/rag-builder)

---

#### 2. Agent 设计与编排 ⭐⭐⭐⭐

```
📚 内容：ReAct、Plan-and-Solve、多 Agent 协作、工具调用
💻 示例：自动对账 Agent、客服 Agent
🎯 产出：Agent 编排器技能包
⏱️ 学时：10 小时
```

[📖 阅读文档](docs/agent-guide.md) | [💻 查看示例](examples/auto-reconciliation) | [🔧 使用技能包](skills/agent-orchestrator)

---

#### 3. Function Calling 实战 ⭐⭐⭐

```
📚 内容：Schema 设计、参数验证、错误处理、链式调用
💻 示例：LogiNexus API 集成、数据库查询
🎯 产出：函数调用最佳实践模板
⏱️ 学时：6 小时
```

[📖 阅读文档](docs/function-calling-guide.md)

---

#### 4. 提示词工程与优化 ⭐⭐

```
📚 内容：CLEAR 框架、Few-shot、CoT、提示版本管理
💻 示例：提示词 A/B 测试、自动化优化
🎯 产出：提示词优化器技能包
⏱️ 学时：4 小时
```

[🔧 使用技能包](skills/prompt-optimizer)

---

#### 5. AI 应用评估 ⭐⭐⭐⭐

```
📚 内容：评估指标、自动化测试、人工评估、持续监控
💻 示例：RAG 评估框架、A/B 测试系统
🎯 产出：评估框架技能包
⏱️ 学时：8 小时
```

[📖 阅读文档](docs/evaluation-guide.md) | [🔧 使用技能包](skills/evaluation-harness)

---

#### 6. 部署与监控 ⭐⭐⭐

```
📚 内容：Docker/K8s 部署、性能优化、监控告警、日志分析
💻 示例：生产环境部署配置、监控仪表板
🎯 产出：部署助手技能包
⏱️ 学时：6 小时
```

[📖 阅读文档](docs/deployment-guide.md) | [🔧 使用技能包](skills/deployment-helper)

---

#### 7. AI 安全与合规 ⭐⭐⭐

```
📚 内容：威胁模型、提示注入防御、数据隐私、内容过滤
💻 示例：输入输出过滤中间件、审计日志
🎯 产出：安全检查清单和工具
⏱️ 学时：4 小时
```

[📖 阅读文档](docs/security-guide.md)

---

## 示例项目

### 🎬 完整可运行项目

| 项目 | 难度 | 描述 | 核心技能 |
|------|------|------|----------|
| [LogiNexus RAG](examples/log nexus-rag) | ⭐⭐⭐ | 订单智能检索系统 | RAG、向量搜索 |
| [自动对账](examples/auto-reconciliation) | ⭐⭐⭐⭐ | 财务数据自动核对 | Agent、Function Calling |
| [客服 Agent](examples/customer-support-agent) | ⭐⭐⭐ | 智能客服问答系统 | Agent、RAG |
| [报告生成器](examples/report-generator) | ⭐⭐ | 自动化报告生成 | Function Calling |
| [多 Agent 系统](examples/multi-agent-system) | ⭐⭐⭐⭐⭐ | 复杂工作流编排 | 多 Agent 协作 |

### 每个示例包含

```
✅ README.md - 项目说明和运行指南
✅ docker-compose.yml - 一键运行环境
✅ src/ - 完整源代码（带详细注释）
✅ data/ - 示例数据（可替换）
✅ tests/ - 单元测试
✅ .env.example - 环境变量模板
```

---

## 面试准备

### 🎯 为 AI 公司面试而设计

本项目的面试准备资源基于对以下公司的岗位分析：

- **国际**：OpenAI, Anthropic, Google DeepMind, Meta AI, Microsoft Research
- **国内**：百度文心、阿里通义、腾讯混元、字节豆包、MiniMax、月之暗面

### 📋 技能矩阵图谱

[📖 查看完整技能矩阵](interview-prep/skill-matrix.md)

```
┌─────────────────────────────────────────────────────┐
│              AI 应用工程师技能矩阵                    │
├─────────────────────────────────────────────────────┤
│  基础能力                                           │
│  ├── Python 编程 ████████████░░ 85%                │
│  ├── 数据结构   ██████████░░░░ 70%                │
│  └── 系统设计   ████████░░░░░░ 60%                │
├─────────────────────────────────────────────────────┤
│  AI 核心技能                                         │
│  ├── RAG 系统   ████████████░░ 85% ← 重点          │
│  ├── Agent 设计 █████████████░ 90% ← 重点          │
│  ├── Prompt 工程 █████████████░ 90%                │
│  └── 模型微调   ██████░░░░░░░░ 45%                │
├─────────────────────────────────────────────────────┤
│  工程能力                                           │
│  ├── 代码质量   ████████████░░ 85%                │
│  ├── 测试覆盖   ██████████░░░░ 70%                │
│  ├── 部署运维   ████████░░░░░░ 60%                │
│  └── 安全合规   ████████░░░░░░ 60%                │
└─────────────────────────────────────────────────────┘
```

### 💼 项目创意库

[📖 查看 50+ 项目创意](interview-prep/project-ideas.md)

面试时，一个高质量的项目胜过 10 个玩具项目。我们提供：

- **初级项目**（适合应届生）：文档问答、简单 Agent
- **中级项目**（适合 2-3 年经验）：RAG 系统、多工具 Agent
- **高级项目**（适合资深工程师）：多 Agent 协作、生产级部署

### 🎤 模拟面试题

[📖 查看 100+ 面试题目](interview-prep/mock-questions.md)

```
📝 技术面试题示例

Q1: 设计一个电商订单检索系统，用户可以用自然语言查询订单。
   考察点：RAG 架构、向量数据库、查询优化

Q2: 如何评估 RAG 系统的检索质量？
   考察点：评估指标、测试方法、A/B 测试

Q3: Agent 在执行复杂任务时经常"迷失"，如何解决？
   考察点：Agent 设计模式、任务分解、状态管理

Q4: Function Calling 中如何处理参数验证和错误恢复？
   考察点：Schema 设计、异常处理、重试机制
```

---

## 社区与贡献

### 🌟 为什么贡献这个项目

- **提升影响力**：成为热门开源项目的贡献者
- **深入学习**：教学相长，贡献是最好的学习
- **建立人脉**：连接全球 AI 开发者
- **职业机会**：展示能力给潜在雇主

### 🏆 贡献者激励计划

| 贡献等级 | 要求 | 奖励 |
|----------|------|------|
| 🥉 新手贡献者 | 1 次 PR | Discord 特殊角色 |
| 🥈 活跃贡献者 | 3 次 PR | GitHub 感谢名单 + 贴纸 |
| 🥇 核心贡献者 | 10 次 PR | 周边礼包 + 联合署名 |
| 👑 模块维护者 | 负责一个模块 | 项目 Co-maintainer |

### 🚀 快速贡献指南

```bash
# 1. Fork 项目
# 2. 创建分支
git checkout -b feature/your-feature

# 3. 开发并提交
git commit -m "feat: add new example project"

# 4. 推送并创建 PR
git push origin feature/your-feature
```

[📖 详细贡献指南](CONTRIBUTING.md)

### 💬 加入社区

- **Discord**: [加入服务器]() - 日常交流、求助问答
- **GitHub Discussions**: [参与讨论]() - 功能建议、技术讨论
- **微信群**: [扫码加入]() - 中文社区

---

## 路线图

### 📅 2026 年发布计划

```
v0.1.0 (4 月 15 日)  ✅ MVP 发布
├── RAG 模块完整内容
├── rag-builder 技能包
├── LogiNexus RAG 示例
└── 技能矩阵初版

v0.2.0 (5 月 15 日)  🔄 内容扩展
├── Agent 模块
├── Function Calling 模块
├── 2 个新技能包
└── 面试题库

v0.3.0 (6 月 15 日)  📋 评估与部署
├── 评估模块
├── 部署模块
├── 视频教程
└── 模板库

v1.0.0 (7 月 15 日)  🎉 正式发布
├── 全部 7 个模块
├── 生产级技能包
├── 中英双语文档
└── Product Hunt 发布
```

[📖 查看详细路线图](PROJECT_PLAN.md)

---

## 📬 保持联系

- 📧 **邮件订阅**: 获取最新更新和教程（即将上线）
- 🐦 **Twitter**: [@OpenClawAI]() - 项目动态
- 📱 **微信公众号**: OpenClaw 社区 - 中文内容
- 💼 **LinkedIn**: [OpenClaw]() - 职业机会

---

## 📄 许可证

MIT License - 你可以自由使用、修改和分发，包括商业用途。

[查看完整许可证](LICENSE)

---

## 🙏 致谢

- **OpenClaw 团队** - 提供强大的技能包平台
- **LogiNexus 团队** - 提供真实业务案例
- **所有贡献者** - 让这个项目变得更好

---

<div align="center">

**如果这个项目对你有帮助，请给一个 ⭐ Star！**

[Star 项目](https://github.com/openclaw/ai-engineering-skills) · [报告问题](https://github.com/openclaw/ai-engineering-skills/issues) · [请求特性](https://github.com/openclaw/ai-engineering-skills/discussions)

</div>
